---
layout: post
slug: design-decisions-throw-custom-exceptions
title: "Design Decisions:Throw Custom Exceptions"
date: "2022-12-20"
categories: [Software Design, Design Decision]
authors: [iain]
---
## Decision

> A Parthenon method should not throw exceptions that don't belong to Parthenon. It should catch all third-party exceptions and then throw a Parthenon-owned exception with the third-party exception passed to the new Parthenon exception. If the third-party exception contains valuable custom information for the exception it should be available via the Parthenon exception.

## Reasoning

One of the ways implementation details of an interface can be leaked are by third-party exceptions. If the client code catches and handles a third-party exception then they're coupled to the third-party code. The aim of Parthenon is that everything is replaceable with your own implementation having parts of Parthenon code depend on third-party exceptions - which would happen if Parthenon interfaces threw third-party exceptions. 

And for many parts of Parthenon, the code is usable/extendable/etc by user developers to develop custom applications, if they depend on the third-party exception then their code also becomes dependent on the third-party code. This means if in the future there were to be a change in the third-party code or how the Parthenon code worked internally it would become a breaking change.

The reason to pass the third-party exception to the new exception is that the third-party exception will contain valuable information about what happened and we don't want to lose that. User developers would still be able to use the third-party exception, however, it becomes more obvious that such coupling is fragile. And the custom exception should be able to provide the same information.

TL;DR - Removes the ability to become dependent on third-party code which improves flexibility.

## Support Implications

This means if someone reports:

* A Parthenon interface throws a third-party exception, it must be changed to throw a custom one.
* A Parthenon exception does not contain all the information that is available in the third-party exception, it must be added.