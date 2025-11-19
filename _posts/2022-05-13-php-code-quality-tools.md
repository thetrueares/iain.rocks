---
layout: post
title: "PHP Code Quality Tools"
date: 2022-05-13
draft: false
categories: ['PHP', 'Software Quality']
authors: [iain]
---
Building software is difficult and it's easy to make mistakes. To help developers keep the quality of their code high, developers have created an array of tools to help. From testing tools to ensure the code works to code styling tools to ensure code is consistently readable to Linters.

<!--truncate-->
# Testing Tools

Testing is an extremely important if not the most important part of code quality. There is no point in having highly decoupled, well abstracted, and performant code if it doesn't work. No point at all. So testing is right at the top of code quality tools.

## PHPUnit

Considered the defacto testing tool in the PHP world, PHPUnit is derived from JUnit. PHPUnit has been integrated with most frameworks for example, Symfony comes with it's own extension to the PHPUnit tool to allow for better testing with the Symfony framework.

Using PHPUnit will allow you to automate testing from unit testing all the way to end to end testing using extensions for Selenium.

More information can be found at [https://phpunit.de/](https://phpunit.de/)

**Used by Parthenon**

## Behat

Behat is the BDD testing tool. It allows creating tests based on examples written using the Gherkin language spec. This allows you to create examples with non-technical people that they're able to read, understand, and correct. Then to use those examples as tests to ensure that you've built an application taht delivers these.

More information can be found at [https://behat.org](https://behat.org)

**Used by Parthenon**

## PHPSpec

PHPSpec is an opinionated unit testing tool. Often considered a competitor to PHPUnit, in reality it provides different functionality. PHPSpec is only for unit testing, as in testing an isolated unit of code.

PHPSpec is great for Test Driven Development, where you write the test before you write the code to test. PHPSpec will create the class and method based on the signatures in the Spec.

As I said PHPSpec is opinionated. If you don't write code the way they authors think is a good way to write code PHPSpec can be very painful to use. If you want to do SOLID style development then PHPSpec can help you.

More information can be found at [https://phpspec.org](https://phpspec.org)

## Codeception

Codeception is an all in one testing framework that is styled after BDD. It provides a fluent interface to create easy to understand tests on all levels of testing.


More information can be found at [https://codeception.com](https://codeception.com)

## Pest

Pest is a testing framework that uses the BDD style testing and is focused on simplicity. It is quite popular within the Laravel community and comes with good integration with the Laravel framework.

More information can be found at [https://pestphp.com/](https://pestphp.com/)

## Infection

Infection is a Mutation Testing. Mutation testing is where things are mutated to input incorrect values and see how your system handles it. Since a lot of bugs in production come from inputs and outputs not being what we expected, mutation testing can be extremely useful for testing.

More information can be found at [https://infection.github.io/guide/](https://infection.github.io/guide/)

# Static Code Analysis tools

Static code analysers can find bugs extremely quicker and more efficiently. They will look at all the data available such as data types, method signatures, etc. and report potential issues. It's often possible that code will work when used in a specific way but is vulnerable to flaws when it is used in a different way later.

The two tools listed are very similar; they have slight differences, however both are very good.

## PHPStan

PHPStan is a static code analyser that allows for multiple levels of strictness to allow you to onboard a legacy progress at steps.

PHPStan also has a pro version!

More information can be found at [https://phpstan.org/](https://phpstan.org/)

**Used by Parthenon**

## Psalm

Psalm is the static code analyser from Vimeo. Again it allows for multiple levels of strictness to onboard legacy applications.

It has a web version so you can share code snippets and show examples with the errors from Psalm clear.

More information can be found at [https://psalm.dev](https://psalm.dev)

## Deptrac

Deptrac provides code analysis for tracking dependencies. It allows you to define what things should depend on other things.

Examples:

* Bundles are self contained
* Entities don't depend on repositories
* Controllers don't use repositories directly

More information can be found at [https://qossmic.github.io/deptrac/](https://qossmic.github.io/deptrac/)

## ScanMyCode

ScanMyCode is a new startup working on adding

it has a community edition at [https://github.com/marcinguy/scanmycode-ce](https://github.com/marcinguy/scanmycode-ce)

More information can be found at [https://www.scanmycode.io/](https://www.scanmycode.io/)

# Code Style

Having code style guidelines is almost considered a must in most development teams. It allows all the code to look the same and makes it easier to read and edit code without having to worry about what the code looks like.

## CodeSniffer

CodeSniffer is one of the code style tools that has been around for years and is extremely well battle-tested.

CodeSniffer just finds errors. You have to fix them yourself.

More information can be found at [https://github.com/squizlabs/PHP_CodeSniffer)

## PHP-CS-Fixer

PHP-CS-Fixer automatically fixes your code style issues. It allows for just detecting issues and returning an error code and can be used as part of a CI process to ensure the code committed passes the code style rules.

It is advisable to use a githook to run php-cs-fixer. Thus making your code style process painless and effortless.

More information can be found at [https://github.com/FriendsOfPHP/PHP-CS-Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer)

**Used by Parthenon**

# Commerical Cloud

There are commercial PHP code analysers that run in the cloud. These have extra checks and run on their systems and often include dashboards and extra tools to help with the development process.

## Exakat

Exakat comes with the option for self-hosted or using their cloud service.

Exakat can also provide you pull requests with automatic easy fixes.

More information can be found at [https://exakat.io/](https://exakat.io/)

## Scrutinizer

Scrutinizer was maybe the first cloud-based code analysis tool for PHP.

It can provide more than just code analysis allowing you to test code to. It provides a lot of support for emulating environments, such as docker, Heroku, apache2, etc.

Scrutinizer can also provide you pull requests with automatic easy fixes.

More information can be found at [https://scrutinizer-ci.com/](https://scrutinizer-ci.com/)

## SonarCloud

SonarCloud is the commercial cloud offering from SonarQube that supports lots of languages.

It just handles code analysis.

More information can be found at [https://sonarcloud.io/](https://sonarcloud.io/)
