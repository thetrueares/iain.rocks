---
layout: post
title: "What is serverless and should you be using it"
date: "2021-09-05"
slug: what-is-serverless-and-should-you-be-using-it
authors: [iain]
categories: [serverless, 'Non-Technical Founder']
---
Serverless seems to be one of the greatest trends in the current tech ecosystem. Many people are building their entire applications on it and using it frequently to scale and save money – but what is it really? is it worth the hype? and should you be using it too? These are the questions that we’re going to tackle today.

## What is Serverless?

Let’s answer the first question because, well let’s be honest, we can’t answer the other questions if we don’t even know what Serverless is. Serverless, Lambdas, cloud functions, or whatever some other company has chosen to call their service, is when you give your code to a cloud provider and they handle the rest. Simple, right? Serverless then automatically scales to handle the requests that you receive and you only have to pay for the run time of your code.

### Just the code

So there’s three major things: the code, the scaling, and the payment; but let’s start on the code.

With Serverless, you supply your chosen cloud provider (AWS, Google, Microsoft, etc…) with your code and they manage the servers. The code has to be written in a programming language that they support and in a style that they’ve chosen. It then has to be packaged in a specific way and given to them. It’s similar to using a framework.

All other server-esque aspects are gone. Hence the serverless part, get it? That means that you don’t need to worry about the operating system, web servers, etc – you just worry about the code.

### Automatic scaling

With all the server stuff gone, your code can run on any server that is available. AWS, Google, and Microsoft all have a significant number of servers running, so if you suddenly get thousands of requests, they’ll run your code on enough servers to properly handle your traffic.

### Pay-as-you-run

This is exactly what it says it is: you only pay when your code is run. If no one visits your website, your hosting cost will be zero. With Serverless, you no longer have to pay for servers which run all night, just to cover you in case one insomniac decides that they want to use your service…at 3am. This is what lots of us thought they meant when they said this about cloud computing in the first place years ago, but this is the real deal.

### Rundown

Here is a quick rundown of what we just covered:

* You provide the code, Serverless does the rest.
* Automatic scaling covers your traffic.
* You only pay when your code is run.
* Server stuff is all taken care of for you.

## What is the catch?

So far, Severless sounds awesome – you don’t need to worry about servers, it automatically handles scale, and you only pay when your code is being executed. This all sounds a bit too good to be true, right? Well, there are a few things that you need to know.

### Sluggish servers
When your serverless application is not being used it, well, isn’t being used. This means that it isn’t ready to go straight away as it needs to be set up before it can do anything. For instance, think of it like someone who is waiting for their workload to arrive. While there is nothing to do, they’re asleep. When something arrives, they wake up but need a few moments to adjust and get up to speed. Once they’re awake, they’re working at full speed; but, for a few minutes at the start they’re a bit sluggish.

The same is true for serverless applications. This is known as the cold start. During the cold start, the response time is longer and, depending on the programming language used, can be really slow. This can make it unusable for rarely-used applications in certain programming languages where performance matters.

### It isn’t a magic bullet for scale

As previously mentioned, serverless applications scale exceptionally well. At this point you might be thinking: well if that’s the case, why don’t we just build everything on Serverless, then we don’t need to worry about scaling and we’ll never fail, right? Wrong. Serverless can scale well, but that doesn’t mean that your application will be able to scale. Confused? I bet.

If your application depends on something like a database which can’t scale to the same levels as your serverless application, then it will fail. A serverless application can only scale up to the limit of the things that it has available. If your database can only handle 100 requests per second, your serverless application can only handle 100 requests per second. Any request above that threshold and your serverless application will run but return an error. At that point, you’re paying a lot of money just to watch it fail.

### You have to work within their code

Another downside is that you’re stuck using the cloud provider that you’ve built on top of. You can’t pick up your serverless application from AWS and then go over to Google Cloud without using a framework layer in between. If you did want to do that, more often than not, you’ll have to rewrite your serverless application in order to switch cloud providers.

You’re also limited in your programming language. If your cloud provider doesn’t support your programming language, you’re out of luck and will need to choose another language.

### Costs a pretty penny

Serverless is one of the most expensive ways to run an application, as your cloud provider charges a hefty fee to manage the rest of the tasks for you. While it’s cheaper at lower levels, constant use of a high traffic application will be more expensive with Serverless, than if you have the proper amount of servers ready to power your application.

### Rundown

Here is a little rundown of the downsides of Serverless:

Sluggish to start with.

* Can’t automatically scale with unlimited potential.
* Vendor lock-in to the cloud provider.
* Limited to certain programming languages.
* More expensive for high traffic applications.

## Should you use Serverless?

So the big question is: should you use it? When used correctly, it’ll solve scaling problems, help cut costs, and make life easier. When used incorrectly, it’ll cause cascading failures, increase costs, and make life very painful. So let’s dive in to see if Serverless is for you.

### When to use Serverless

#### Infrequently used applications

If you have something that a user only does once a month or an application that is barely used, having a dedicated server 24/7 makes no sense. In this case, a serverless setup will help you cut costs. 

#### Scheduled jobs 

If you have a task that needs to be run at a scheduled time separately to everything else, then Serverless would be a good choice. This works well for reminder emails as it doesn’t matter if it takes 20s or 20 minutes, Serverless will only run during that time. This will save you from having to pay for a server which covers you for a day, only for you to use it for 20 minutes.

#### Event-based applications

Lastly, a serverless setup is great for when you have an independent event. With this setup, a single event can be run alone in response to a user’s action. A good example of this is with subscriber emails. If you need to send an email to someone after they have signed up, even if it’s 1s later or 60s later, it would make sense to have a serverless setup that will handle that for you.

#### When not to use Serverless

So if Serverless was designed for event-based, scheduled, infrequently-used applications, then using it for unscheduled, non-event based, frequently-used applications would not be a good idea. It’s just not designed for it. So the smart money is on sourcing a proper amount of servers.

If you have an API which receives calls 100s of times per second all day every day, then Serverless will be a waste of your money.

#### Rundown

Here is a rundown to help you decide whether you should or shouldn’t use Serverless:

Should:

* Application is not used often.
* Scheduled job that runs at set times.
* Event needs to occur in response to an action.

Should not:

* For high traffic applications.
* For things that run non-stop.
* For things that depend on something else being available.
