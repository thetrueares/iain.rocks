---
layout: post
slug: how-to-remove-secrets-from-logs-with-monolog
title: How to remove secrets from log with monolog
date: "2021-08-01"
authors: [iain]
categories: [PHP, Logging]
---
Logging is a very important part of operating an application if you're unaware of what happened in your system you're unable to quickly and efficiently identify the issue. However, logging can open up some potential pitfalls. One of them being including secrets and other sensitive information within the logs accidentally. [Twitter](https://www.bleepingcomputer.com/news/security/twitter-admits-recording-plaintext-passwords-in-internal-logs-just-like-github/) and [Github](https://www.zdnet.com/article/github-says-bug-exposed-account-passwords/) both accidentally logged people's passwords in plain text. To help protect our users we've made it so that we automatically filter passwords out of the logs created via monolog. And we're going to share how we did it so you can also ensure your logs are also secret free.

<!--truncate-->
## Removing Secrets with Monolog using Processors

The way we filter out Monolog entries of passwords is by using the `Monolog\Processor\ProcessorInterface` to create our own custom Monolog processor. What a Processor does is when Monolog gets a log entry then Monolog runs all the processors it has on the log entry and this allows people to add data or in our case remove data.

Here is the code for our password filter processor.

```php
<?php

namespace Parthenon\User\Logging\Monolog;

use Monolog\Processor\ProcessorInterface;

final class PasswordFilterProcessor implements ProcessorInterface
{
     private CONST PASSWORD_KEY = 'password';
     public function __invoke(array $record): array
     {
        foreach ($record as $key => $item) {
            if (self::PASSWORD_KEY === strtolower($key)) {
                $record[$key] = '****';
            } elseif (is_array($item)) {
               $record[$key] = $this($item);
           }
        }
        return $record;
    }
}
```

This works by going through the array given and checking each item to see if the key is equal to the password and if it is then it filters it out. If not it checks to see if it's an array and if so it calls the processor recursively. This concept can be used to deal with whatever secrets you want to filter out.

An extremely easy thing to do but often not even thought of. The fact Twitter and Github both got caught out with this and I personally have seen secrets developers won't DM each other via Slack in plain text in the logs shared via Slack show this can be an easy thing to overlook.