<!--yml

类别：未分类

日期：2024 年 05 月 13 日 00:07:59

-->

# 在 500 FPS 下黑客纳斯达克：向英特尔致敬

> 来源：[`hackingnasdaq.blogspot.com/2009/12/rock-on-intel.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2009/12/rock-on-intel.html#0001-01-01)

好了，现在新年的狂欢已经结束了，让我们回归正轨。首先，新的英特尔网卡被放入了 Machine B，所以我们现在

Machine A（英特尔 82573L）Xeon 2.6Ghz

Machine B（英特尔 82574L）i7 2.6Ghz

因此，Machine A 在 CPU 和 NIC 方面比 Machine B 落后一两代，但这就是我们要处理的情况。

首先是发送直方图，在 A 到 B 方向和 B 到 A 方向

Machine A 发送

Machine B 发送

正如你所见，Machine B 以大约 5-600ns 的速度击败了 Machine A。其中有多少是 NIC 生成的，有多少是 CPU 生成的还不清楚，毫无疑问，两者都在起作用。

另一边，收到首先 B 到 A，然后 A 到 B 看起来如下（以下）

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg7afBInegnJreMFQZ5SB1VfMU8FjvSpb_nCL-QuGb0_0Rg_cRDvLrfYG_LJKvr-xAMNcwTce3_P_n6txx7faknOqmszzXw8OALWR-eYJ8bXh4S5PMk-iIJfEMx1jQQ4eiL6oHvy0yFTw/s1600-h/recv_latency_82573.png)

Machine A 收到

Machine B 收到

再次，我们看到 Machine B 几乎是 Machine A 的两倍提高，但并非完全达到两倍！无论如何，它看起来比 Realtek 的直方图要好得多，那些......实在是糟糕，而且我们现在有了一个基准线来工作。

接下来要看的是来回延迟，即 A->B->A，假设网络交换机没问题（不会太多......它旧了），我们应该期望约 1300ns（A 发送）+ 500ns（B 收到）+ 750ns（B 发送）+ 900ns（A 收到）总计...约 3450ns 来回延迟 - 真的是相当长的时间。

让我们看看它的性能如何。
