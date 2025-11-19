---
layout: post
slug: code-review-how-to-make-enemies
title: "Code Review: How to make enemies"
authors: [iain]
categories: ['Satire', 'Code Review']
date: "2022-06-09"
---
Sometimes people at work annoy you, and you feel like you need to get your own back. Make them pay for the imaginary slights they've committed against you. Often there isn't really a way. But if you work in software development. Then there is always a way; that way is code review! When done correctly, code review can be an excellent tool to help improve code quality and spread core knowledge throughout a team. But when done incorrectly, it can be the bain of someone's life. It is a fantastic place to get your own back via passive-aggressive actions. Are they too good? Do they never refill the coffee pot? Did they not say good morning to you one time 3-years ago when they didn't realise you were in the office? Now is the time to take it out on them during code review!

<!--truncate-->
# Step 1: Code Style comments

The first step in this passive-aggressive war on your unsuspecting co-workers is the code style comments. Most companies have code style guidelines. Learn them! And then start asking for changes that are not explicitly mentioned. If the code style guidelines haven't mentioned something, then this is a perfect chance to ask for pointless changes that will just cause your target more work.

Did they correctly type-hint the methods in the unit test class? NO?! Better tell them to add `void` to make it clear to everyone in the future that unit tests don't return anything!

Did they name a variable in too verbose of a manner? Yes? Better them to make it less verbose.

No mention of a Yoda conditional? Demand they change it to the opposite of what they want to use.

Use coding style to grind your co-worker into the ground!

# Step 2: Ask for changes that make no difference

Step 1 is annoying, but alone, it won't drive hate into your enemy's heart. You need to continue on your drive. And next up are pointless change requests.

If there are two ways of doing something, demand they change their code to do it your way. Don't listen to reasons such as downsides to your way or upsides to their way. You need to engage in a 20 comment long thread about why this should be changed.

If in doubt about what to say, you can gaslight them into thinking they're being unreasonable with something like:

> I don't know why you're being so difficult about this request. Doing it this way will also work. Please change. Thanks

Make your co-workers spend a lot of their day rewriting code that works perfectly well.

# Step 3: Long delays

Take your time when responding. Take at least 24-hours, maybe 48 hours, to do anything regarding code review. Claim to be busy with other things when challenged.

The goal here is to make their PRs stale. Open pull requests are considered technical debt because they take work to maintain. This is annoying, tedious work. So you want to make that pull request last as long as possible, so they have to spend time just fixing merge conflicts.

One good way of doing this is refusing to deal with a PR that has merge conflicts because the code may look different after the conflicts, and you don't want to waste time reviewing it to then have to review it again after the conflicts are solved. This is a great delaying tactic.

If they've not had to fix merge conflicts 2-3 times per pull request, you're responding too quickly!

# Step 4: Demand they add bugs

Asking for changes is an excellent way of adding work, but demanding changes that cause negative side effects is a fantastic way to add work. They need to work to add the change and then they look silly when the bug is discovered and then they need to fix that bug.

# Step 5: Make code style changes in code review requests

Every pull request you make that you get your enemy to review should include 50% unasked for, unneeded code style changes. Make it so hard to find the actual functional change in the pull request that people just blindly accept your pull requests.

# Step 6: Create mega-sized pull requests

Code review is easy when there are 10-30 lines of code. But easy isn't what you're looking for here. You want to make people dread when they get a code review request from you. This means all pull requests must be 1000 lines of changes across a minimum of 10 files.

Demand quick action on these pull requests too. They're technical debt, and you don't want to be fixing merge conflicts yourself. So harass everyone until your pull request is merged. Don't accept any back chat about how you're slow with responding to other people's pull requests. Let them know that your pull requests are more important and state over and over again the technical debt being occurred while this pull request is open.

# Step 7: Ignore their comments

So you've been hammering this during code review. They may want to try and get back at you. An excellent way to avoid any blowback during code review is to just ignore them. Do they comment asking for a change? Go get your buddy to approve the pull request and merge it without dealing with that comment.

Don't like people get in your way with valid feedback. Let it roll off your pull request like water off a duck's back.

# Conclusion

When these steps are done repeatedly and consistently for a period of months, your enemy will regret the imaginary slight they committed against you.

Things you should not do if you want your enemy to enjoy code:

Automate your code style so it's automatically handled.
Only ask for changes when they provide a benefit over the existing version
Respond quickly to pull requests and schedule time daily to just code review
When asking for changes, ensure those changes also get tests
Have separate pull requests for when you're applying new code style rules.
Create small and frequent pull requests for code review.
Respond to all feedback, either agreeing or stating why you disagree.

Anyways, while you're here. Check out [RepoHealth](https://repohealth.io) a micro-SaaS built on the [SaaS Boilerplate - Parthenon](https://getparthenon.com).
