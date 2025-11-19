---
layout: post
title: "Go dep in Docker"
date: 2017-02-04 12:30
comments: true
categories: [Debugging]
---
Go's dependency handling has been an area which has been needing unification, over the years. Multiple package managers have been created. The Go community has been working on creating a dependency manager recently, which they plan on getting added to the official toolchain. I've decided to jump on the bandwagon and start using this tool. Here's how I've been using it in docker.

<!--more-->

The first issue I encountered was the command `dep` not being found. It turned out my original docker build file had `GOBIN` pointed to somewhere that was not in the `PATH` env for some reason. Looking at the original `Dockerfile` for golang it `GOBIN` doesn't appear to be set at all. So I've set it to `/go/bin` which has already been added to the path.

The next issue was, I was storing and building my code outside of the `GOPATH`. So I moved where I was storing my code to inside the `GOPATH`. With that done it was just a case of running the `dep` commands.

An example `Dockerfile` can be found below.

```dockerfile
FROM golang:1.7

# Set go bin which doesn't appear to be set already.
ENV GOBIN /go/bin

# build directories
RUN mkdir /app
RUN mkdir /go/src/app
ADD . /go/src/app
WORKDIR /go/src/app

# Go dep!
RUN go get -u github.com/golang/dep/...
RUN dep ensure

# Build my app
RUN go build -o /app/main .
CMD ["/app/main"]
```
