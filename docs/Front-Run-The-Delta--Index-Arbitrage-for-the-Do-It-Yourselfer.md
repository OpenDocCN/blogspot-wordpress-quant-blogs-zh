<!--yml

类别: 未分类

日期：2024-05-12 23:37:18

-->

# 预先获取列标 3：自助型指数套利

> 来源：[`frontrunthedelta.blogspot.com/2011/06/index-arbitrage-for-do-it-yourselfer.html#0001-01-01`](https://frontrunthedelta.blogspot.com/2011/06/index-arbitrage-for-do-it-yourselfer.html#0001-01-01)

这是用于构建伪-

[指数套利](http://en.wikipedia.org/wiki/Index_arbitrage)

(类似于

[一对对冲](http://www.efinancialnews.com/story/2011-06-10/delta-one-nomura)

) 模型

[SPDR 道琼斯工业 ETF](https://www.spdrs.com/product/fund.seam?ticker=dia)

相对于在 CBOT 上列出的一个靠前月份

[迷你道琼斯工业指数期货](http://www.cmegroup.com/trading/equity-index/us-index/e-mini-dow_contract_specifications.html)

期货合同。我们的软件是自主的，并且是从零开始开发的（不是由我开发）。我们目前使用

[IB 的 TWS](http://www.interactivebrokers.com/ibg/main.php)

作为我们进入市场的媒介。这就是我的化学试验。

**构建利差点。**

步骤 1：定义您的基础。给你的系列命名。在这种情况下，我们命名文件为 “DIA_YM”。 “t13,t14” 对应于左侧带有开放连接的两个变量。 t01 到 t12 是软件当前引用的其他证券。

步骤 2：输入您选择的 “专有” 算法。如图所示，目前在 e01 到 e06 的框中模糊显示（抱歉，不能全部透露）。

步骤 3：点击 LiveTrack(c)！

步骤 4：等待几分钟并取一份数据样本。这是 DIA/YM 对的非常高频、同步交易和报价数据。同步化（讨论

[这里](http://rogerenright.blogspot.com/2011/06/triangular-arbitrage-using-usdhkd.html)

) 意思是，当任何预定义的变量（出价，出价大小等）发生变化时，整个集合的快照会被拍摄下来，并且时间戳精确到毫秒。

[,](http://en.wikipedia.org/wiki/Serial_comma)

并记录。

步骤 5：最后，检查结果。2 分钟 13 秒的睡前交易中，共有 159 个变量发生变化。
