<!--yml
category: 未分类
date: 2024-05-18 05:00:35
-->

# Magmasystems Blog: First experiments with Velocity

> 来源：[http://magmasystems.blogspot.com/2008/07/first-experiments-with-velocity.html#0001-01-01](http://magmasystems.blogspot.com/2008/07/first-experiments-with-velocity.html#0001-01-01)

I played around with

**Microsoft Velocity**

this past weekend, and I put together a little Order Cache. This application reads

**FIX**

messages off of a

**Tibco EMS**

bus, turns the messages into a C# object, and stores the object in the Velocity cache.

The primary key of the Order Cache is the

**ClOrdId**

, and this value should be unique for each trading day. Every time we see a FIX message, we check to see if an object with the same ClOrdId is in the cache. If it is, the Order object is updated, and store the object back in the cache. The order and execution state is kept, the quantities are updated, and Cancels and Cancel/Replaces are accounted for.

Admittedly, it is an extremely simple application, but I did it just so I could get familiar with the first CTP of Velocity. One cache holds all order objects. I did not try to alpha-partition the orders by symbols amongst different caches, nor did I experiment with multiple regions yet. Just simple Gets, Puts and Adds. I used Reflector a bit to peer into the Velocity code, and I could see that there is a lot more hidden under the surface of Velocity that has not been exposed yet.

Where can we use an object cache with a Complex Event Processing system?

First, we can use it to support resiliency of the CEP system. Let’s say that our CEP engine crashes in the middle of the day. We want to be able to retrieve the current state of our orders and executions, but we don’t want to have to go back to some sort of FIX repository, and play back each FIX message in order to re-create the state of the CEP engine. We can use the object cache to aid in recovering the state.

Now, most CEP engines have a facility where they can save state. For instance, with Coral8, you can choose to save all windows out to a database every n seconds or minutes. But, there is a certain tension with persistence of a CEP engine that is processing fast streams of real-time data. If you persist too frequently, you can slow down the CEP engine. If you persist infrequently, then you can lose a significant amount of your state if the CEP engine fails.

Most of the CEP engines will use an external database like SleepyCat, BerkeleyDB, and SQL Server to store state. But, depending on the size and shape of your saved data, recovery might be slow. So, why not save to an object cache? Reading and writing to an object cache would be extremely fast, and if the object cache supports asynchronous storage to a back-end database (or Microsoft’s SSDS), then you can have the best of both worlds.

Among the various CEP engines, I have not seen any built-in adapter support for object caches, like Gemfire, Tangasol, GigaSpaces, and Velocity. It would be fairly easy to write one, but it takes time to marshal between a native C# object and something like a Coral8 tuple.

**Wish #1: The CEP vendors to explore object caches as a way to do persistence.** 

Another use of an object cache is to assist with a query façade. CEP engines like Coral8 support the notion of ad-hoc queries of the windows. If the CEP engine is aggregating data like orders and executions inside a publicly queryable window, any application should be able to query the CEP engine for something like “What are the top ten stocks that have open orders between 10:15 and 10:30”.

We don’t want external applications connecting directly to the CEP engine. There are compliance and security issues involved, and we don’t want any application tied to a particular variant of Streaming SQL. (Note: Coral8 has SQLite embedded in it, and that is what you use to query the public windows.) Therefore, we want to provide a “query façade”. All applications have to connect to the query façade in order to do ad-hoc querying of the CEP engine.

There is a cost to performing ad-hoc queries on the CEP engine while it is trying to process tons of streaming data. And, unless you index your public window correctly, the ad-hoc query can be very slow.

So, why not be able to query the object cache instead? If we are storing aggregated orders and execution data inside of Velocity, why can’t we query Velocity to find the top ten stocks that have open orders between 10:15 and 10:30? In other words, querying an object cache should be almost the same as querying an SQL Server database. I don’t care if the query language is SQL 92, Streaming SQL, LINQ, or the LINQ-ish thing that SSDS has…. As long as it’s not Q :-)

**Wish #2: Microsoft will get together with the object cache and CEP vendors and come up with a common method to query database, caches, and CEP engines.** 

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.