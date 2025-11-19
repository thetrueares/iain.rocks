---
layout: post
slug: how-to-review-a-your-mvp-project-as-a-non-technical-founder
date: "08-08-2021"
title: How to review your MVP project as a non-technical founder
authors: [iain]
categories: ['Non-Technical Founder']
---
As a non-technical founder, you can be worried when you're having a project built but do not know if it's good or not. We want to help non-technical founders better understand what is happening so they can make informed decisions.
<!--truncate-->
## Code

The code seems like it would be one of the hardest things to be able to correctly judge as a non-technical founder. However, due to the tooling created to help developers, this is one of the easier things to judge since you can use these tools to get a report about the quality of the code. These tools are called static code analysers, and you can find them running in the cloud, so you won't even need to install anything technical on your computer to be able to use them.

For example, you can use SonarCloud to analyse your code, and it will give you back a detailed report of what it found, such as issues and its rating for the code. While this is not a hard and fast system, it will provide you with a good overview of the quality of the code.

It should be noted that for an MVP, you do not need really good code quality. You want the code to work and be of reasonable quality. You want to avoid major issues. Medium and minor issues can wait until you've passed the MVP stage.

## Infrastructure

For nearly every sort of application these days, you will need some sort of web infrastructure. While this can seem daunting for an MVP, this is reasonably easy to judge. There are three things you want to look at – the hosting provider, the server setup, and then you also want to check to see if it can handle the number of users you are expecting/hoping to attract.

### Hosting Provider

To start off, it's probably best to use a cloud provider like Digital Ocean. It's very easy to use. Other cloud providers like AWS and Google Cloud Platform are geared more towards tech professionals using it. Digital Ocean has a very low barrier to entry and has a simple point and click. Once you gain some traction, it is reasonably easy to move off Digital Ocean whereas it's harder to move off AWS and Google Cloud Platform.

### Server Setup

With your MVP server setup, you want to be able to grow and scale. The easiest way to do this is to have a large database and then have multiple web servers talking to the database server. You will want to have your domain pointing towards a load balancer, a server that forwards requests to the web servers and makes sure each web server gets the correct share of the users. With this approach, when you get more users and need more web servers, you can just add a new web server to the load balancer and you'll be able to handle more traffic.

One important thing you'll want to get your tech professionals to do is to make it so that you can add new web servers very easily. To do this, you'll want to have them create what is called an image of one of your web servers. An image is basically a backup that is easy to use to create new servers that are the same as the server that got backed up.

### Load Testing

Load testing is when you use tools to pretend that there are lots of users using the application. This is good to know how many users your application can handle on the servers you have. It is also good so that you can see how fast it performs. If you have a slow website, your Google ranking wouldn't be good, and users won't have a good experience.

To do load testing, you can use cloud tools such as LoadForge. With this tool, you can record what you do in your browser and use that for load tests. Once you run them, you'll be able to see how much traffic you can handle and if it meets your expectations.

## Database

Your database is one of the most important parts of your system. If you can scale your database, you can scale your application. The key to being able to scale is using the correct type of database for your data and the links they have.

### Relational

A relational database is best for, well, relational data. This is data that is linked to multiple other bits of data, for example, if you have users that are linked to charging sessions that are linked to charging stations that are linked to companies. A company can have many charging stations, a charging station can have many charging sessions, and a user can have many charging sessions. Charging stations and charging sessions are linked to two different bits of data. Then you have relational data that would be best served by using a SQL database like MySQL.

### Document

A document-based database is good for data that is not linked to others, or data that is linked to it is only linked to it. For example, you have a blog that has posts, and the posts have comments. The comments are only connected to the posts and can't be linked to anything else. With a document-based database, all of this data would be stored together in what is known as a document. In your application, when things are only related to one other item and can't be linked to anything else, then you would be best served by using a database such as MongoDB.

## Testing

Testing is an important part of the software creation process. No matter how well you do it, there will still be bugs, and people will ask why you didn't test it. With an MVP, you're looking for the showstopper bugs; when these happen, the application is completely unusable.

### Automated Testing

Testing can be a very boring process, and it's quite common that when a developer changes one part of the application, it breaks another part of the application. This means you would have to test every part of the application every time there is a change. This isn't feasible. This is why it is extremely common to write automated tests called unit tests that test the code in an automated way. This allows you to test everything constantly without having to spend countless hours clicking through the same area. If you have unit tests, you will want to run those tests every time you change something. To do this, you'll want your tech professionals to use what is known as a continuous integration system.

Depending on how much you're paying, you may or may not expect the developers to create automated tests. If they are not doing these and you're doing the testing yourself, you will want to create your own automated tests using something like Ghost Inspector, which will allow you to create automated tests based on your browser. What you would want to test is your most critical paths, such as the user sign up path. These paths are the core things you want users to do on your application. If these paths don't work, then your application will be useless.

### Doing User Testing

Doing user testing seems very easy, but it is a skill in itself. This is why there are QA professionals. Most people, when they do user testing end, up just doing what is known as the happy path, which is testing if everything happens the way it's supposed to work. The thing is, most of the bugs found are from users attempting things never meant to happen. One example is typing the word "ten" in a field that is expecting a number. When you're doing user testing, you want to sit and think about what can possibly happen and then see how the application works if you try it. Here's a good example of something that can realistically happen and realistically break. You have a user sign-up form and ask the users to enter their information into the fields, but they miss a field. It is a common occurrence where validation breaks but the user form can be submitted even when it shouldn't be submittable.