<!--yml
category: 未分类
date: 2024-05-18 06:24:18
-->

# Google Go In Banks? | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/06/04/google-go-in-banks/#0001-01-01](https://mdavey.wordpress.com/2013/06/04/google-go-in-banks/#0001-01-01)

## Google Go In Banks?

Investment banks have historically been quite restricted on what languages can/can’t be used within the software development stack – Java/C#/Flex/JavaScript possibly being the main choices.  This has opened up a little in the last time period, with various banks making large jumps into the Python pond,  smaller jumps into Scala ([Scala vs Go](http://www.cs.colorado.edu/~kena/classes/5828/s12/presentation-materials/smithbrentgibsonleon.pdf)), and even smaller jumps into Clojure.  With the recent release of Go [1.1](http://blog.golang.org/2013/05/go-11-is-released.html), the usual spike on the web to accompany such an event, is it time to investment in this language?

First off, if you’re not familiar with Google Go, try these links:

*   The Go Programming [Language](http://golang.org/doc/effective_go.html#web_server)
*   Rob Pike on Google Go: Concurrency, Type System, Memory [Management](http://www.infoq.com/interviews/pike-google-go) and GC
*   “My favorite programming language:” Google’s Go has some [coders](http://arstechnica.com/information-technology/2013/05/my-favorite-programming-language-googles-go-has-some-coders-raving/) raving
*   Google Go: A [Primer](http://www.infoq.com/articles/google-go-primer)
*   Go [Projects](http://code.google.com/p/go-wiki/wiki/Projects)

A few obvious observations about Go:

*   Go’s main aim appears on the server side
*   Performance, [concurrency](http://blog.golang.org/2013/01/concurrency-is-not-parallelism.html) (language primitive), and simplicity are a few of the attributes that Go offers
*   The compiler is quick

Everyone has their IDE preference, I’m using the Intellij [golang](http://plugins.jetbrains.com/plugin?pluginId=5047) IDE plug-in.  Prior to writing any server application in Go, you may want to look at the Wiki Go projects.  Of interest 😉 are:

*   memcache and Redis
*   MongoDB and Neo4j
*   ZeroMQ, Kafka and RabbitMQ

If you prepared to stretch the Go solution you are considering, and the architecture would benefit, then you might want to glance 😉 at:

Today I suspect nobody is really considering Go within the investment banking arena.  Thus if nothing else, Go is an interesting language to PoC a few idea with if you happen to have a bit of spare time

~ by mdavey on June 4, 2013.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)
Tags: [Concurrency](https://mdavey.wordpress.com/tag/concurrency/), [Go](https://mdavey.wordpress.com/tag/go/), [Scala](https://mdavey.wordpress.com/tag/scala/)