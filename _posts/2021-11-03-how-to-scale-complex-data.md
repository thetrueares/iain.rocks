---
layout: post
slug: how-to-scale-complex-data
title: How to Scale Complex Data
date: '2021-11-03'
authors: [iain]
categories: ['Software Design']
---
For most complex large-scale applications, one of the main issues is maintaining a high level of performance with extremely complex data. This is a problem whether you use microservices or a monolith, as the problem is data-related and not a system architecture problem. In this blog article, I'll try to explain, in simple terms, how to maintain performance with a complex data model. I'll use the real-world domain of an Electric Mobility Service Provider (EMSP) including their locations and prices to provide you with a solution for performance issues.

<!--truncate-->
## Understanding EMSP

I'll start by giving you an overview of the domain and problem of an EMSP. An EMSP allows an electric car owner/driver to charge their car using public charging stations. Most charging stations are owned by a specific company, and typically owners/drivers don't want to have a contract and account with each company. These companies are known as Charging Point Operators (CPOs) and they don't want to handle billing for users' single sessions. This is where an EMSP comes in. EMSPs provide a platform which allow drivers to find public charging stations with a list of prices for each one.

The pricing can become rather complex as there are multiple layers for an EMSP, but here are some examples of the pricing rules:

*   Users who live in Country A are given price B for chargers in Country A, but users who live in Country B are given a different price.
*   The time of day for the charging session affects the price. So a charging session at midnight may cost a different price to a charging session during the day.
*   Users who have a deal with the car manufacturer are given price A for CPO A, but all other users are given price B.

Figuring out the charging price for a user at a specific point in the day takes a lot of time to calculate as there are multiple layers affecting the price. Due to the time it takes to retrieve this data and the complexity of the data, the system may experience performance issues.

In a microservices world, you would have one service which is responsible for charging stations and then a separate service which is responsible for pricing. Whereas in a monolith world, you would store these bits of data in separate tables. In both worlds, you would have to fetch the data which, due to its complexity, would take a long time to retrieve, with the time increasing the more data you add.

## The Problem

This problem will be explained from the viewpoint of the microservices world, as microservices is a buzzword, it's cool, and the way it separates things is generally clearer which makes illustrating diagrams easier. The same logic used in the diagram can be applied to a monolith system, but the services would become databases or tables.

Using common logic of an EMSP, the steps would be: 1) fetch the data you want to display for all charging stations; 2) fetch any additional CPO information needed (such as contact information, names, branding, etc); 3) fetch the pricing information for each charging station.

![](/images/blog/scale-complex-data/scale_problem.png)

Essentially, the more complex your application, then the more complex the data will be that you need to fetch for each charging station. If you’re doing this in a single monolith-based application, it would be an expensive call that would likely underperform. If you’re doing this in a microservice-based application, the performance issues are typically more obvious as you may have multiple calls from each service.

## The Solution

My solution for solving this performance issue is to create a composite data model which is then used to search and display the information. The idea is that there would be a service which generates the search data based on an update or insert event. This would fetch the data from each service and then build the usable search data. In a monolith, this would just involve a command which would be run at a scheduled interval and would update the location search data.

So instead of searching charging stations and then retrieving the information that goes with it, all the information would be attached automatically. It rarely matters how big a single data record is and data space is reasonably cheap compared to CPU power, so it makes sense economically to copy the data to avoid CPU cycles later and to map all of the information together. Then the application can choose which of the prices to display, even if it does retrieve all of the prices available. It's faster to check which price is valid than it is to fetch all the prices dynamically and only return with the current valid price. The most expensive part of the call will be fetching the pricing data.

![](/images/blog/scale-complex-data/scale_solution.png)

One of the benefits of this model is that it allows you to build your data in a way that is optimised for searching. Before, if you were searching for a specific set of charging stations (for example, ones that had a certain price), it would be a performance nightmare. The way the data should be modelled in order for it to be searched performantly is often very different from how it should be modelled in order for it to be mapped to other items.

One of the downsides of this model is that by choosing availability and partitioning from the CAP theory, you have to give up consistency. As we make composite data and duplicate that data, there is a possibility that the data will be updated; but it'll take some time for that change to propagate and be displayed to the end user. In this specific domain it isn't a big issue. If it takes a few minutes to update a charging station’s information, it's not the end of the world. There are systems where this approach wouldn’t work as the information needs to be updated in real time and people always need to have the latest version; but for an EMSP, this system would maintain performance.

## Conclusion

This approach shows how a composite data model may help with your performance issues in some domains. I’ve seen this pattern employed with many systems, so hopefully this pattern is recognisable to some people. For others, I hope it solves any performance issues that you may encounter.