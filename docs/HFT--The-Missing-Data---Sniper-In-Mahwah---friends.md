<!--yml

category: 未分类

date: 2024-05-18 14:20:11

-->

# 高频交易（HFT）：缺失数据 - 马瓦狙击手与朋友们

> 来源：[`sniperinmahwah.wordpress.com/2014/09/19/hft-the-missing-data/#0001-01-01`](https://sniperinmahwah.wordpress.com/2014/09/19/hft-the-missing-data/#0001-01-01)

2013 年 4 月，我参加了伦敦的 Trade Tech Europe 活动 - 这是我首次深入了解高频交易（HFT）的技术世界。我收集了一些[*最优执行*](http://www.bestexecution.net)的副本，因为我对市场微观结构的时空问题感兴趣 – 例如：订单如何在不同位置的交易所/暗池/交叉网络之间路由 – 我发现这篇[paper](http://www.bestexecution.net/viewpoint-darren-toulson-2/)非常引人入胜。

然后我学到了一件事：交易所没有时间同步。这意味着纽约证券交易所（NYSE）的匹配引擎与 BZX 的匹配引擎没有时间同步，EDGX 的匹配引擎与纳斯达克的匹配引擎也没有时间同步，如此类推。这是个问题：在 HFT 世界中微秒就很重要，精确地，不可能完全知道哪个订单何时被填充，使用了哪种订单类型等。因此，学者和投资者都没有精确的数据。数据丢失了。

在这篇以前的文章[post](https://sniperinmahwah.wordpress.com/2014/01/13/about-timestamps-and-exchanges/)中，我谈到了约于 2013 年 12 月在巴黎提出的 McKay Brothers 联席首席执行官 Stéphane Tyč的一个建议。简而言之，该提议是：

*交易所在最重要的匹配周期时产生时间戳。他们还用唯一编号标识每一次匹配的交易。监管机构可以为这些信息定义标准，并强制交易所在结束时刻发布原始数据。每笔匹配的交易都应附上:*

*– 在触发交易的订单时间时的时间戳入口匹配引擎。*

*– 在公开可用数据流中发布交易的时间戳。*

*– 匿名交易 ID 编号。*

*所有时间戳应准确到 PTP（精确时间协议）可轻易获取的 1 微秒的原子时间。这样，所有同步问题都能被非常精确地研究。* 

*这应该在每天结束时以原始市场格式提供。应该提供一个简单的代码来读取这些数据，并且应以开源许可证提供。*

*基于这些信息，任何经纪人的客户都可以收到构成他交易的交易编号集合，并且可以自行找到是否该交易符合其标准。*

*开放数据，开放格式，开放源代码，这些将有助于进一步推动辩论，并使研究能够阐明这个非常具有挑战性的问题。*

令人惊讶的是，在我发布这篇文章之后，我收到了法国金融市场管理局（AMF，法国证券交易委员会）的一封邮件，他们表示他们正在解决同步问题，并希望与我会面，以听取我的观点。看到监管机构对我的观点感兴趣，有点有趣，但我没有太多东西要说，尽管我见过参与这些问题的 AMF 人员，并告诉他们要与**斯特凡·泰克**交谈。他们确实这样做了，通过斯特凡的帮助，他们完善了他们送交欧洲监管机构 ESMA 的关于时间戳同步的提议。我只是一个中间人，在这里仍然是一个中间人。

由于我现在对**斯特凡**已经相当了解（他帮助我理解了一些高频交易中使用的微波网络），他友好地邀请我阅读并评论他正在撰写的关于最佳执行、交易所时间同步等内容的白皮书。虽然我不能称自己为真正的专家，但我认为**斯特凡·泰克**提出的方法是一个非常有趣的方式来公平竞争。以下是这份白皮书：

![最佳执行和过度市场复杂性的技术解决方案](http://www.quincy-data.com/wp-content/uploads/2014/09/Atechsolutiontobestexec.pdf)
