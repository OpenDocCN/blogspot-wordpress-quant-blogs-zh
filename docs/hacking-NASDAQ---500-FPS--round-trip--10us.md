<!--yml

类别：未分类

日期：2024 年 05 月 13 日 00:06:00

-->

# 以 500 FPS 黑客方式攻击纳斯达克：往返时间-10 微秒

> 来源：[`hackingnasdaq.blogspot.com/2010/01/round-trip-10us.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2010/01/round-trip-10us.html#0001-01-01)

就像我们在之前的帖子中发现的，我们的假设是，大部分延迟是在软中断/任务 let 到调用者上下文的切换，也就是调度程序的问题。因此，如果正确，相对于阻塞接收来说，轮询接收应该可以带来很好的加速，当然会有更高的 CPU 使用率，这意味着您的 HVAC 和电费会增加。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgDRZwFEbVIp5W4uVUKuQTbv1AXdS1QkAkb0EJ_9um-fPOfphbnJgwqkWzHmTVgujTcxFWGvAtpFzo28kmbSYFTA4dWtplgYpMQvJUQcIcGMnTQfbugnP7E1y7-kJXKq5dgpZdJKUes9A/s1600-h/tcp_round_default.png)

TCP 128B A->B->A 的往返延迟时间。阻塞 recv() x2

TCP 128B 从 A 到 B 再到 A 的往返延迟时间。轮询 recv() x2

... 并且哇，就只需要几行代码就可以有很大的差别！并且确认我们需要黑客入侵 linux 调度程序。最终加速约为 10,000ns+ 因此每边 5,000ns（A 接收，B 接收）具有非常不错的小标准偏差-喔耶。

俗话说“轮询是不好的”，会被视为坏程序员，而实际上您应该进行花哨/聪明的操作，因为延迟很小。如果小到 100 微秒，这是一个合理的假设，但在高频交易中 100 微秒并不小。因此，在低延迟环境中，我们要计算纳秒，而且每个核心的周期都不会太小，你应该使用非阻塞轮询套接字循环。也许也应该放弃传统的基于中断的设备驱动程序  :)

... 或者在内核调度程序上进行黑客攻击 哈哈
