<!--yml
category: 未分类
date: 2024-05-18 05:37:27
-->

# Midori: Fine-Grained Process Scaling | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/12/02/midori-fine-grained-process-scaling/#0001-01-01](https://mdavey.wordpress.com/2015/12/02/midori-fine-grained-process-scaling/#0001-01-01)

## Midori: Fine-Grained Process Scaling

Finally, Joe [Duffy](http://joeduffyblog.com/) has started blogging again, and with it, we get details of [Midori](http://joeduffyblog.com/2015/11/03/blogging-about-midori/) (programming language, compilers, OS, its services, applications, and the overall programming models), the multi-year journey.

> A key to achieving asynchronous everything was ultra-lightweight processes

I’d be interested to know if Midori influenced [Orleans](http://research.microsoft.com/en-us/projects/orleans/) – given the actor model similarities.  Orleans code is available in [GitHub](http://dotnet.github.io/orleans/).

Throughout the “Asynchronous Everything” article there are a number of great callouts:

*   Midori did not have demand paging which, in a classical system, means that touching a piece of memory may physically block to perform IO.
*   Midori was an entire OS written to use garbage collected memory – Unfortunately, we don’t see Joe offer a view if Midori was a viable production OS.
*   Avoid superfluous allocations like the plague.  Gen0 collections are NOT free.
*   One of the tricks to garbage collection working at the scale of Midori was precisely the fine-grained process model, where each process had a distinct heap that was independently collectible.
*   Processes were ultra-lightweight and single-threaded – event loop based.
*   Batches of messages could be stuffed into channels before they filled up. They were delivered in chunks at-a-time – Interesting, as similar concepts have been used in financial software for many years.
*   “zero-copy”, SharedData was a automatic ref-counted pointer to some immutable data in a heap shared between processes.  Interested in how this worked across machines
*   causality IDs that flowed with messages across processes
*   asynchronous everywhere

~ by mdavey on December 2, 2015.

Posted in [.NET](https://mdavey.wordpress.com/category/languages/net/)