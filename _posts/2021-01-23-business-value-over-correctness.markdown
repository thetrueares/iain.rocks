---
layout: post
date: 2021-01-23
title: Business value over correctness
categories: [PHP]
authors: [iain]
---
So last night I managed to get myself into a twitter fight that I think brings up an important aspect of software development and highlights two different mindsets within the software development world. So here I will try to explain my position and theirs in a better format than 280 characters and while it’s not 3am.

# Quick Breakdown of the Fight

The Twitter fight was over the idea that there are some bugs found by QA in code that has been in production for years and has never happened to another person ever and these bugs aren’t worth fixing. Their position was it should be deeply investigated to understand it and to fix it to avoid affecting other users and mines is it brings the company no value to have a developer spend a day fixing a bug that has literally never affected anyone other than QA who was purposefully breaking it.

I think it’s important to remember, I described the QA report I hate as specifically being a bug that affects no one. The other person straight away brings up that the wrongness will be affecting other users in other places. I ignored the whole implied fact that they seem unable to modulate their code and pointed out it wouldn’t have because then we would have had error reports. They say users don’t always report errors, I point out we use tooling to get error reports from the software without user interaction. This confused them to no end. And from here on it basically boils down to them thinking the correctness and understanding is super important and I’m clearly incompetent for not thinking fixing bugs that affect no one or hardly anyone is super important.

# Mindset #1 - Correctness

I understand this mindset because as a junior developer, I had the same mindset. It’s the mindset that got me into TDD; it’s the mindset that invented TDD.

The core of this mindset is that it’s important that your code works and the overall mind it embarrassing if there are bugs (or at least I did). And to get the core of writing code that doesn’t have a bunch of bugs is to understand everything and the code and how it works and how it got to where it got to. And when you find a bug it’s a chance to improve yourself and how you write code in the future because clearly, something happened you didn’t expect to happen.

Overall, this mindset isn’t wrong or invalid. At the core of it is wanting to do a good job, which is a good thing.

# Mindset #2 - Business Value

This is my current mindset. I got this mindset after getting into Behaviour Driven Development, which is all about delivering business value and having the IT teamwork on things that are important to the business and will help the business in the best way.

At the core of BDD is that IT is a service department that is there to provide value to the rest of the business. This leads to things such as it’s better to write a feature that will help 10 people than to fix a bug that affects 3 people. Or it’s better to fix a bug that is costing 1,000 EUR a day than it is to write a feature that will help 1,000 people but generates 100 EUR a day revenue. To me the core of this mindset is to help the business the best way possible and that the people best to decide how that is are users and other people within the business.

# Is bug-free code important?

In some cases bug-free code is super important. These are mission-critical applications, and correctness is super important and any bug must be fixed. However, these applications are a tiny percentage of what is developed.

In lots of businesses, if you talk to the other departments they will openly admit they don’t need the code to be 100% bug-free, they just need it to work 99% of the time and for the essential things. As it turns out, lots of people don’t care if the application is bugfree, in fact, many users will figure workarounds for bugs, and once they’ve figured a workaround, they don’t care that bug exists because they’re still able to do what they want to do. Because people care that they are able to achieve whatever action they are trying to do, and the value of the app is still delivered.

# Business Stages

I think it’s important to note that there are stages in a business lifecycle where you will want one mindset over the other, and sometimes you’ll want both.

## Start Up Stage

During the start-up stage of a company, you will 100% want to have the Business Value mindset. There are phrases such as “Move fast and break things” and “If you’re not breaking things you’re not 0moving fast enough”. Which are, in my opinion, about the fact that in a start-up you need to care more about your traction and growth than you do over complete correctness of your software and that if you break something, it’s not something to beat yourself up over.

An example, say you have 4 features that if done with 100% correctness will generate 1,000 EUR a day and will take 2 weeks to implement with 100% correctness. However, if you do 90% correctness, it will generate 750 EUR a day and will take 1 week to implement. So you have a choice, spend 2 weeks and have 100% correctness and 1,000 EUR a day or have two features with 90% correctness and 1,500 EUR a day. To me, it seems clear 90% correctness and 1,500 EUR a day is the option required at this stage.

## Growth

During this phase is where the company decides it needs to improve it’s correctness, years of start-up stage has resulted in an application with lots of bugs and they are now spending too much time dealing with all the bugs and bug reports. This is where you still want to have some business value over correctness, but you will want some correctness over business value people.

Why both? Because you’ll still want to focus on important things and shipping features to grow, rarely will a company grow just from fixing bugs and not improving their product feature-wise. But you want to reduce the number of bugs being added as well as have people who are able to understand the system and how these bugs were introduced and how to avoid these bugs in the future.

