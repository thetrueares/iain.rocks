---
layout: post
title: "RabbitMQ One consumer blocking others"
date: 2017-02-01 16:30
comments: true
categories: [Debugging]
---
I've been working on a distributed application that requires multiple workers to process items from a queue. I decided to use RabbitMQ as the queue. However I noticed that there was a 10 minute pause or whenever the consumer started up. After looking into it further I noticed that it appeared that only one consumer could run at any given time.

<!--more-->

After doing a lot of searching and looking at various documents and trying to see if it was the library I was using. I discovered that I had to set the number of items prefetched. Once I did this my consumers were able to start almost instantly consuming.

How I set the prefetch configuration using the Qos command. In Go and in PHP (since I had a PHP version to see if it was just the library in Go I was using.)

## Go 

```go
func main() {
	conn, err := amqp.DialConfig("XXXX",
		amqp.Config{
		Heartbeat: time.Second,
		Properties: amqp.Table{
			"connection.blocked" : false,
		},
	})

	blockings := conn.NotifyBlocked(make(chan amqp.Blocking))
	go func() {
		for b := range blockings {
			if b.Active {
				log.Infof("TCP blocked: %q", b.Reason)
			} else {
				log.Infof("TCP unblocked")
			}
		}
	}()
	if err != nil {
		return nil, err
	}

	ch, err := conn.Channel()

	if err != nil {
		return nil, err
	}
	ch.Qos(
		30,     // prefetch count
		0,     // prefetch size
		false,      // global
	)

	msgs, err := ch.Consume(
		"repositories", // queue
		"",             // consumer
		false,          // auto-ack
		false,          // exclusive
		false,          // no-local
		false,          // no-wait
		nil,            // args
	)
  // messages can be processed
 }
```

## PHP

```php
<?php

$connection = new \PhpAmqpLib\Connection\AMQPStreamConnection('xxxx', 5672, 'guest', 'guest');
$channel = $connection->channel();

$callback = function($msg) {
  echo " [x] Received ", $msg->body, "\n";
  sleep(10);
};

$channel->basic_qos(0, 1, false);
$channel->basic_consume('repositories', '', false, false, false, false, $callback);

while(count($channel->callbacks)) {
    $channel->wait();
}
```