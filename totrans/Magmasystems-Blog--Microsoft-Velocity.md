<!--yml
category: 未分类
date: 2024-05-18 05:01:49
-->

# Magmasystems Blog: Microsoft Velocity

> 来源：[http://magmasystems.blogspot.com/2008/06/microsoft-velocity.html#0001-01-01](http://magmasystems.blogspot.com/2008/06/microsoft-velocity.html#0001-01-01)

I have blogged a number of times about Distributed Object Caches. Almost all large financial firms have investments in object cache products. The three biggies are Gemfire, Tangasol Coherence (now part of Oracle), and GigaSpaces, and traditionally, these companies have targetted the Java and C++ marketplaces.

There have been niche products like NCache and memcache, but I have not seen an incredible amount of use of these out there in Wall Street.

If you have been reading this blog for any length of time, you know that I constantly lament the fact that Microsoft did not have what I refer to as "The Wall Street Stack".

However, last week, Microsoft landed with both big boots on the Wall Street Stack with the introduction of Velocity, their first attempt at a distributed object cache. Velocity, combined with some other efforts that Microsoft is working on (I have been sworn to secrecy on these efforts), dispells my ideas that Microsoft is ignoring enterprise technologies that matter to Wall Street, and especially, the area of trading systems.

I won't go into my thoughts on Distributed Object Caches, as I have blogged about them many times. But, I just want to list of few things that went through my mind as I read the Velocity announcement. I have a call this week with the Velocity team, and I hope to ask them these questions:

1) Will it remain free? I hope so. For the companies who pay lots and lots of money to Gemstone, Tangasol, and GigaSpaces, a free entry into this arena from a major vendor is sure to make the other vendors think about lowering their prices. In these economic times, financial companies will certainly welcome the chance to embrace this technology without having to spend a lot of money.

2) Will it be supported? If so, for how long, and by what product group? Microsoft is well known for coming out with technology that they let languish or deprecate. Right now, it seems like there is a small group in Microsoft that is working on Velocity. Does Microsoft have the appetite to build a support organization to properly support the product?

3) What are the synergies with other Microsoft technologies? LINQ? SQL Server? Gemfire has a SQL query language which you can apply to the data in their cache.

4) The Velocity team already said that they do not have push notifications yet. But, when they do, can we integrate a version of streaming LINQ (CLINQ?) with it? Push notifications is an extremely important feature that Velocity is missing right now, but it seems that a lot of people have told the Velocity team that this is a major shortfall.

5) Support for different messaging systems. Once we are able to get push notifications from Velocity, can we use JMS/Tibco EMS or RV?

6) Interface with Grids. It is no secret that the most prevelant use of object caches on Wall Street is with Grid Computing. How will Velocity interface with Compute Cluster? How about Digipede (if I know John Powers, he probably has support for Velocity already)?

7) Interoperability with non .NET-based systems?

8) What external database systems to they support? Will they support Oracle and Sybase? How about KDB?

©2008 Marc Adler - All Rights Reserved