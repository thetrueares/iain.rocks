---
layout: post
slug: php-isnt-that-like-really-bad
date: 2021-07-04
title: PHP, isn't that, like really bad?'
categories: [PHP]
authors: [iain]
description: Explaining why PHP isn't as bad as many people make out. Explaining the current state of the current practices, security, and performance.
---
The aim of this article is to explain to non-technical individuals that PHP isn't as bad as many make it out to be. Try to answer some of the more common assertions about PHP. PHP has a terrible reputation because it used to be horrible.

**To skim, just scroll for the TL;DR in bold.**

<!--truncate-->
## Doesn't it encourage terrible practices?

Not anymore. In the past, many developers learning from books were taught extremely bad practices, so the quality of the PHP code was typically poor. PHP also once allowed you to do some extremely odd things, making it very easy to build but a nightmare to maintain.

These are no longer common problems. With the introduction of high-quality learning material that is easy and widely available, a new developer learns PHP the right way. This prevents many junior developers from writing code that is extremely painful to maintain because they don't know the correct way to build things.

With the introduction of frameworks, much of the generic code that caused many of the terrible practices is now done automatically; so, the developer just uses the framework, and the framework codes it correctly.

Also, over the years, some of the terrible practices were caused by missing features, resulting in things being allowed that shouldn't be allowed. Most often now, it's not even possible to implement some of the things that were previously written to cause this reputation.

### TL;DR

*   **It no longer encourages terrible practices..**
*   **Terrible practices are avoided by using a framework.**
*   **The language features now have many discussions. Bad features no longer make the cut.**
*   **PHP has added most, if not all, of the language features that are present in other languages.**

## Doesn't it have poor security?

In the past, the security of PHP applications was often poor because of things the language allowed. Those things are no longer used because PHP applications are developed completely different.

Remote and Local file inclusions, where PHP reads files from other locations than originally intended, have been removed by using autoloaders to include files instead of having dynamic file inclusions.

Cross-Site Scripting attacks where a user adds JavaScript to what is displayed to another user, which were caused by using HTML directly in PHP, are prevented by the widespread use of templating systems that automatically handle the escaping and security matters of displaying dynamic content.

SQL Injection attacks where a user could add extra SQL commands to a query, which were caused by the need to build SQL queries and send the query and data together, are prevented by prepared statements in SQL. Also, the use of ORMs, which ensure that user data and the query are sent separately and unable to be thought of by SQL as separate commands, is widespread.

Cross-site request forgeries, where a user is able to be tricked into doing something on your site, are prevented by form libraries that are widespread and use nonce systems.

### TL;DR

*   **Not anymore.**
*   **Remote and Local file inclusions are avoided by using an autoloader that is standard in all major frameworks.**
*   **XSS attacks are avoided by using either a templating language as standard or a front-end framework such as React.**
*   **SQL injections are avoided by using ORMs and widespread knowledge of using prepared statements.**
*   **CRSF attacks are avoided by using a nonce token, which is automatically supported by all major frameworks.**

## Isn't it really slow?

This really depends on what you compare it to. If you compare it to Java, C, or Go, yes. But if you compare it to Python, Ruby, etc., no. In its class of languages, PHP is one of the fastest and improving performance constantly.

Most of the time, your application is slow because the server is overloaded or the database queries are slow. These are issues that will affect you with any language.

### TL;DR

*   **It is slow compared to compiled languages.**
*   **It is fast compared to other scripting languages.**
*   **A website being slow is often not a case of the language used not being fast enough but the server and database causing performance issues.**

## It doesn't really scale.

Actually, any language can scale. A compiled language such as Go, C, or Rust can scale cheaper than a scripted language such as PHP. However, those are not designed to do the same job. The fact is the same with all of them; it simply comes down to the number of servers you use. You can scale any application if you use enough servers. PHP is able to scale cheaper than other scripted languages because it needs fewer resources to start running and can run on smaller memory servers with more CPU.

Also, with scaling, the important thing is the database. If you can scale your database, you can scale your application. The database is harder to scale than application servers. Adding another client reading to your database is easy; however, having your database run quickly and fast is much trickier.

### TL;DR

*   **Any language can scale; it's a matter of how many servers you use.**
*   **The real issue with scaling is the database and not the application language used.**
*   **If you can scale your database, you can scale your application.**

## Should I always use it?

No. Each programming language is better at different things. PHP is very good with web applications. You should use it for building websites and APIs.

If you're building a system application where every ms counts, go with Rust or C.

If you're building an AI application, Python is a good option.

If you're building a SaaS application, PHP is a good option.

If you're building an Android application, Kotlin is a good option.

If you're building an application that runs on multiple platforms, Java is a good option.

### TL;DR

*   **No, each language has its own best use case.**
*   **PHP’s best use case is web applications.**
*   **Go, Rust, C are good for system applications**
*   **Python is good for AI**
*   **Kotlin is good for Android apps**
*   **Java is good for platform-independent applications.**

## Conclusion

Many of the things said about PHP are things that are 10-years out of date. And in our opinion, if someone is giving you 10-years out of date information about a tech subject, this person may not be someone you want to trust as a technical expert.

PHP is a good programming language for creating web applications and we feel that it is the best language for web application development.

## TL;DR

*   **Many of these complaints are 10-years out of date.**
*   **PHP is in our opinion the best language for building web applications.**

## Translations

*   Chinese - [https://www.infoq.cn/article/62WbGkDTJ1rgXav261wi](https://www.infoq.cn/article/62WbGkDTJ1rgXav261wi)
