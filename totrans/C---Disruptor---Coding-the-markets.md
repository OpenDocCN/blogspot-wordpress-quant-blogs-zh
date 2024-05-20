<!--yml
category: 未分类
date: 2024-05-12 19:33:50
-->

# C++ Disruptor | Coding the markets

> 来源：[https://etrading.wordpress.com/2012/09/20/c-disruptor/#0001-01-01](https://etrading.wordpress.com/2012/09/20/c-disruptor/#0001-01-01)

## C++ Disruptor

### September 20, 2012

I’ve collected some handy links on the [Disruptor](https://etrading.wordpress.com/disruptor/) and lock free programming in general [here](https://etrading.wordpress.com/disruptor/). I’m coding up a Windows specific C++ Disruptor implementation at the moment, using the [Interlocked*](http://msdn.microsoft.com/en-us/library/aa908785.aspx) family of Win32 API functions. I’m using the volatile keyword, in the Microsoft sense to enforce the code ordering intent on the compiler, and the Interlocked functions to address cache coherence when there are multiple writers to, for instance, the RingBuffer cursor.