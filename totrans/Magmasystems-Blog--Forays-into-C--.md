<!--yml
category: 未分类
date: 2024-05-18 04:58:02
-->

# Magmasystems Blog: Forays into C++

> 来源：[http://magmasystems.blogspot.com/2008/10/forays-into-c.html#0001-01-01](http://magmasystems.blogspot.com/2008/10/forays-into-c.html#0001-01-01)

We have a C#/.NET-based Reuters market data adapter that we wrote ourselves (well, actually, I wrote it). This is an out-of-process Coral8 adapter that reads real-time ticks from RMDS, turns then into Coral8 tuples, and feeds them into our Coral8 engine. The adapter has two caches in it, and since market data is last reliable, we can publish the last-reliable ticks from one of the caches at specific intervals.

When we hooked the market data adapter up to our Coral8 engine, we started seeing an immediate backup in the pending message queue. We were sending Coral8 about 3000 ticks per second. In addition, our Coral8 engine was processing our order flow, which could hit a max of another 3000 messages per second.

My first thought was that it was taking too long for Coral8 to deserialize the market data tuple, so I wanted to transform our market data adapter from an out-of-process adapter to an in-process adapter. Unfortunately, in-process adapters have to be written as a vanilla, Win32-based C/C++ DLL.

I grew up on C++. However, I have not touched a lick of C++ since diving into .NET in 2001\. I was scared. I was frightened. However, I know that my teams needs some experience in writing in-process adapters for Coral8, and since my team consists of very strong .NET and Java people, I decided to bite the bullet and take one for the team.

Man, oh man! I can't believe how much I had forgotten! Strange symbols like '*' and '->' were coming from my fingers. Compilation errors sprang up everywhere. There was no

Resharper

to help me along. Linker errors to strange

obfuscated

functions that I swear I never wrote started appearing in the error window.

Perhaps I need to use a little bit of

extern "C"

here? Maybe there? Maybe everywhere!

Where was my .NET Thread class? Where was System.Timer? How do I do events? There is a new kind of pain that you have to go through in order to get callbacks to work within

templated

C++ classes. It took me hours to get simple callbacks to work.

Finally, after two days of work, I got the market data adapter ported over to Coral8\. To start with, let's try reading the ticks from a flat data file instead of from Reuters. Whew, it works. I see the ticks appearing

in the

Coral8 stream viewer. Now, let's try Reuters. After a bit of tweaking and some crashes on the

destructors

, ticks are finally coming in.

Then, I get an email from our Coral8 developer telling me that the reason why the market data feed was slow in Coral8 was because of one of those mysterious coral8 queries that he wrote that clogged the system! So, my

inproc

adapter was not needed anymore. Market data was now zooming through our Coral8 engine.

Nevertheless, it was a fascinating experience to return to my C++ roots from a 7-year hiatus in the .NET world. Never again!

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.