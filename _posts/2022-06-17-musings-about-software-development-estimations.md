---
layout: post
title: "Musings About Software Development Estimations"
date: "2022-06-17"
authors: [iain]
categories: ['Development Process']
---
Estimations are one of the most important parts of project planning and one of the most common tasks that developers do no matter which language they code in, what team they are on, or which company they work for. Estimating is hard, so hard we pretty much get it wrong a lot of the time.

<!--truncate-->
## Not enough details - guesstimates

Estimating without enough information is in my opinion of the leading causes of estimating poorly and causes project overruns. It's a classic case of someone asking how long it will take to do something without you really knowing anything about the task. Standard things would be how long would it take to integrate an API into your system. You have a rough idea but that idea is a rough guesstimate. The problem is when you provide an estimate others plan upon those estimates. Remember, they're normally asking for the estimates for a reason. If you have someone who is not that good at project management this will often result in your estimate becoming a deadline and you over-running on your estimates and looking bad.

To explain to non-developers I ask them how long it'll take them to build a house. Then when they give their estimate I say that house needs 26 rooms, 13 bathrooms, 3 kitchens, 6 living spaces, a pool, and a wine cellar. Then ask how long it'll take.

### Smell: Need to investigate

One of the main smells I've noticed here on the day to day issues is when we're estimating the ticket and people start talking about needing to investigate it. If people think there is a need to investigate an issue, I feel creating a task to investigate and estimate that and then when it's done you can estimate the original ticket.

### Smell: no specifications

This one is normally coming from Project/Product managers when they want to do long term planning. And as my explanation to non-developers, you would be providing an estimate on something you have no clear idea what the work will actually be.

## Story Points

When I first started doing development everything was estimated in time.  Hours, days, weeks, months. For within the development team everyone understands why you spend 2 hours doing a 1-hour task. You discovered something that was bigger than you thought. Outside of IT, it can result in why is X working 40 hours a week but only achieving 30 hours worth of work? To solve this issue Story Points came along. To remove the direct connection to time.

### Time based

While story points remove the connection to time, I feel like the biggest mistake people do when they're estimating things is they don't use the story points to relate to time.

On the team where our estimates were the most reliable we had a rule, outside of the team story points weren't time but within the team and in the planning meeting we agreed 1 story point would be 1 day.  

The teams where estimates were the worst were where they used story points and then they had a completely different estimate for time. Where people would stick to the idea that story points are just complexity and not related to the amount of effort required to estimate it. To rebuttal this, I always talk about a data mapper, the complexity of a data mapper is always very small. It's pretty much the lowest complexity you can have, unless, you're doing something really weird and that's probably a smell of a different issue.  However, the amount of time required to implement a data mapper varies widely, if you have 5 fields to map, it'll be quick. If you have 500, it'll take you a considerable amount of time. So giving it an estimate solely on how complex it is doesn't really help for planning purposes.

### Fibonacci Sequence

It seems when it comes to story points, everyone is convinced that using only Fibonacci sequence numbers is the best way to go. And honesty, I really don't understand where this idea comes from. There are only estimates that a story will be 1,2,3,4,5,8. So anything that is in between a 5 and an 8, people have to vote either way. You end up underestimating or you end up overestimating. Either way, it doesn't seem the best way to get a reliable estimate which can be planned upon.

I've pretty much never seen a team that uses Fibonacci sequence have a reliable velocity.

Again on the team where it had the best reliability for the estimates and velocity, it was literally how long people thought it would take. We had 0 story points for it'll take me 5 minutes, no point counting it, to a quarter of story point, half, etc. If something came out at 4 it got 4.

If your only options are 0, 1, 2, 3, 5 story points and the task is going to take 15 minutes, people are giving it 1 story point and then will give a task they think will take 3 hours 1 story point. Then giving tasks they think will take 2 days 2 story points. But in reality, you could have done multiple of the 15-minute story points in the time it took to do the 2 story points. So your velocity for a sprint can be super high because you had a bunch of small tasks but when you try to put in the same number of story points of the bigger tasks you don't get anywhere near that. Then you look bad and people are struggling to understand why the velocity is always changing.

## Negotations

This is something that often happens when you have someone with poor leadership skills in charge asking for estimates. As well as, somewhere that treats estimates as deadlines. What happens is someone gives and estimate the person receiving it doesn't like it and thinks it's too long/large of an estimate and then starts asking if they can do it in less time. Offering to give them a certain amount of time to do the task instead of the estimated task. Giving in and reducing your estimate or worse accepting a purposed estimate given to you will result in you either over-running or cutting corners.

### Difference between challenging and negotiating

I think it's important to note, there is a difference between challenging an estimate and asking why the person thinks it'll take that long and trying to get the estimate down.

I once had a developer give an estimate of a day to add a field to an entity. I was gobsmacked and asked them if they thought it would take them a day to add a field to an entity that was stored in MongoDB. And why they thought that. It turns out they had no real reason and team re-estimated and came back with a lower estimate.

## Changing Estimations

One thing I see a lot is people changing estimates, especially when the task is larger than they thought. This I disagree with, we don't change an estimate when we did it quicker than what we thought. Only when it's larger. So tickets that were over-estimated remain the same and are incorrect and the tickets that were under-estimated are increased and are correct.

I like the idea that when estimating we're pretty much always going to be wrong. We'll under or overestimate a task. If we're consistently wrong we can plan based upon the wrongness.  This is why I disagree with changing estimates. If you estimate it and then learn more information, you should keep the original estimate since the amount of information you had was roughly the same as the amount of information you had for other tickets that you estimated so your level of wrongness will be the same but if you update it when you get more information the level of wrongness will be lower and affect the overall level of wrongness.

## Estimating bugs

It's commonly thought that you shouldn't estimate bugs. It's either because people say you don't know how long they'll take or they will say fixing them was part of the original estimate. For me, if something requires effort to do in a sprint that doesn't already have an assigned estimate it needs one.

If fixing a bug's effort was already calculated in the ticket but the original ticket was done 3 sprints beforehand then the effort it'll take to do will have to affect the current sprint's velocity since this velocity won't include this effort. So your velocity doesn't actually represent the amount of effort to do all the tasks done within the sprint.

Not estimating bugs doesn't give the developer credit for work done. The developer did 10 tickets but only gets credit for 9 in his velocity because one was a bug.

I've also heard that not giving bugs story points is to punish the developers for creating the bug in the first place, that idea is just nuts to me. I think if you're in the mindset of punishing your employees for mistakes, you're going to have a hard time keeping them and they're going to hide their mistakes with is a lot more costly. And in a world where there are more developer jobs than developers, it seems unwise to do things that will increase your employee churn rate.

## Velocity

The velocity is the number of story points or hours worth of work achieved within a set period, normally a sprint. The goal for a development team should be to have a consistent velocity so that plans can be made and the team can be relied upon.

What I find is most teams don't know their velocity and teams that are paying attention stop mentioning it because theirs is constantly changing. If your velocity isn't consistent then I believe you'll be suffering from some of the problems I've listed and some I haven't (either forgot or don't know them). An ever-fluctuating velocity should be considered a smell for poor estimations.
