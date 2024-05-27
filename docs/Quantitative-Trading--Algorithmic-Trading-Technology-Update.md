<!--yml

分类：未分类

日期：2024-05-12 19:18:53

-->

# 量化交易：算法交易技术更新

> 来源：[`epchan.blogspot.com/2009/01/algorithmic-trading-technology-update.html#0001-01-01`](http://epchan.blogspot.com/2009/01/algorithmic-trading-technology-update.html#0001-01-01)

最近，一些对算法交易者有用的（至少对我来说）新技术引起了我的注意：

1) Matlab2IB API

我在我的书中说过，使用 Matlab 作为执行平台是困难的。因为

一个叫[Max](http://www.maxdama.com/)的人

指出，这已经不再正确。这个便宜的

[API](http://www.exchangeapi.com/ProductOverview.htm)

连接 Matlab 和你的 Interactive Brokers 账户。它允许你检索历史数据、获取实时报价，以及发送订单。换句话说，所有你创建自己的执行引擎所需的基本功能。

2) R

很多人（致谢：Steve H.）都知道

[R](http://www.nytimes.com/2009/01/07/technology/business-computing/07program.html?partner=permalink&exprod=permalink)

是一个开源的（即免费的）Matlab 替代品。我发现还有一个

[API](http://cran.r-project.org/web/packages/IBrokers/vignettes/IBrokers.pdf)

连接 R 和 Interactive Brokers，尽管我自己还没有尝试过。

3) Trade Ideas

[Trade Ideas](http://www.trade-ideas.com/)

是一个完整的自动化交易平台，提供与不同券商（scottrade, IB, TD Ameritrade 等）的连接

4) 亚马逊 EC2 云计算平台

你的许多策略运行所需的电脑都用完了？试试亚马逊的

[EC2](http://aws.amazon.com/ec2/)

云计算平台。只需支付适度的每小时费用，你就可以访问 Linux 或 Windows 环境的一个实例，并且你可以添加尽可能多的实例。连接速度至少是 T-1 线路的 10 倍，非常适合高频交易。

这里有一个[链接](http://www.maxdama.com/2008/08/amazon-ec2-re-test.html)

是一些其他的性能基准。
