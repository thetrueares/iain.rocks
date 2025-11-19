---
layout: post
title: "AI is a Junior Dev and needs a Lead"
date: "2025-08-19 06:18:40 +0200"
categories: [AI]
author: Iain Cambridge
---
Using AI to help with programming is becoming increasingly popular as time goes on, with developers across the industry embracing tools like Junie, GitHub Copilot, ChatGPT, and Claude to accelerate their workflow. We're seeing plenty of horror stories where things go spectacularly wrong - from subtle bugs that slip through code reviews to complete architectural disasters that require massive refactoring efforts. Security vulnerabilities introduced by AI-generated code have made headlines, and there are countless tales of junior developers blindly copying and pasting AI suggestions without understanding what the code actually does.

But who's really at fault here? Is it the AI tools themselves, user inexperience, or deeper integration issues within our development processes? To answer this question, I've deliberately tested AI coding assistants across various scenarios. And I think I've figured it out, it's a junior dev that just needs a lead dev
<!--truncate-->
## Starting Out

When I first started exploring AI and coding, I began asking AI systems questions about programming challenges. These systems consistently provided clear explanations and working code examples. Over time, they became a reliable first port of call for tackling problems—something I could count on to break down concepts and suggest practical solutions.

After a while, the results became increasingly reliable and genuinely impressive. GitHub Copilot developed remarkable auto-complete capabilities, effortlessly filling in boilerplate code that followed established patterns in my work. It began to understand the context of what I was building, suggesting not just syntactically correct code, but code that actually made sense within the context of that area in my project. The AI could recognise when I was writing a data mapper like the other data mappers and would see all the fields that need to be mapped and just provide it as an auto-complete.

What started as a novelty gradually transformed into a useful time-saving measure that I really like and miss when I don't have it.

## Enter Junie

I'm not the fastest adopter of new things ever, and I'm often a bit resistant to change until something has proven itself to be genuinely worthwhile rather than just another passing fad. So it took me a few months to even try out Junie, despite all the hype and constant chatter from other developers who seemed to think it was the second coming of software development tools. (You know who you are)

And honestly, at first, it was absolutely rubbish. Complete and utter garbage, if I'm being frank. I genuinely hated it with a passion. It ate up all my quota within the first few days of testing, delivered broken code that wouldn't pass the build no matter how many times I tweaked the prompts, and generally wasted my precious time that I could have spent actually writing working code myself. It took longer and produced less.

But one thing was absolutely clear, the other developers I knew were way better at using AI than me and they said they were getting genuinely good results from their interactions. These weren't just casual users either - these were experienced programmers who I respected, people whose technical judgement I trusted. They were raving about how AI was helping them solve complex problems, generate clean code, and even debug tricky issues that would normally take hours to resolve. Meanwhile, I was struggling to get anything useful out of the same tools they were using. The disconnect was obvious. So I had to figure out what the problem was - was it my prompting technique, my expectations, or something else entirely?

## It's a Junior Developer and needs a Lead Developer!

At first, I was asking it to do things like I would ask a senior developer on my team. I expected it to know certain things and just understand how to develop from start to finish. I'd throw complex requirements at it, assuming it would grasp the nuances of our codebase, understand our architectural patterns, and know exactly which libraries we preferred to use. I thought it would inherently understand our coding standards, our deployment processes, and the subtle business logic that had evolved over months of iterations. Basically, I was treating it like a seasoned colleague who had been working alongside me for years, someone who could read between the lines and fill in the gaps without needing extensive context or detailed explanations. So even though I was giving it junior-level tasks, I was treating it as a senior developer doing super-easy obvious task.

The first task I gave it was to refactor DTOs in PHP from the old legacy way of creating them to using new features such as readonly classes and constructor promotion with public properties instead of getters. For an experienced developer, that's an easy task that is just long and boring. Junie, on its first try, did about 10 out of 100 or so classes, gave up, and pretended like it was all done. The build was broken and it was so half done that even the things that it touched weren't worth dealing with. 

To be fair, everyone said it was too much, and they were absolutely right from the start. I was being far too ambitious with the scope, trying to tackle everything at once when I should have known better. The breakthrough came when I started doing it in a much smaller namespace and methodically moving through the different namespaces one by one, and suddenly it was able to do the job properly. The key was breaking everything down into manageable pieces rather than attempting some grand, sweeping implementation.

If I focused on specific small chunks of functionality - really drilling down into the individual components and tackling them separately - it could actually do it. The difference was night and day once I adopted this more granular approach. So I could now get it to do very basic things reliably, and more importantly, it was clear what was working and what wasn't. Each small success built upon the previous one, creating a solid foundation that I could actually understand and debug when things went wrong.

## Treating it like Jr Dev

I then remembered all my time being a lead developer with multiple junior developers working under me. The memories came flooding back - countless code reviews, debugging sessions that went on for hours, and those frustrating moments when I'd discover someone had pushed untested code to production. And I realised all the things I complained about, all the stupid AI blow-ups, the overly complex solutions to simple problems, the failure to consider edge cases, the tendency to reinvent the wheel instead of using established patterns, etc all had one thing in common. They're exactly the same things junior devs do because they don't know any better. They haven't yet developed the experience to recognise when they're overengineering something, or when a seemingly clever solution will create more problems down the line. Just like junior developers, AI systems lack the hard-won wisdom that comes from years of making mistakes and learning from them.

