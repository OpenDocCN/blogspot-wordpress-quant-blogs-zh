<!--yml
category: 未分类
date: 2024-05-18 04:58:06
-->

# Magmasystems Blog: Coral8 and Performance

> 来源：[http://magmasystems.blogspot.com/2008/10/coral8-and-performance.html#0001-01-01](http://magmasystems.blogspot.com/2008/10/coral8-and-performance.html#0001-01-01)

From the head of our

CEP

engine development team (used with his permission) :

I'm pleasantly surprised at how fast c8 is when one gets it right. (On the other hand, one misstep and performance goes over the cliff.)

This is one of the main problems with the variants of Streaming

SQL

that you find in many of the

CEP

engines. It is not at all transparent what goes on under the hood of all of the

CEP

engines when you are writing complex queries in Streaming

SQL

.

Unlike Microsoft, where you find very good profiling tools in

SQL

Server, the

CEP

vendors do not provide the necessary tools that will enable a developer to isolate bottlenecks. This has been an issue with Coral8, which they recognize and hope to remedy in the future.

Every time that I've cursed out Coral8 for what I might think is lousy performance, it has turned out that it was

us

that managed to write a query that clogged the engine. And, when you clog up Coral8, it can bring an entire machine down very quickly as the pending message count builds up.

The important thing is about choosing a

CEP

vendor is the level of technical support, and despite some turnover in Coral8's tech support staff (goodbye to the excellent

Trahn

), we have been able to have access to their chief architect and to the head of development when we have really gotten ourselves into trouble. Coral8 also recently hired a New York-based support person who used to be an architect with Gemstone. So, even though it will take this guy some time to get up to speed with Coral8, we are glad to have a local person to help us when we need the assistance.

Coral8 has just released version 5.5, which will be a major help to us in terms of real-time

OLAP

and entitled subscriptions. It is a major release that will force us to refactor some of our code. But, it is good to see that Coral8 is making it easier for us to implement our real-time dashboards where every user can possibly be entitled to see a different view of data. I feel that support for real-time

OLAP

is going to be a major selling point for

CEP

systems, as it is *really hard* to implement it totally on your own.

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.