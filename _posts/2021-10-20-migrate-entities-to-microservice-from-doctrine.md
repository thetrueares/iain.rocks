---
layout: post
slug: migrate-entities-to-microservice-from-doctrine
title: Migrate Entities to Microservice From Doctrine
date: '2021-10-20'
authors: [iain]
categories: ['PHP']
---
Doctrine is one of the most used ORMs in PHPLand, with many applications heavily coupled to it. With more and more companies moving to microservices one of the tasks is to migrate their entities to come from the microservice instead of from Doctrine. Here I’ll describe how I migrated an entity so that it was stored in a Microservice instead of MySQL and came from Doctrine. In my approach I used the original entity class, this allowed for using feature flags for migrating each repository method one at a time. As well as, reducing the amount of refactoring that had to be done.

Because Doctrine either uses Annotations or YML configuration the entity class itself isn’t coupled to Doctrine. Normally, what happens is the code becomes coupled to the magic entity that is returned by Doctrine that actually extends the original class and adds the magic of lazy fetching associated entities.

## Step 0. Have automated tests

I have this as step 0 because hopefully you already have some automated tests. If not, you should identify the core functionality you want to ensure remains. And write automated end-to-end tests. This way you can ensure that when you migrate things, your functionality remains functioning.

## Step 1. Wrap the Doctrine repository

The overall aim here is to make it so that no code is directly using doctrine for the entity that is being migrated. So this means creating a class that wraps the Doctrine entity completely. This helps avoid accidental usage of Doctrine’s many methods.

```php
interface BlogPostRepostiory {
  public function save(BlogPost $BlogPost);

  public function findOneById($id): BlogPost;
}

class DoctrineBlogPostRepository implements BlogPostRepostiory {

  public function __construct(ObjectRepository $doctrineRepository) {
      // ...
  }

  public function save(BlogPost $BlogPost) {
     // ...
  }

  public function findOneById($id): BlogPost {
    // ...
  }
}
```

## Step 2. Find all direct usages of Doctrine
Once you’ve created your wrapper class you can start migrating direct calls to Doctrine to the wrapper class. You may in older systems find that you have query builder code in places that result in fetching, as well as, calls to the EntityManager, and ObjectRepository.

```php
// Example usage:

public function readBlogPostAction(int $id): Response {
  $qb = $this->blogPostRepostiory->createQueryBuilder("bp")
    ->where("bp.id = :id")
    ->andWhere("bp.status = 'active'")
    ->setParameters(['id' = > $id]);
  $blogPost = $qb->getQuery()->getOneOrNullResult();
  return ViewResponse($blogPost);
}

// Repository Method

public function getActiveBlogPostById(int $id): ?BlogPost {
    $qb = $this->doctrineRepository->createQueryBuilder("bp")
      ->where("bp.id = :id")
      ->andWhere("bp.status = 'active'")
      ->setParameters(['id' = > $id]);
    return $qb->getQuery()->getOneOrNullResult();
}

// Refactored usage:
public function readBlogPostAction(int $id): Response {
  $blogPost = $this->blogPostRepostiory->getActiveBlogPostById($id);
  return ViewResponse($blogPost);
}
```

While we could probably improve the code that we moved, all we care about is isolating it into a single place. Why refactor code you’re literally working to remove? This is why I advocate that you just copy and paste the code into your new class.

Remember every method you add to your new repository class you need to add to your interface to make sure your new implementation will have this method.

## Step 3. Remove links to other entities and from other entities

With Doctrine you can get entities via the relationship they have with other entities. This often results in entities being widely used from the doctrine entity instead of coming from a repository. So even if you have wrapped all of your calls to doctrine to get the entity, you’ll probably still have to deal with the entity coming from Doctrine via other entities.

What I did was, I searched for references of the Entity I was migrating in other entities. Once I found those I looked for all the calls to the get method and then changed those to calls to the repository. Once the repository was being used to return get the entity I then removed the reference to the Doctrine entity and left that field as just an id.

```php
// Example usage

public function getNumberOfViewsForAuthor(Author $author) {
  $blogPosts = $author->getBlogPosts();
  $views = 0;
  foreach ($blogPosts as $blogPost) {
    $views += $blogPost->getViews();
  }

  return $views;
}

// Repository

public function getBlogPostsForAuthor(Author $author) : array {
  $qb = $this->doctrineRepository->createQueryBuilder("bp")
    ->where("bp.author_id = :authorId")
    ->setParameters(['authorId' = > $author->getId()]);
  return $qb->getQuery()->getResult();
}

// Refactored usages
public function getNumberOfViewsForAuthor(Author $author) {
  $blogPosts = $this->blogPostRepository->getBlogPostsForAuthor($author);
  return $views;
}
To start off with you could just have

public function getBlogPostsForAuthor(Author $author) : array {
  return $author->getBlogPosts();
}
```

And when you’ve refactored all calls to Author::getBlogPosts() to come from the repository. You can remove the relation from Author and refactor the repository to use the code in the first snippet. This would allow faster and smoother refactoring if you have lots of calls to Author::getBlogPosts().

You also need to remove any associations from the Entity you’re migrating since in the future there won’t be Doctrine to magically populate it. If the entity is directly related and should be migrated to the microservice too then it’s ok to leave it. For example, if BlogPost had a 1 to 1 relation to BlogPostUrl entity that just contained the URLs to the blog post then that data should be migrated to the Microservice.

If you have lots of calls to an associated entity then you can always populate the entity from Doctrine in your hydrator until you’re able to refactor that association away.

### Step 4. Microservice implementation

Once you’ve isolated all the fetching of the entity to the repository and removed the unneeded entity associations, you can start implementing your microservice fetching code.

```php
class BlogPostHydrator {
  public function __construct(AuthorRepository $AuthorRepository) {
    // ..
  }

  public function hydrateBlogPost(array $result) : BlogPost {
    $blogPost = new BlogPost();
    $blogPost->setId($result['id']);

    $this->hydrateAuthor($blogPost, $result);

    return $blogPost;
  }

  private function hydrateAuthor(BlogPost $blogPost, array $result) : Author {
    $author = $this->authorRepository->findById($result['author_id']);
    $blogPost->setAuthor($author;
  }
}

class MicroserviceBlogPostRepository implements BlogPostRepository {
  public function getById($id): BlogPost {
    $data = $this->client->makeRequestForId($id);
    return $this->hydrator->hydrateBlogPost($data);
  }
}
```

### Some other things

What I did when I migrated was to have a bridge class and feature flags. This allowed me to have production use the microservice for a section at a time and monitor errors. As well as, allowing for quick rollbacks if there was an error. With a feature flag, you can enable or disable without deploying so instead of having to trigger a deployment and wait for the deployment to finish to enable or disable you can just change your feature flag and it’s switched over.