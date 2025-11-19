---
layout: post
title: Some Monolog logging best practices
date: '2022-06-03'
draft: false
authors: [iain]
categories: ['PHP', 'logging']
---
Logging can help to debug massively. Today, we'll go over some of the best practices for logging with Monolog I've learnt over the years.

<!--truncate-->
# Tracer/Process ID

One of the first things that makes reading logs easier is the ability to group the logs together. You often want to figure out what happened after a log message happened and to be able to see all the records for a request or process.

Adding a process id to the extra array of your via a processor, such as something similar to the below code, will add a process_id to all your logs so you'll be able to quickly group logs together to see what happened as the process happened.

Monolog comes with a UidProcessor that can be used to do this : https://github.com/Seldaek/monolog/blob/main/src/Monolog/Processor/UidProcessor.php

# Adding request information

It can be helpful to have all the request information such as URL and method in the logs. This can allow you to find all the logs that go to a specific endpoint via a specific method.

Below is an example of how to add this information.

```php
<?php

declare(strict_types=1);

/*
 * Copyright Iain Cambridge 2020-2022, all rights reserved.
 */

namespace Parthenon\Common\Logging\Monolog;

use Monolog\Processor\ProcessorInterface;
use Symfony\Component\HttpFoundation\RequestStack;

final class RequestProcessor implements ProcessorInterface
{
    private RequestStack $requestStack;

    public function __construct(RequestStack $requestStack)
    {
        $this->requestStack = $requestStack;
    }

    public function __invoke(array $record): array
    {
        $request = $this->requestStack->getMainRequest();

        if (!$request) {
            return $record;
        }

        $record['extra']['request_uri'] = $request->getUri();
        $record['extra']['request_method'] = $request->getRealMethod();

        return $record;
    }
}
```

## Create unique searchable log messages

When you see a log message in the code what you search for to find all log messages generated at that point and only at that point.

* Don't have variables in the log message
* Don't use the exact same log message in more than one place.

## Use the context array

When logging information, context for a log message is important. Often people add this context to the actual message so the message has all the information. This stops the message being as easily searchable. It's possible to create searches to find these messages, but those searches aren't as nice.

Example

`The user example@example.org has updated profile 2303` would need the search `has updated profile` to find all the logs for it.

`The user has updated the profile` with the user email and profile id in the context array. We can just search for the specific log message.

Also, when the context is in the log message, then systems like Kibana can't allow you to filter and aggregate this information.

Using the context array field in Monolog will allow you to filter in systems like Kibana while having easy to search messages.

## Filter out secrets

Having secrets in your logs is not good. Both GitHub and Twitter at separate times, logged user sensitive information in their logs.

A common one is when you're logging the input from a user that you log their password in plain text. It is best if you create a way of filtering out sensitive information automatically to ensure no accidental luggage of sensitive information.

An example:

```php
<?php

declare(strict_types=1);

/*
 * Copyright Iain Cambridge 2020-2022, all rights reserved.
 */

namespace Parthenon\User\Logging\Monolog;

use Monolog\Processor\ProcessorInterface;

final class PasswordFilterProcessor implements ProcessorInterface
{
    private const PASSWORD_KEY = 'password';

    public function __invoke(array $record): array
    {
        foreach ($record as $key => $item) {
            if (is_string($key) && self::PASSWORD_KEY === strtolower($key)) {
                $record[$key] = '****';
            } elseif (is_array($item)) {
                $record[$key] = $this($item);
            }
        }

        return $record;
    }
}    
```

## Convert exceptions to an array

Passing exceptions in the context is rather common. However, when this is converted to JSON, it creates an ugly unsearchable text representation of the exception.

In my opinion, it's better to convert these exceptions to an array that contains the exception information.

I've found it's also better to not include the backtrace as this can result in the length of the log message string being too long and the log message not being parsed correctly.

Example:

```php
<?php

declare(strict_types=1);

/*
 * Copyright Iain Cambridge 2020-2022, all rights reserved.
 */

namespace Parthenon\Common\Logging\Monolog;

use Monolog\Processor\ProcessorInterface;

final class ExceptionProcessor implements ProcessorInterface
{
    public function __invoke(array $record)
    {
        $output = [];

        foreach ($record as $key => $value) {
            if (is_array($value)) {
                $output[$key] = $this->__invoke($value);
            } elseif ($value instanceof \Throwable) {
                $output[$key] = [
                    'message' => $value->getMessage(),
                    'file' => $value->getFile(),
                    'line' => $value->getLine(),
                    'code' => $value->getCode(),
                ];
            } else {
                $output[$key] = $value;
            }
        }

        return $output;
    }
}
```

## Logging the input and output for API calls.

When dealing with integrations with lots of partners being able to debug while something isn't working is often down to knowing what the inputs and outputs are. Clients will often think they sent something but when you look at what they actually sent then you'll be able to find the error is just user error. Sometimes they claim you didn't return the correct information.

Other times, it's good to see what they sent so you can correctly reproduce the call.

Trying to test integrations with other partners without this data is terrible and not fun. I highly advise against doing it.

## Adding a log message to all controller actions and commands

One of the easiest things to do that can help is by adding a unique log message to the first line of all controller actions and commands. This then gives you a log message you can use to find all those requests/command runs.

Often you're left with searching for various other messages that can occur during a request to find the correct message. This just takes time and is annoying. Since sometimes, that log message could be in a service class and be usable from multiple places. It is a lot easier to be able to have a single message that allows you to quickly identify all the logs from that endpoint/command.

This is often the second logging task I do when joining a new project, straight after adding a process id to the logs.