AI, if left on its own, will choose the lazy way every single time. It will take shortcuts that seem clever in the moment but create technical debt that'll haunt you for months. It will choose the risky way, implementing solutions that work in the happy path but completely fall apart the moment you encounter edge cases or unexpected user behaviour. It'll do downright stupid things that make you question how something so supposedly "intelligent" can be so utterly clueless about basic logic and common sense. Because at the end of the day, it's just a junior dev—one that's incredibly fast at writing code but lacks the wisdom, experience, and critical thinking skills that come from years of making mistakes and learning from them. It doesn't understand context, can't read between the lines, and has no intuition about what could go wrong.

So I decided I was going to do what I did to junior developers: be specific about what they are to do, break down the task into manageable steps, provide clear user stories or BDD scenarios and comprehensive guidelines. And even then, ensure that the task isn't too big or overwhelming for them to tackle in one go. And most importantly, code review them thoroughly. 

I've learnt from years of mentoring that vague instructions like "make this better" or "fix the performance issues" are absolutely useless. Junior developers need concrete, actionable guidance - they need to know exactly what success looks like. The same principle applies here. Instead of giving broad, sweeping requirements, I started crafting detailed specifications that left little room for misinterpretation. I'd outline the acceptance criteria, provide examples of expected behaviour, and even include edge cases they should consider. This approach transforms what could be a frustrating guessing game into a clear roadmap with defined milestones.

I went from staring at dodgy code whilst twiddling my thumbs to producing production-ready software—and suddenly found myself far busier. Whilst Junie worked on the tasks I'd assigned, I was either reviewing code that Junie would then address or crafting specifications for the next piece of work. It transformed my role overnight into something resembling a lead developer: I decide how the work gets done and ensure quality standards, whilst others handle the actual coding.

## What I did

### Guidelines

One of the first steps to mastering coding agents is establishing clear guidelines. Junie makes this straightforward with the `.junie/guidelines.txt` file. It even helps you get started with a prompt from the Master Junie section. From there, you simply edit and expand the guidelines, describing how each component of your system works and how to build features that integrate seamlessly with it.

The guidelines are incredibly powerful and can work seamlessly with MCPs (Model Context Protocol). The integration possibilities are genuinely impressive once you get everything configured properly. For example, I have it set up so that it automatically commits the changes to a new branch with a descriptive commit message, pushes it directly to GitHub, and then requests a review from both me and GitHub Copilot. It's quite satisfying to watch the entire workflow execute automatically - from code generation to version control to review requests - all without manual intervention.

The only minor hiccup I've encountered is that the Copilot review request fails about 50% of the time, though I suspect that's a race condition on GitHub's side.

### Scenario

Having learnt to love BDD, I use scenarios quite a lot as a way of defining a feature and how it should work. There's something incredibly powerful about the structure and clarity that BDD scenarios provide - they force you to think through the actual user journey and what really matters. I've found it's absolutely brilliant for explaining to everyone, technical or non-technical alike. Product managers get it, developers understand the requirements clearly, and even stakeholders who've never written a line of code can follow along and provide meaningful feedback.

So I create a comprehensive feature file with detailed scenarios for how this feature should work, covering not just the happy path but also edge cases and error conditions. Each scenario follows the classic Given-When-Then format, which creates a shared language that bridges the gap between business requirements and technical implementation. It's become an essential part of my workflow because it eliminates so much ambiguity and miscommunication that typically plagues software projects.

### Prompt

Then I craft the prompt explaining what we're doing in clear, precise language. If it's adding a feature, I take the time to explain what the feature is for, providing context about why it's needed and how it fits into the broader application architecture. I describe how it should work in a sentence or two, being specific about the expected behaviour and any edge cases that need to be considered. I then provide a comprehensive task breakdown, methodically listing out what things need to be done, prioritising them in logical order, and noting any dependencies between tasks. This structured approach ensures nothing gets overlooked and gives the Junie a clear roadmap to follow from start to finish.

```clike
We are adding a feature to allow users to see the subscription stats. For now we're just going to add the backend part.

Users need to see how many subscriptions they have for each month. They need to see how many are existing subscriptions that rolled over from that month, how many are new subscriptions, how many are upgrades, how many are downgrades, how many churned, and how many users came back and reactivated.

Tasks:
- Run behat features/Stats/Subscription/new_subscription_stats.feature and add all the steps
- Create a repository class that fetches all the data using SQL/DQL and not the QueryBuilder
- Add the backend app end point that returns the stats
```

So while still not totally spoonfeeding it, it's getting spoonfed a lot.

## Result

The result from this was code that was almost ready for production, which frankly surprised me given how quickly it all came together. It needed your standard code review and removal of the silly things - you know, those little shortcuts and quick fixes that always creep in when you're in the flow of getting something working. There were a few hardcoded values that needed to be made configurable, some error handling that could be more robust, and the usual suspects like inconsistent variable naming and missing documentation.

After 2-3 thorough code reviews and feedback sessions with the team, where we caught the edge cases I'd missed and polished up the logic, the code was all done and properly tested. The backend was solid, performant, and ready to handle whatever we threw at it. With that foundation firmly in place, I moved on to the frontend part, which promised to be an entirely different beast altogether.
