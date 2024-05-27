<!--yml

分类：未分类

日期：2024 年 05 月 13 日 00:09:02

-->

# Hacking NASDAQ @ 500 FPS: the book

> 来源：[`hackingnasdaq.blogspot.com/2009/12/book.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2009/12/book.html#0001-01-01)

当订单被分发到市场后，下一步是构建订单簿，即简单地将订单分离和排序为买单/卖单、价格级别和订单号的组合。其结果是买单和卖单价格级别的列表，每个价格级别都有其自己的列表，其中包含该价格的各个订单。虽然这听起来简单，有趣的是订单簿的数量和深度。也许它有 bug，但订单簿的深度大约是我所期望的 1.5-2 个数量级。 2008/11 年的 MSFT 平均有 500 个买单价格级别，1500 个卖单价格级别，同时书上约有 18,000 个订单。左边的情况明显不同，这是我的预期。

所以这是怎么回事？我认为答案是它只显示接近最近执行价格的报价，或一些移动平均 + 标准差，因此订单簿很小。它实际上是什么样子的？这是 MSFT 的买单订单簿，每 10 毫秒采样一次，相当漂亮。

每 10 毫秒采样的买单订单簿。y 轴 $0 -$30

请注意，着色是基于那个时间点的价格级别订单数量。它不是价格级别的交易量，挺不错的吧？有点像地质学。可以看到所有那些蠢货的（近）$0 订单，各种“卖了吧”价格级别（长水平线），以及边缘 - 所有的活动都在那里。

更详细的版本显示从 $18 美元（左下角）开始的价格。每个垂直像素等于 1 美分。不确定水平黑线的含义。假设这是价格级别中的间隙，或是浮点式计算与固定点计算之间的问题......尽管在这个水平上不应该是问题，或者只是我的代码中的一个错误。

来自 $18，1 垂直像素 = $0.01，水平像素 = 10 毫秒

还有... 如果不带卖单的话将会不完整，这是相同的 $0-$30 价格范围。任何 > $30 的价格都被限制在 $30。看待此事的方式有很多，可能是洞穴，或者是日落中的山。令人感兴趣的是比起买单订单簿，卖单的更高价格（长水平线）数量要比买单的更密集。我想这就是 500 对 1500 价格级别的大部分所在。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgUGp3ik73MWJWrpKhA30bepl0z1Eg-XLjKMjhdzsdnPo3Q5KYVppn6ybpTgJdlkQmPt5hm5J_YCEeBvoebjxEVigbIoTOpgJZd0LjWZ4yIBzXEcIWOhrt2GQHVmC65_KB3ewDFk-TWpQ/s1600-h/msft_sell_10ms_0_30.jpg)

卖单纵向刻度[$0，$30] 1 水平像素 = 10 毫秒

还有一个关注边缘的特写 - 令人着迷的东西。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjxlSiOc9AH351-z7mDm-sUbvZazit4saqQnLXfhQ9BJizamBu7Rh4_HvB1Rql7b3zTHUFp29HfiV91u_mGqmKx9ZnHg4X5jiUvc1WdPOVpehIFQJSPIC6miZnJTHQLd_RrxOEgPGX3IQ/s1600-h/msft_sell_10ms_18.jpg)

销售书籍的垂直刻度为 $18，每个垂直像素 = $0.01，水平像素 = 10 毫秒
