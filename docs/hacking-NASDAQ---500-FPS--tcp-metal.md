<!--yml

分类：未分类

日期：2024-05-13 00:05:29

-->

# 黑客 NASDAQ @ 500 FPS：tcp 金属

> 来源：[`hackingnasdaq.blogspot.com/2010/02/tcp-metal.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2010/02/tcp-metal.html#0001-01-01)

快速更新，TCP 金属与 linux 有何不同？我们的 TCP 堆栈还没有完全完成，但已经完成了足够的工作，可以得到某种数量级的数据。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjUenWMNLgfsTdkzcZl_J0nywhLx2EeGgW4Y5Mm7qeuKKoVHP_bIp95S6KmcWuD-fNN2ivFARQaDv82KG5mfGrACRDtnDxgnssWdT0HSvhvC3aOIpthQuMM8N3INDWPjoXsG1nzAiPrzQ/s1600-h/round_tcp_metal.png)

128B TCP 所有金属

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjBkq3zagM53n8CW66Tl1zqCwhg3e8Pc5_wjve8MIb9LcVYr3o5n0G3Mz1GG1dirOjhXDhkGStcEZibX3hJFyAEp4NsaKmjOQ2gwrVz4UHggy_yMeD_C8Opdq3oyr5BWQRbMyC6xhvC0Q/s1600-h/round_tcp_linux.png)

128B TCP 金属->linux->金属

正如你所看到的，我们仅仅在这里击败了 linux，大约有 1-2,000ns 的优势-而且我们甚至还不是一个完整的 tcp 堆栈！肯定不是我预期的，但 linux 确实非常好... 或者我的第一次代码真的很糟糕。所以需要在我们的实现中削减大约 5,000 个 cycles... 事情终于变得有趣起来了。
