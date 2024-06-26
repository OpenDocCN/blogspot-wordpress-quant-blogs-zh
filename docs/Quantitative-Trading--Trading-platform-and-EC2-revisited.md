<!--yml

分类：未分类

日期：2024-05-12 19:02:18

-->

# 量化交易：交易平台和 EC2 再访

> 来源：[`epchan.blogspot.com/2011/11/trading-platform-and-ec2-revisited.html#0001-01-01`](http://epchan.blogspot.com/2011/11/trading-platform-and-ec2-revisited.html#0001-01-01)

最近我开设了一个

[讨论](http://epchan.blogspot.com/2011/09/more-on-automated-trading-platforms.html)

在各种软件平台上，使我们这些程序员能够轻松构建交易策略。这里还有一个新增功能：

[Quantopian](http://www.quantopian.com/)

。它目前处于 alpha 阶段，但我已经预览了其功能：

1) 你可以用 Python 编程，这是一种比 Java 更容易学习的语言，但毫不逊色。事实上，我认识一个出色的程序员，他用 Python 回测高频交易策略。

2) 它是基于网页的，这意味着你可以利用在比你自己桌面更稳定的服务器上托管的优势。（对于那些担心自己策略机密性的朋友，创始人告诉我，他们可以在你拥有的亚马逊 EC2 账户上运行软件镜像，所以他们不会接触到你的代码。至于留在 EC2 上的代码的机密性，请参见下文*。）

3) 它是事件驱动的（或者对于那些喜欢最新术语的人来说：CEP 启用），就像我之前文章中讨论的所有 Java API 一样。

4) 他们为回测提供了 1 分钟的美国股票数据。逐笔数据即将推出。

5) 常见技术指标、数学算法等工具箱即将推出。

6) 他们将举办一个交易模型竞赛，这使得独立交易员更容易成为其他人的交易顾问，或者为他们的基金筹集资金。

不幸的是，现场前进测试尚不可用。

* 一些读者想知道是否安全地在亚马逊的 EC2 上运行他们的交易模型。亚马逊的员工会不会接触到他们盈利丰厚的策略？答案是否定的：亚马逊的**

[安全政策](http://media.amazonwebservices.com/pdf/AWS_Security_Whitepaper.pdf)

：

**客户操作系统：虚拟实例完全由客户控制。客户拥有完整的 root 访问**

**对账户、服务和应用程序的管理控制权。AWS 不拥有任何对客户**

**实例上无法登录到客户操作系统……**

感谢来自法国的读者 OL 提供这些信息。他还告诉我：

所以，我最终在 EC2 的一个 Linux 实例上部署了我的动量策略（顺便说一下，这是免费的）。

我是基于 Interactive Brokers 提供的 java 演示应用程序和 Algoquant 的一些部分编写的。

到目前为止，我使用了一个欧洲实例的 EC2，遗憾的是，它到 IB 美国服务器的延迟（90 毫秒）并不是最好的，但仍然比我的卧室连接要好。

从美国实例到 IB 美国服务器的 ping 测试仅需 15 毫秒……"

所以就这样了：Java+Algoquant+IB+EC2=利润。
