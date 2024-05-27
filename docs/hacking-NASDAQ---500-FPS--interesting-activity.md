<!--yml

类别：未分类

日期：2024 年 05 月 13 日 00：09：18

-->

# 以 500FPS 黑客 NASDAQ：有趣的活动

> 来源：[`hackingnasdaq.blogspot.com/2009/12/interesting-activity.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2009/12/interesting-activity.html#0001-01-01)

上一篇帖子是随机选择的市场片段，有时有趣，有时没有。好奇的是，当天最高订单率是什么情况，结果是...就在市场开盘后的第 30 秒左右。大约有 10k（主要是新增）订单以非常有趣的模式放置在订单簿上。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjNUQb4wnZ78rAeEy0-f9wAhELFbIR-d8lPYGhQcpLPgBkoLSoEpu-8JkVOy9IUtJ83Uu6PmYDcEy6rpFOY2ySJE4P9xzC87CpXKVkoPdwLQZOJ9zf1jj21JvBp8-kNCVXqDAVSxsA09w/s1600-h/msft_stack1ms_marketopen.png)

正如你所看到的，这里有一系列的订单，然后突然变得平稳。非常奇怪的是，每个 1ms 片段内的订单数从未超过 100 个-再次检查了数据，因为这是一个高度人为的模式。那么这里到底发生了什么？我的猜测是，由于几乎完全是新增订单，这是交易所软件的一个人为现象。例如，在交易所开张时，所有参与者同时发送他们的订单，这些订单在交易所排队，并以每 1ms 100 个订单/的有限速度处理，或者每秒 100k 个/（假设是每个符号）。一旦每个人的初始订单都放置好，一切就会稳定下来，就像往常一样。结论是什么？很可能如果你向交易所灌输> 100 个订单/ 1ms，它会严重阻塞，所以也许你可以减缓竞争对手的订单。

第二个有趣的点有点让人扫兴，是在当天执行订单数量最多的一段时间，结果是就在 6H 之后的时间。

1 水平=1ms

没什么特别有趣的东西。2 个巨大的波峰，然后是一大片活动。记住，这是#执行的订单，而不是交易量。所以对于 1ms 的时间片来说，这是很多的活动，也许是一些大型愚蠢的算法大量吸收了一部分订单？接着是监视算法认为会发生某些更大的事情。但...目前只是猜测。
