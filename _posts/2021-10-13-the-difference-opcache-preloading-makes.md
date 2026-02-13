---
layout: post
slug: the-difference-opcache-preloading-makes
title: "How Much of a Difference does Opcache Preloading Make?"
date: '2021-10-13'
authors: [iain]
tags: ['Technical']
---
With the release of PHP 7.4, comes the addition of opcache preloading. While it's probably one of the best additional features, it's also one of the lesser-known features. Today we're going to show you how much of a difference opcache preloading can make.

<!--truncate-->
## What is opcache preloading?

As some people may be wondering what opcache preloading is, we will answer that first by explaining PHP, opcache, and then opcache preloading itself.

PHP is an interpreted language. This means that when a file is interpreted at runtime, it is read and all lines are translated into commands for the computer to run. Since a PHP script typically won't change between executions, a lot of the commands that have been translated will be the same for each execution. Opcache is a way that PHP stores the bytecode for the script, so that PHP doesn't have to translate the same commands each run. This provides a performance boost as the less work the PHP has to do per execution, the faster it runs.

Now that you have a better idea of what opcache is, we can answer the question as to what opcache preloading is. Opcache preloading means that the PHP will preload specific files into the opcache for every request. This means that the PHP won’t need to read the file and determine if it’s in the cache or load the cache, it’ll be automatically available. PHP will then use the opcache commands for the preloaded files, which are stored in a shared memory between requests.

So, opcache preloading is when you have PHP cache the bytecode for your PHP application into shared memory, so that, for each request, it doesn’t need to load or translate the PHP source code into bytecode, as it’ll be automatically available.

## What difference does it actually make?

This sounds like a useful feature; however, will it only provide a 1% performance boost or will it actually make a significant difference to the optimization? Well, the point of this blog post is to answer that question. To show you the difference it would actually make, I spun up a cloud instance and ran some tests.

### Test Env

For this test, I used:

*   PHP 8.0
*   Symfony Demo App
*   Digitalocean droplet
*   k6.io

I ran two tests: One test with 10 virtual users on a 1GB/1CPU droplet and a second test with 100 virtual users on a 16GB/8CPU. Please note, I just resized the instance to increase it.

### Requests Per Second

![](/images/blog/opcache/meta-chart-1024x683.png)

**Larger is better**

As expected, preloaded achieved better results each time. On the $5 droplet, a 20% improvement was seen, going from 53 to 66 requests per second. On the $90 instance, a 30% improvement was noted, going from 254 to 337 requests per second.

### Response time

![](/images/blog/opcache/meta-chart-1-1024x683.png)

**Smaller is better**

Again, we can see a clear benefit with preloading. On the small droplet, the time went from 203ms to 171ms, which is a 13% improvement. On the larger droplet, we saw a 25% improvement in response times, with a drop from 445ms to 323ms.

## Conclusion

Looking at these stats, it’s clear - if you're running multiple servers to host your application, there is a strong possibility that you could remove the need for an entire server or more, just by enabling the opcache preloading. So, if you're speaking to your boss and struggling to justify why you should upgrade your PHP or make this change, all you need to tell them is: it'll save you money on server costs, which means an extra round at the bar for Friday night beer sessions.