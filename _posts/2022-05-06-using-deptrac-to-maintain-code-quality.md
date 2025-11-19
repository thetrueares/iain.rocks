---
layout: post
title: Using Deptrac to maintain code quality
date: '2022-05-06'
authors: [iain]
categories: ['PHP', 'Software Quality']
---
Within the PHP ecosystem there are tons of super cool and super useful tools to help you to maintain a good level of code quality. And I use quite a few of them. Today I'm going to go over one of the first code quality tools I added to the Parthenon tech stack right at the start of development - Deptrac.

<!--truncate-->
## What is Deptrac?

Firstly, I'll explain what Deptrac is, since you may not have heard of it.

Deptrac is from the top flight German PHP consultancy [QOSSMIC](https://qossmic.com/) and can be found at [https://qossmic.github.io/deptrac/](https://qossmic.github.io/deptrac/).  

The purpose of Deptrac is to help keep your code architecture clean. It allows you to define boundaries within your code. It'll generate charts and stuff to show you the dependencies and you can create rules for what should depend on what. You can add it to your build pipeline so that if the rules are broken your build fails.

## Defining boundaries

Why would you want to define boundaries? There are several possibilities. You may want to ensure that a module is entirely self-contained and, therefore, reusable. You may want to your code to be in a DDD style domain and monitor the interactions to act like the business does in real life. Or you may want to avoid circular dependencies.

Previously, when joining companies, one of the first thing I would do was create a Deptrac dependency chart for all the internal bundles to see how interconnected they are. I found this useful for just understanding the code and how all the business logic works together.

But whatever your reasoning, when using PHP. Deptrac is the tool for you.

### How to define boundries

Deptrac is configured by using a yaml file, by default, this is `depfile.yaml` within your project root directory. You define `layers` within the yaml config and are able to define the layers based on collectors which are very powerful and flexible. With options ranging from directory, class name, to even implements as seen [here](https://qossmic.github.io/deptrac/collectors/).

For Parthenon, I just use the directory collectors as I'm just dealing with the modules.

Then you define your ruleset, which is determining which layers can depend on which other layers.

A quick extract from my depfile which is a rather basic example. But if you look at the documentation for Deptrac you'll see it can be very powerful and really useful.

```yaml
paths:
  - ./src/Parthenon
exclude_files:
  - .*test.*
layers:
  - name: Athena
    collectors:
      - type: directory
        regex: src/Parthenon/Athena/*
  - name: Notification
    collectors:
      - type: directory
        regex: src/Parthenon/Notification/*
  - name: Common
    collectors:
      - type: directory
        regex: src/Parthenon/Common/*
  - name: User
    collectors:
      - type: directory
        regex: src/Parthenon/User/*
  - name: Funnel
    collectors:
      - type: directory
        regex: src/Parthenon/Funnel/*
  - name: Health
    collectors:
      - type: directory
        regex: src/Parthenon/Health/*
  - name: RuleEngine
    collectors:
      - type: directory
        regex: src/Parthenon/RuleEngine/*
  - name: Invoice
    collectors:
      - type: directory
        regex: src/Parthenon/Invoice/*
  - name: Payments
    collectors:
      - type: directory
        regex: src/Parthenon/Payments/*
  - name: Subscriptions
    collectors:
      - type: directory
        regex: src/Parthenon/Subscriptions/*
  - name: Plan
    collectors:
      - type: directory
        regex: src/Parthenon/Plan/*
ruleset:
  Payments:
    - Common
    - Subscriptions
  Subscriptions:
    - Common
    - User
    - Athena
  Plan:
    - Common
    - User
    - Athena
  Athena:
    - Common
  User:
    - Common
    - Notification
    - Athena
    - RuleEngine
  Notification:
    - Common
  Funnel:
    - Common
  Health:
    - Common
  Invoice:
    - Common
  RuleEngine:
    - Athena
    - Common
    - Notification
  Common:
```

## Benefits

For me, the main benefit of using Deptrac is that I can add it to my CI testing suite and have the code checked on every commit to ensure that the boundaries are being respected. It is super easy to import a class, interface, constant from another namespace and not think much of where it's coming from or even notice. Having Deptrac check can avoid awkward problems that code became interconnected and no one noticed.

Another benefit that I really got to value more recently is that it can help show when there is possibly a hidden domain/boundary within the code that isn't defined.

The hidden boundary issue happened recently within the Parthenon code base. I had a module Plans and a module Payments. Payments depended on Plans to find the price based on the Plan and I ended up with a recent change with Plans depending on Payments. The underlying issue was I had Subscriptions within Payments and Plans and needed knowledge of Subscriptions.

![](/images/blog/using-deptrac/before-problem.png)

After some time thinking about it, it became clear the issue was that Subscriptions didn't belong in Payments. Subscriptions needed to be it's own module that Payments depended on. And Plans should be part of the Subscriptions module. Without Deptrac bringing the boundary issue to my attention, I would not have had reason to rethink the code structure at all.

![](/images/blog/using-deptrac/after-problem.png)

## Conclusion

I feel like Deptrac is the hidden gem in the code quality tooling we have within PHP. It's not as often discussed but can provide a layer of code quality that I feel can't be provided by other tooling within the PHP ecosystem. It can provoke thought about your code quality on an architectural level that can easily be ignored during normal development.
