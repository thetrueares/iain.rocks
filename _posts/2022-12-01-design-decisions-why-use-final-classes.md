---
layout: post
slug: design-decisions-why-use-final-classes
title: "Design Decisions: Why use final classes"
date: "2022-12-01"
categories: [Software Design, Design Decision]
authors: [iain]
draft: false
---
I've started to document the design decisions made for Parthenon. One of the main decisions made was to make classes that aren't meant to be extended to be `final`. There are many schools of thought when it comes to development. With many people having different opinions about when and why to use `final` classes, I thought I would add my opinion to the mix.

## Decision

The decision was made to make classes that aren't meant to be extended `final`. All `final` classes should have an interface that matches their publicly available methods.

<!--truncate-->
## Open/Closed Principle

Some people like SOLID principles, and some people don't. Personally, I think trying to apply SOLID principles when they make sense is the way to go. Like all things, they shouldn't be blindly applied. Within Parthenon, there has been attempt to apply SOLID rules. For those not aware Open/Closed Principle is that a module should be open to extension but closed to modifications. To apply that principle to Parthenon, I've used final classes and interfaces.

Each module is open to extension in the fact you can extend what it does by implementing an interface. This will allow you to change almost every part of how Parthenon does things by adding in and using your own extensions. If you want to be able to just extend how something works by doing something before or after the execution there is always the [decorator pattern](https://en.wikipedia.org/wiki/Decorator_pattern).

It is closed to modification in the fact that each implementation in Parthenon's core that is not meant to be extended uses a `final` class.

## Limiting maintainance requirements

Another reason for making classes `final` is it limits the surface area for which other developers can interact with. When a developer is able to extend a class, they can become reliant on how the class functions internally. This means that any changes to how the class functions internally could affect how their application functions and add in breaking changes.

By having classes as `final` the only considerations I need to have are related to the inputs and outputs. These are generally covered by the actual interface that is being implemented.

## When would I not use final classes?

I would not advise using `final` classes on in-house applications. I've worked with people who kept saying all classes should be `final`. These people would say things such as "If it's extendable, we'll need to maintain it if someone extends it. If it's `final` we won't." This line of thought works only if your code is going to be distributed. However, within an in-house application, if someone does something you need to maintain it. It doesn't matter if you originally made it `final` or if you don't like it. You're literally getting paid to maintain the code.

Also, if they're working on the code base and they want to do something but you've made it `final`, then they can just remove the `final` keyword. Making things `final` only works when they can't just remove the `final` keyword so things like libraries, sdk, etc that are being distributed in packages.

## Conclusion

While I'm sure, not everyone is going to like the thought process here and think it's over engineering or whatever. It's how I want to develop; therefore it's how it's been developed. If someone can provide a good reason why something shouldn't be `final` then that will be taken onboard and the `final` keyword removed.

If you're interested in the other design decisions, you can see what has been documented so far at [the design decisions documentation page](/docs/next/design-decisions).

To get started with Parthenon, which is a general functionality bundle for Symfony, you can check out [the getting started guide](/docs/getting-started)