At this stage, you still can’t really afford to spend 2 weeks to have 100% correctness but a week and a half for 95% correctness is now the best approach.

## Scale

Scale is where you want to have correctness over everything and you can spend 2 weeks for 100% correctness. At this point, the company should have so many users that any random bug will affect lots of people even in the edge cases. At this point, the company wants to present a polished product that is best of class. They will want to reduce costs in other departments caused by these bugs so they will want correctness.

# If we have nothing else to do bugs

So since my original point was that there are some bugs that aren’t important. I think it’s important to point out, my mindset is not that these bugs should never be fixed or that I can’t be bothered to fix them. Especially, since the main reason these bug reports of bugs that affect no one, annoy me is that I actually fix them even though I think it’s not a good use of resources.

If a bug exists, I have no core issue with it being fixed. But what I’ve found is the majority of the time we have more important things to do than to fix a minor bug that affects one user and the user has a workaround. For me this is a bug that should only be fixed when there is nothing else to do. Which does happen from time to time.

# Someone will have to come along later and fix that mess

One of the points made during this twitter fight was that the other person made the point of saying they were about to start work on a six-figure project to fix the issues caused by this mindset. Which is completely true, I am often part of the workforce that joins during the growth stage of a company and spend lots of my time fixing and scaling the start-up stage code. It is 100% true that if you allow bugs to mount up and aren’t dealt with, you will need to hire consultants, agencies, etc to come in and help you repair the system. And these people often have the Correctness mindset. This is true of all technical debt because that is what this business value mindset is about creating what the business considers acceptable technical debt.

Technical debt is not a bad thing if correctly managed. Technical debt is all about saying we can get X now, but it’ll cost us Y later and Z even later if we don’t deal with it quick enough. Techincal debt while getting something for it makes complete sense and isn’t something that should be 100% avoided. It’s just something that should be managed. But technical debt provides no benefit currently, and only downsides later should be avoided.

And I think it’s important to point out, that the companies are able to afford to hire expensive agencies and consultants because the original code delivered enough business value that the company survived the start-up phase and is generating enough revenue they have the money to spend on expensive agencies and consultants. Basically, it delivered what the business needed at that time and got the business to where it wanted to be. And now a different approach is needed to get the business to where it now needs to be.

# Correctness can also be Business Value

I feel like I’ve pointed out multiple times in this post that there are times where the company wants and needs correctness. At this point, to deliver the best business value to the company, I feel that the two mindsets don’t conflict and it would be hard to tell the difference between developers with the two mindsets.

# The Correctness mindset can get you fired

I feel like a lot of the developers with the Correctness mindset seem to think that it makes them better developers than ones who have no issues with 90% correctness during the start-up or growth stage. So I would like to share an example of a developer I was working with who had the Correctness mindset.

So I was working in a team with 5 other developers. And we had one developer who was all about understanding and correctness. Which as I feel I’ve said before, is not a bad thing in itself. So whenever he got a bug he would spend time researching everything about the bug, reading lots of code, and truly understanding what was going on and then would fix it. This would result in bugs that would be fixed by other developers in 1-2 days taking weeks and sometimes requiring intervention so someone could point out the cause of the flaw instead of allowing him to carry on his understanding everything approach. I would not say this developer was less skilful than the other developers. It was just his approach was very much to understand everything and then move forward and to have complete correctness.

When Corona struck, he was the first person let go (he was not the last). Why? Because he worked slower than the others and the company was not at the scale stage they were very much at the start of the growth stage. And not only did he work slower, he literally made meetings twice as long and half as productive because he would spend ages asking edge case questions even after being told the edge cases weren’t important right now.

## 10x developers

I often see people complaining about how they have fast but sloppy developers where they work and that these developers are loved by the business even though other developers have to clean up all their bugs.

My personal experience with this kind of developer is that they produce more bugs because they produce more features. The bug to feature ratio is the same as other developers but that is just my experience, and they could be right, and they are working with devs who have a higher bug to feature ratio.

But what I do think this shows overall, is that business value is not always delivered by 100% correct code and that key to being a valued member of the company is by focusing on business value.

## Conclusion

So overall, I hope that I’ve explained why I think Business Value is an important mindset while also pointing out there is a time and place for a Correctness mindset. For example, if you’re building a self-driving car, correctness is 100% needed. If you’re building an MVP, correctness is not super important and to help the company the most it’s best to accept some bugs to help the majority. And that while I think not all bugs are important, I have no issues with fixing them, I just have issues with fixing them overdoing things users/business think is more important.