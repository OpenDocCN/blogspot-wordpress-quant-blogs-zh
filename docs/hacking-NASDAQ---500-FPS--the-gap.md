<!--yml

category: 未分类

date: 2024-05-13 00:06:35

-->

# 以每秒 500 帧的速度黑客入侵纳斯达克：间隙

> 来源：[`hackingnasdaq.blogspot.com/2010/01/gap.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2010/01/gap.html#0001-01-01)

太多软件，太多交换机，太多拨号... 变量太多... 如何使 Linux 系统在这个时间级别上稳定？之前的 UDP 图表是根据上周的测试得出的，所以如果我们使用相同的内核、相同的驱动程序，甚至没有重新启动... 使用 UDP 运行相同的 128B 对战会发生什么呢？

UDP 128B 延迟 A -> B -> A

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhTwtUuF0OMab9b_XIkdO9FLjDGJ3svPxLcU1k3_uZzlaJjZUlTrmfuKNpxypfLcn-xDO9lBFJiUWG_XNrv_CD7MiVAElKt3uMA72n-2NObqR8Y077nUUzR4CA7tLaEzxhbL_kVEh3p-g/s1600-h/tcp_round_default.png)

TCP 128B 延迟 A -> B -> A

... 数字与我们的 7,000ns 差距非常接近，这大致是在 Rx/Ty 处理程序中看到的差异，所以我们正在正确的方向上运行，看起来还不错 - 有点。
