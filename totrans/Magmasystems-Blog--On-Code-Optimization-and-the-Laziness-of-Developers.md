<!--yml
category: 未分类
date: 2024-05-18 05:02:01
-->

# Magmasystems Blog: On Code Optimization and the Laziness of Developers

> 来源：[http://magmasystems.blogspot.com/2008/06/on-code-optimization-and-laziness-of.html#0001-01-01](http://magmasystems.blogspot.com/2008/06/on-code-optimization-and-laziness-of.html#0001-01-01)

A very wise man, someone who runs the group that owns our more important trading framework, once said to me “I don’t know why we spend all of this effort in investigating Hardware Acceleration. If we actually went into our code,

refactored

it, and optimized it, we could probably speed up the end-to-end performance by 50%.”

I have always maintained that the continued use of high-level, object-oriented programming languages has made the average programmer lazy. Perhaps it is the pressure of continually churning out releases, but some of the code that I have seen lately is abysmal. Game programmers would cringe if they ever saw some of this code. So would a good number of people who started their lives programming in C (and even C++).

I started programming professionally in 1984\. My first commercial product, a word processor for UNIX and the PC, had to run in 128K of RAM. I can’t tell you the number of hours I spent riding the subway, looking over a file of code to see what optimizations I could make in a function or two. That whole optimization-conscious culture seems to have fallen by the wayside.

However, take heart, Mr. Corporate Programmer. It’s not only your code that I am finding fault with.

Last Friday, I dropped down from Manager Mode into Code Optimization Mode. I wanted to optimize a particularly crucial part of our system. Our system is written in C#, so we are using the .NET

SDK

that is provided by one of the vendors. I notice that vendors who provide

SDKs

for Java, C++, and C# usually tend to treat the C#

SDK

as a second-class citizen. I have blogged about this before, and in this case, I felt that it was no different with this vendor. As I debugged into the vendor code, I was amazed at some of the things that I found, and in about 30 minutes worth of time, I had fired off six emails to the vendor.

I found things like this:

[Snippets of Code removed for now]

However, I just scratched the surface of their .Net

SDK

. I did not give it a full profiling, nor did I bother to give it a code review. This is not my job. It is the vendor’s job to do this.

Just to make sure that I

wasn

’t bitching about nothing, I showed the code to a colleague who runs one of our departments. He was an old C game developer way back when. When I showed him the code, he shook his head, and said that there was no excuse for this laziness.

Since this code is called about 2 million times per day, I am very concerned. If I found these kinds of anomalies in source code that is made public, what could be lurking under the covers of the actual engine of the product?

In summary, I have some advice for vendors and for coders everywhere:

*   1) Continually optimize and refactor

*   2) Put your code through a profiler. Use the .NET CLR Profiler. Use DevPartner Studio. Use the built-in profiler in Visual Studio 2008.

*   3) Don’t treat C# as a pariah. If you are going to put out a .NET SDK, make sure that it is just as good as your Java and C++ SDKs. And, when you refactor your java SDK, refactor the C# SDK as well.

*   4) Quality control. In this case, we see that the vendor did not do their due diligence with regards to the .NET SDK. Code coverage and unit tests must be done.

*   5) If you make an enhancement in one superclass, make sure you enhance all of the other superclasses as well.

*   6) Code reviews. Get more pairs of eyes on that code!

For my part, I just had one of our junior developers refactor some of the code that parses our FIX messages and converts them into C# objects. He replaced 3 calls to string.Substring() with one call to string.Split(). After running some tests, he said that we only had a 2% improvement. For code that is called a few million times per day, I will gladly take that 2%, not to mention less small things going into the heap.

We need to start working on code coverage, but right now, we need to get a system out there to the traders .... and we have the luxury that nobody except us will be looking at our code!

©2008 Marc Adler - All Rights Reserved