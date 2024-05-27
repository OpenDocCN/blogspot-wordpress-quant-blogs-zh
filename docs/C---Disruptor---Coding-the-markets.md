<!--yml

类别：未分类

日期：2024 年 5 月 12 日 19:33:50

-->

# C++ Disruptor | 编码市场

> 来源：[`etrading.wordpress.com/2012/09/20/c-disruptor/#0001-01-01`](https://etrading.wordpress.com/2012/09/20/c-disruptor/#0001-01-01)

## C++ Disruptor

### 2012 年 9 月 20 日

我收集了一些关于[Disruptor](https://etrading.wordpress.com/disruptor/)和无锁编程的有用链接 [此处](https://etrading.wordpress.com/disruptor/)。我目前正在编写一个特定于 Windows 的 C++ Disruptor 实现，使用[Interlocked*](http://msdn.microsoft.com/en-us/library/aa908785.aspx)系列 Win32 API 函数。我使用 volatile 关键字，按照微软的意义，来强制编译器执行代码顺序意图，并使用 Interlocked 函数来解决当有多个写入者时，例如，对 RingBuffer 游标的缓存一致性。
