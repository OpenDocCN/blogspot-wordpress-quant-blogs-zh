<!--yml

分类: 未分类

日期: 2024-05-13 00:06:22

-->

# 利用 FPS @ 500: TCP Rx 处理

> 来源: [`hackingnasdaq.blogspot.com/2010/01/tcp-rx-processing.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2010/01/tcp-rx-processing.html#0001-01-01)

之前的帖子在更宏观的层面查看了事物，所以让我们深入一点到栈中去找出发生了什么。我们分析了驱动程序 / IP / TCP / 用户进行了拆分，我们得到了下面的结果

TCP 128B 往返总时间

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhZ37UGr46X26bvickQPyTTT1JFSXTm_2P3wuolxhwOp8evfZykRZigl8IpBOeKrdrWH26sVV_4vpw9U32WPgUmzk7RvcvWE1El-nWBvhe6K2jGY4hzSIaI13OsHT2lgPLvR_05hBheYQ/s1600-h/tcp_Rx.png)

NIC 驱动程序时间

IP 处理时间

![](http://3.bp.blogspot.com/_wI0x7e0fUck/S1hzAPxgaMI/AAAAAAAAASk/nXr8cDOS-5s/s1600-h/tcp_TCP_Total.png)

TCP 处理时间

内核 -> 用户 切换

这是预期的结果，TCP 处理时间成为瓶颈，但它实际上在做什么？再深入挖掘一下，我们得到:

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgcUoWR-k5TM0Psdbo3Xa_W7A3fvcSe0DXeCiVu5KpcwSJg2tC81r832AkIwywKIh891li0JeNpp1Z4N2QWnXLm5WXvy2YyldEv2ibJDvL_mKe8XcbipWZWhZBTYH3meOuyIfTD0iuNvQ/s1600-h/tcp_TCP_Top.png)

TCP 顶层处理 + 预排队

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEje8TlXa2BBOpLZTkm-9Ut4FRSzdbZR1IJwjo6vCurdqubXfOFFpfWfc53Ec54ptedH4iP0Xh0gxc5AaYc9XPRxGNsFXiMBRSkdwrUFDLGhXZWitzdu8Cxa8HvZ4yx7XRihv5zVj1S9OQ/s1600-h/tcp_TCP_Recv.png)

TCP tcp_rcv_established()

相当令人惊讶的是，看起来 tcp_v4_rcv() 中的顶层处理是大部分时间的去处！这不是你预期的 tcp_rcv_established() 是主要的工作代码所在。然而…情况变得更奇怪。

TCP 预排队之前 -> tcp_rcv_establish()

结果显示，大多数时间都消耗在将数据包推送到 tcp 预排队和实际在 tcp_rcv_established() 中处理数据包之间。我不确定那儿发生了什么，但令人惊讶的是，那才是所有活动的发生地。
