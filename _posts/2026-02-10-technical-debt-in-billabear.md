---
layout: post
title: "Design Decision: Technical Debt in BillaBear"
date: "2026-02-10 12:50:40 +0200"
categories: ["Code Review", "Design Decision", "Software Design"]
author: Iain Cambridge
---
Like any startup code there has to be decisions made about where you’re going to spend time working and what you’re going to leave for latter when you have the time and money to resolve the issues you choose to ignore. Here I’ll list what the current problems are to prepare for when I’m going to start resolving the issues.

<!-- more -->

# Out of Date Practices

There are some things I did because I did them previously and I just needed something quickly. Also, for somethings I was supporting an old version of PHP.

## Data Transfer Objects

One of the issues within the codebase that I’m actively working on improving and dealing with but will take some time is changing over the classes from the old standard method of defining properties within the body of the class to moving over to constructor promotion and readonly classes. This was originally done because it was super easy to copy stuff over from other classes and modify. It was also what I was used to since at the time 7.x was still in wide usage in production systems that I was used to working with.

## Enums

With Enums, I was lazy and was just googling how to do things and I found some code somewhere, I’m not 100% sure where tho, and I went with that style. So I needed to remove that code and then I realised that I put them in a single namespace to keep them together, this didn’t really fit in with the DDD architecture (not hexangonal architecture). This meant I felt like I should and kinda had to my opinion move them to be within the correct namespace to keep the correct architecture for the codebase.

# Refactored but not completed

There are somethings I did like creating my old background processing system before Symfony had the Symfony Scheduler.

There are things I did because I wanted something to do it but I wasn’t 100% sure on how to do it and later I’ve found a better way or a feature has been added to Symfony.

## Serialization

One of the features that got added and basically improved was the ability to define what DTOs are to be used and to do the serialisation before it gets to the controller. I’m not really 100% sure I want to use this new approach because I’m a bit worried I’ll lose control of the error handling. Which is a minor issue, but I really want to have diagnostic logging in my error handling, and for that error logging to allow me to pinpoint which controller and method was being used. Which I can find out via other logging methods, but I’m lazy, and it’s easier to write logging code once and then look for the log messages than continuously look through all the logs and figure out what the request was actually for.

## DataMappers

I was never really a fan of the name; it felt like they should be called factories. While the overall way the datamappers are built is good, Symfony has actually added ObjectMappers. So now I want to refactor to use them because everyone will want to use the framework's provided functionality. The benefit of this is it basically removes the need for a separate class, as we’re now able to just add attributes to the DTOs and say what we want them mapped to.

Things I don’t really like and are improvable

Here are some of the things I don’t really like and will be improving in the future because I think they’re kinda eww.

## Elasticsearch

I added some elasticsearch code but ended up not using it, but the way I was using it wasn’t that good since I didn’t wrap the client properly. However, it turns out that I don’t think that Elasticsearch is actually what I want or need to be using. Since it’s a full text search powered by lucene and I’m doing UUID searches, it makes more sense to use a database that handles uuids and indexes on those correctly in a performant manner. It’s extremely likely I’ll encounter a problem that elasticseach solves well and will use that then, but for now it’s overkill and not the best match. The exact use case just now is to be able to fetch the audit logs for users, subscriptions, and admin users, which is just searching for that id and then adding pagination.

## Namespaces

One of the things I did that I didn’t like and still needs to be refactored, something I like more, was the namespaces that are currently.

An example of one of the namespaces I don’t like is I called the customer portal public which doesn’t really make much sense. So it’ll get renamed to portal. I’m just waiting until I’ve cleaned up other, more important, and much larger messes.

## Unit Test

One of the few things people criticise BillaBear is the lack of unit testing. While they do have a point, in that there are very few (they often claim none), I made the decision to focus on functional since I wanted to have BDD feature files. There are some unit tests but not as many compared to the functional behat tests, so few that many people wrongly assert that there are no unit tests.

This is something that will be improved over time. Especially since AI is pretty good at writing unit tests for pre-existing code and will only get better, for those curious about AI and want to test it out, that is definetly the first place to look and play to see the quality it can do and how to improve your guidelines to have it produce high-quality tests first time round.

## Frontend

The frontend code is an absolute mess. I’m a hardcore backend developer so learning frontend wasn’t high on my todo list. I got a basic setup working and had the UI looking ok and usable. Over time I gradulally got better at frontend code and started to add better frontend code that followed the best practices more. Things such as composing UI elements and using stores correctly to allow for the change of state between components.

There is a lot of work, and honestly, I’m thinking of hiring a project recovery team to fix and improve the code since it’s a lot of work and I want to focus on the backend and improve that.