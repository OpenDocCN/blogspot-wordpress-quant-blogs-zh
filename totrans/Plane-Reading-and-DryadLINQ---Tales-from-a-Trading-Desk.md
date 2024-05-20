<!--yml
category: 未分类
date: 2024-05-18 06:14:30
-->

# Plane Reading and DryadLINQ | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2010/08/27/plane-reading-and-dryadlinq/#0001-01-01](https://mdavey.wordpress.com/2010/08/27/plane-reading-and-dryadlinq/#0001-01-01)

For once I wasn’t flight to New York. But as usual one has to read something during these long flights.

*   [jQuery](http://weblogs.asp.net/jalpeshpvadgama/archive/2010/08/27/jquery-javascript-library-write-less-do-more.aspx)– JavaScript Library Write less do more
*   HTML5 [Reset](http://html5reset.org/)
*   HTML5 [Boilerplate](http://html5boilerplate.com/)
*   Azure Throughput [Analyzer](http://research.microsoft.com/en-us/downloads/5c8189b9-53aa-4d6a-a086-013d927e15a7/default.aspx)
*   [Orleans](http://www.zdnet.com/blog/microsoft/orleans-microsofts-next-generation-programming-model-for-the-cloud/7152): Microsoft’s next-generation programming model for the cloud
*   [Rx](http://blogs.msdn.com/b/jeffva/archive/2010/08/20/rx-on-the-server-part-3-of-n-writing-an-observable-to-a-stream.aspx) on the server, part 3 of n: Writing an observable to a stream

So lets get back to DryadLINQ. Dryad has been on my radar for a long time – I’ve also blogged about it a little. One of the problem I have with Dryad and Windows HPC 2008 R2 is the amount of hardware you need to just do development 😦 I’m sure that if I could get more hardware I would have done a lot more than I’ve currently been able to achieve. One think I’ve found to date is that the HPC API is “painful”.

So let me get back to Dryad and Real-Time Market Risk (a topic I seem to be spending a fair amount of time on from solutions to iPad UX). In DryadLINQ, I can get the trades I want to process using

> PartitionedTable trades = PartitionedTable.Get(inputUri);

Which lead to calculating market risk using something like:

> var result = trades.Select(t => Risk(t, curves);

Assuming I have a function:

> TResult Risk(Trade t, Curve[] curves);

However the above is flawed, since I don’t want to send all the curves to every trade as its network bandwidth unfriendly 🙂

**Sidebar:** The DryadLINQ Programming Guide’s samples are primarily driven from a dataset within flat files which again isn’t what I typically have the luxury of using as a trade repository. Given the amount of hardware/software to install for Dryad development, one would have thought Microsoft would propose a simulator mode to speed up development, and reduce cost?

Anyway, back to a better solution which possible comes from the Histogram sample and specifically the BuildHistogram function.

> return inputTable
> .SelectMany(x => x.line.Split(‘ ‘))
> .GroupBy(x => x)
> .Select(x => new Pair(x.Key, x.Count()))
> .OrderByDescending(x => x.Count)
> .Take(k);

Specifically if the trade set is a full book/portfolio, then maybe we want to do a SelectMany and spit to trades by product and then maybe GroupBy currency. We could then send the appropriate yield curves to the correct trades.

More thought needed.

~ by mdavey on August 27, 2010.

Posted in [HPC](https://mdavey.wordpress.com/category/hpc/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)