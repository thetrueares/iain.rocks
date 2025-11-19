---
layout: post
title: "Musings About Code Review"
date: "2022-06-24"
authors: [iain]
categories: ['Code Review']
---
Code review is the process of having others review code that is written and accepting feedback and adapting the code to the feedback given. These days code review is seemingly at every IT department and widely ruled agreed upon as a best practice. It is often one of the largest sources of conflicts within a development team since giving and receiving criticism about work is often hard to do while remaining detached from the work itself. After several years of code review in several teams, I've noticed somethings that work and something that don't, as well as, things that are often touted about code review which I don't think are quite true by default. Here I'll try and share what I currently think about code review.

<!--truncate-->
# Code Review will reduce bugs

I consider the idea that code review will reduce your bugs to be largely a myth. While I fully believe if done correctly and with the correct level of attention it does and I've found bugs and had my bugs discovered at code review. I don't believe that code review will reduce bugs simply by being put in place.

## Reason 1.

Code review can add bugs. This seems extremely counterintuitive since people are normally trying to find bugs during code review. And who goes around actively going around suggesting things they know will break? So, how can bugs end up being added because of code review?

One way is blindly accepting change requests assuming the developer who asked for the change actually thought it all the way through. This is most commonly done on change requests that are at face value seemingly innocuous. For example asking for some data building code to be moved to a seemingly related builder function, which then results in the data being build in an incorrect way. The change request seems simple since both are part of building the same data structure and it's copying and pasting the code. But it turns out they're building different parts of the same data structure.

Another way is the change request is one that is considered a best practice and being applied blindly without any real understanding of the best practice. For example,  in PHP they added type hints and the benefits of strongly typed languages are well known. People then go around requesting type hints being added on legacy code. This results in a bug because the legacy code doesn't always return that type.

## Reason 2.

Just because there is a bug doesn't mean anyone is going to find it. Discovering bugs often requires a lot of work on the part of the reviewer and often reviewers don't spend that much time reviewing. Sometimes developers just scan the code looking for anything that is screaming out that is wrong. Sometimes they only look at the modified code and not how that code is used or the code that it's using.

Skimping on code review is often the result of various things ranging from developers disliking reviewing code review, not having enough time, or merely not knowing the system well enough.

Code review is a skill in itself, not everyone is good at it and not everyone who is good at it invests the time in it that they need to invest to get the best results.

# Code style reviews

What I've noticed is, there are some people who will focus on code style. Their change request will be asking you to change the syntax from one to another. Everything remains the same, the logic is the same, the bugs are the same, the complexity is the same, just some single-quotes are used instead of double-quotes.

What is worse is sometimes people will ask for code style changes that aren't even in the agreed-upon code style rules. So you can end up having to have a different code style requirement to get each code review done based upon who did the code review.

Side note: What I find funny is people who normally code style review normally spend a large amount of time helping on code style tools so should know how to automate this process.

# Change Requests have to be for a reason

Another annoying thing that I've noticed is that some developers simply want to use code review to ask people to code how they want to code. For example, asking for variables or classes to be renamed, not because the original name was unclear or ambiguous but because they have a different name in their head.

If you're asking for a change request in someone's code there should either be a benefit from your suggested solution or a negative effect from their current solution. For example, if someone has breached SRP, asking for the responsibilities to be split up has a benefit of isolating the responsibilities and improve the ease of unit testing, so in my opinion that is a valid change request. But if you want some variable to be renamed in test code, then I feel there should be a reason why the current name is bad and not just that they would like a different name.

# Hit and run code reviews

A hit and run code review is when someone from another team who is unrelated to your code reviews it. I've seen hit and run code reviews complained about in a few places and I always get the feeling that the people on the receiving side of these don't really understand what is happening.  

Sometimes developers hate these code reviews because they're coming from developers outside their own team and people who aren't directly affected by the code review. However, why would it be bad to get more people to review your code?

If this happens once or twice it's just a roaming developer code reviewing various bits of code trying to keep up to date on everything that is happening. If there is one code review that has multiple people from other teams and especially if it's multiple other teams, it means people are literally talking about how bad that code is. Especially, if this happens to a lot of your code reviews. If this is happening a lot, this is probably a smell of a deeper issue.

## Neverending conflicts

It can occur that the reviewer requests a change however the developer who wrote the code disagrees with the change. Both sides think their solution is better than the other solution. These sort of conflicts are generally the ones that make code review painful to do. It ends up with countless messages back and forth with no real progress and a large amount of time spent on just arguing over a change request. Generally, these are where emotions get high and tensions arise.

If it's 1 v 1 then it really needs someone to help decide which is the approach that is best for the team. If it's more vs 1 then as hard as it can be at times to do, the solution with the most votes should be done.

## Takeaways

* Blindly accepting change requests isn't something that should be done and should be considered a bad practice.
* Accepting change requests because the other person just says "best practice" or "the books say so" is commonly just cargo cult.
* Try to look for bugs yourself and don't just rely on others doing code review finding them.
* When reviewing try to look at the depending code and the code that is dependant upon.
* Automate your code style enforcement
* Have reasons for your change requests
* Request reasons for change requests that you're unsure of.
* Get a third party to rule on disagreements that are dragging on.
* Implement the most voted upon solutions
