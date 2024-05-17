<!--yml
category: 未分类
date: 2024-05-18 05:18:11
-->

# Magmasystems Blog: GemFire

> 来源：[http://magmasystems.blogspot.com/2006/09/gemfire.html#0001-01-01](http://magmasystems.blogspot.com/2006/09/gemfire.html#0001-01-01)

I am starting an evaluation of object cache technology, starting with

[GemFire](http://www.gemstone.com/products/)

. The target app is a legacy C++ app, so the fact that Gemstone has a C++ version of GemFire is a big plus. They also have .NET bindings, and I will be checking those out too.

One gotcha .... GemFire does not work on Windows 2000 because of the underlying dependencies on 29West's LBM message broker. This is a real nasty if you want to do an evaluation on your desktop at work, but your company is still in Windows 2000-land. So, I had to load up GemFire on my home laptop, which runs XP Pro, and will do the evaluation on my laptop.

The plans are to use the object cache as a "data fabric" in order to speed up some of our calc engines. Object Caches like GigaSpaces are used already in a lot of Wall Street IBs just for that purpose. I have heard a little rumbling about GigaSpace implementations from some former colleagues, so we are hoping that GemFire will be worry-free. Already, I am impressed with their support staff (thanks to Mike and Santiago for timely responses).

I would be interested in comments from any of you people who have evaluated or used object caches in your financial apps, especially C++ or C# apps. Feel free to comment here or email me privately.

©2006 Marc Adler - All Rights Reserved