<!--yml

category: 未分类

date: 2024-05-13 00:06:59

-->

# hackers 在 500 FPS 下的 NASDAQ：内核调度程序

> 来源：[`hackingnasdaq.blogspot.com/2010/01/kernel-scheduler.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2010/01/kernel-scheduler.html#0001-01-01)

Rx -> recvfrom() 中的双峰看起来有点可疑，特别是内核 -> 用户空间的切换，这看起来像某种核/硬件交互。那么，如果我们改变核心数量会发生什么呢？这做起来很简单，只需要将 maxcpus=0 添加到内核引导命令中。于是生成了以下图表

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj_y8QiV_4GJCXfUQpXuiw1Rexij9F-eXyHKFAx0YYe4wFBZE61zqGJoG0O-mVG_-gCyWNkX_O84_YrYidD1JiLTUnto7cSPYRMCDZNVkW4SScSZbeNwv-tPwjFBpojGWjbkEL_MWTQVA/s1600-h/cpu2_2_send.png)

2 核心 sendto() -> Tx Desc

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjf6c2RM_fMKYNT5DrPZD9d-2aQlnfZfWSLTBGUY-xgww6XTYoCA-XboC_9LKBlyZmzH9a6cT2c4eD9VYFlAMdDZEpT6P2Uoj3v7ClochHRb-NaluKys5vFKOj9d0WNPrdEAPjvJphvbQ/s1600-h/cpu1_2_send.png)

1 核心 sendto() -> Tx Desc

这有点有趣，不太确定为什么 1 核心 sendto() 具有很多 < 1,000ns 的采样点，而 2 核心版本则一个没有，除此之外并没有什么激动人心的事情。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg9aTngKHtLqtcMoY0LLR9AT2yDX3uwQe9H4-fcSG4HHJwpyzfCGGpd_JDEeG5Xg6dh2zHOmtwzJKeh6KkafPDWgoWQmjHYqITMMTIXrY8eGruJ0nTDLlGKY_gcTi9i2DC5r_uWrkdIFQ/s1600-h/cpu2_3_recv.png)

2 核心 Rx 间断 -> recvfrom()

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgY0LzPCCxW11uHj5RtgFYGzTNBTdM6QWbm7BfABAYpW4zqisagIhqtkOzzH-No6rxamCwhTuVNkIbof__62j_ZFS_YVBnJz9wldlts1_7YgCuOgLPMsmfUZQ1BVmD2_i1MUSbaEhWAlA/s1600-h/cpu1_2_recv.png)

1 核心 Rx 间断 -> recvfrom()

另一方面，接收显示出相当大的改变，正如我们所怀疑的，它从双峰变为单峰，假定为内核 -> 用户空间的信号行为。而 ...

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEinoDiuMGFZP8tD7ai03fmrUkc9ej4eDYrHa7kuB9PiTSjZ9h1pGZp-8PcwO4at2G8JoLXMSkp9p240Vw7lXmkL0UrbZnrpzcPAf-a9X2pQrcB4Y6V3Ha80tONlLS7qiNCHq4itFMr3dA/s1600-h/recv_2core.png)

2 核心 udp 完成内核空间 -> 用户空间 recvfrom()

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiZTx-0auRPLn1p1P_kJAnlhpNZrvSlqUmzvPgaQVRU7XKztMdGI2staWqSXxEOCnJ90ntH5IuuYJps7N8_CqBFRXXrRUfnVefWhZRaiJg7CMhCmGKuOND5qSuG4-VImAWYFlw6UfxoHw/s1600-h/recv_1core.png)

1 核心 udp 完成内核空间 -> 用户空间 recvfrom()

...这些图表说明了问题。奇怪的是，在某些情况下，增加核心会增加延迟（第二个峰值）。不知道出了什么问题，但请记住这是一个阻塞的 recvfrom()调用，显然与 Linux 调度程序处理信号有关。
