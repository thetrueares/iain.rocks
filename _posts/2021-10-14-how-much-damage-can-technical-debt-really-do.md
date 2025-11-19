---
layout: post
title: "How much damage can technical debt really do?"
slug: how-much-damage-can-technical-debt-really-do
date: "2021-10-14"
authors: [iain]
categories: ['Development Process']
---
So, you’ve heard of this mythical thing _- technical debt._ Has IT told you that technical debt is the reason for all your major problems? Have they tried to convince you that it’s real and that you need to deal with it? Maybe you’ve read articles and are wondering: is technical debt really as bad as everyone says it is? If you want answers - you’ve come to the right place. In this blog post, we’re going to give you a few stories of what technical debt causes in the real world, not just stories about longer hours or more bugs; but estimates of company loss due to technical debt.

<!--truncate-->
## What is Technical Debt?

In case you don’t know what technical debt is, I will explain it here or else this entire post will be useless to you. Technical debt is used to describe a technical issue that you may have. That includes the following:

*   We built something quickly, there are flaws, but we will fix them later.
*   We did something which we thought was a good idea, but it wasn’t.
*   We built something that was designed to our old spec, but now we have larger requirements.
*   We don’t have a standardised process for development, so the code is like a patchwork quilt.

So if your website is slow, you've spent lots of money on servers, or if every time you need to make a change you have to do 10 hours worth of testing to prevent the whole system breaking - your IT team will tell you it’s because of _technical debt. _

Technical debt is often likened to monetary debt, in that, if you pay off technical debt quickly, the amount of work (aka cost in monetary terms) is low. If you don’t, then you will accumulate more work, and it’ll take longer to fix (just like interest on a monetary loan).

## Revenue loss

Losing revenue because of technical debt is more common than you would think. Often, this loss occurs because of downtime. To show you how repeated and major downtime can cause significant revenue loss, here is a story about how a company lost 33% of their yearly revenue, equivalent to 3 million pounds, all because of downtime.

The aforementioned company was a price comparison site for holidays. As holidays tend to be a seasonal affair, there are times when the amount of people booking a holiday is a lot higher. These peaks are typically just after New Year's Eve and during the summer. As the summer peak tends to be massive and longer than other one-off peaks, this company found that it had technical issues every year during the summer peak. Normally, the issues would last a day or so, but this time it was different.

Over that summer peak, their site crashed every night during peak usage times (19:00-21:00), with the outage being even longer on Sundays, spanning the entire evening. Every day the technical team would spend time figuring out what the issue was and fixing it. The problem was that there were so many contributing factors, as they fixed one problem, they discovered that there was another issue causing it.

The downtime did decrease over several weeks, but overall the technical team had to solve 7 major issues to fix the outages. When the peak season was over, the revenue charts showed that this technical debt had resulted in a loss of 3 million pounds, which was one-third of the company’s yearly revenue.

## Breached SLAs

Service Level Agreements (SLAs) are extremely common and any business worth its salt is going to need SLAs to ensure everything runs smoothly; however, SLAs are another way for technical debt to hit your bottom line. In this story we'll show you how a company experienced significant financial loss via SLAs.

This time we were in a B2B environment with a company who was contracted to provide data for a large-scale enterprise which services the end-users. This company provided Points of Interest (POI) data, and the issues started cropping up when they built a new POI system. Before this system was even rolled out, the technical team noticed performance issues. They had meetings and decided that they needed to make major changes in order to handle the future traffic requirements.

Due to various reasons, the changes never came to fruition. Then as they encountered more traffic, the system, as predicted, failed to handle the traffic. Not just in a small way either - it took down everything within the company. So, they went back into meetings to discuss the fundamental performance issues, decided that changes needed to be made, but, again, didn't end up making any changes.

Not long after this, the large-scale enterprise customer wanted to go live with their system and start sending traffic to it. The system failed stress tests, they fixed the issues, it passed the stress tests, and they went live. As you've probably guessed, it then failed in the live environment. The deadline for delivery came and went, with the large-scale company receiving no answers as to why these issues had occurred.

After months of ignoring these known issues, the company was unable to deliver the live system to one of their most important large-scale clients. As they missed the delivery date, they were charged with a penalty fee as per the SLA. This cost them 1.5 million euros.

## Increased operating costs

Oftentimes, technical debt costs aren’t as clear as revenue loss or penalty fees. Actually some of the major costs are hidden inside the organisation, mainly through increased operating costs. Companies are typically expensive to run, but they cost even more to run if the tech isn’t being automated to its full potential, or worse - the tech actually causes the company more work.

This time, the story is about how a company’s manual processes resulted in vast operating costs. This company was partnered with several hundred companies, all of whom it accepted and handled data for. This data was entered into the system via a manual process which used a lot of resources. The company hired three full-time employees to input this data, and eventually realised that this manual process was inefficient. As a result, they then built a system to reduce the workload, so that a single employee could do this job for a few hours each week. Overall, this cost them three full-time employees' salaries and then further costs for building the new system.

In addition to these system costs, you can also find technical debt in the server costs. One of the most common technical debt-related projects is reducing the costs of AWS. Hosting costs can spike and then it can take months to bring the costs down to a reasonable number.

## Rewrites

Sometimes you dig yourself into a hole so deep that the only way to get out is to start again. Although rewrites seem like a good option and they’re rather popular - they have a terrible reputation. They are long, have a high failure rate, and you typically end up with fewer features in your rewrite than you had in your original. Plus, while you’re doing your rewrite, your competitors are busy improving their product. Don’t forget that it took you years to build this system in the first place, so it’s not going to be a small project to just, completely redo everything.

Does a rewrite really cost that much though? Well, here’s another story. This story is of a company that decided to focus entirely on its rewrite. The company was rewriting a system that took 7 years to develop. The company had 25 developers working on the rewrite for 18 months, at a cost of approximately 2.6 million euros. On top of that, the project management costs were approx. 700,000 euros. During those 18 months, they neglected their live system and damaged their relations with major customers, as they were unable to deliver any new requests. They only had a skeleton crew on their live system as they struggled to find people able to work on it, and their operational staff, such as accounts' managers, all left.

When they finally delivered their rewrite, it was a shell of what they originally agreed and they rushed the roll out, which meant that it barely met the requirements. In addition, multiple parts had to be redone as the quality and scalability of the new version was dubious. For this company, the rewrite didn't just result in significant financial loss, they also lost relations, employees, and essentially - their original business.

## Conclusion

I won’t bore you by telling you how to manage your technical debt, as there are many technical services out there willing to tell you; but, hopefully you now have a better understanding of the importance of managing your technical debt. You can speak to your IT team confidently with the knowledge that technical debt isn’t mythical, and when they say that you need to deal with it - you can.