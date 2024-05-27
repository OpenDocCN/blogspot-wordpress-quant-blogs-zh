<!--yml

分类：未分类

日期：2024 年 05 月 18 日 13:56:17

-->

# 闪现订单 | 量化投资

> 来源：[`quantivity.wordpress.com/2009/07/25/flash-orders/#0001-01-01`](https://quantivity.wordpress.com/2009/07/25/flash-orders/#0001-01-01)

近期，高频交易（HFT）一直是博客圈（最近甚至是[主流媒体](http://www.nytimes.com/2009/07/24/business/24trading.html?_r=1&scp=1&sq=high%20frequency&st=cse)）热议的话题，由[Tyler Durden](http://zerohedge.blogspot.com/)与约瑟夫·萨卢兹联手展开调查，供给来自[Themis Trading](http://www.themistrading.com)的機構代理經紀方一臂之力。毫无疑问，买方代理经纪人及其他们的[NBBO](http://en.wikipedia.org/wiki/National_best_bid_and_offer)——和[VWAP](http://en.wikipedia.org/wiki/VWAP)挂钩的执行算法正受到高频交易公司的重创。

会引人入胜的发展是来自[Direct Edge](http://www.directedge.com)的 ELP 发起的*闪现订单*。

《Traders Magazine》本月发表了一篇不错的[介绍性文章](http://www.tradersmagazine.com/issues/20_296/-103978-1.html?pg=1)。更有趣的是阅读交易所对闪现订单的实际[FIX](http://www.fixprotocol.org/)支持，因为它们逐渐变得可用。例如，[BATS](http://www.batstrading.com)在 5 月 26 日宣布支持 BOLT 订单（详见[BATS FIX 规范](http://www.batstrading.com/resources/membership/BATS_FIX_Specification.pdf)获取更多细节，如 Page 13 in bold）。对本次讨论相关的是 BOLT 公告中的以下片段（其他交易所也有等效物）：

> 从 BATS 订单簿中去除市场流动性后，BOLT 路由将在路由到交易场外市场之前，首先在 BATS 成员面前暴露订单，暴露时间长达 25 毫秒。BOLT 路由为用户提供了在暴露期间填充订单并在可路由订单上收取每股$0.0015 的回扣的机会，而不是支付标准路由费用。

其中有两个方面是革命性的，后者是接受前者间接“成本”的“奖励”（从接受订单者的角度来看）。

+   先进的知识：订阅专有的 BATS 订单信息反馈的成员可以提前 25 毫秒观察 BOLT 订单路由到交易场外市场的情况，这对其他所有人来说是不可见的（除非订单在目的地发布，或者如果订单由目的地的可用订单簿处理，则永远不可见）。

+   回扣：如果您同意让您的订单闪现，市价订单将获得**回扣**（而不是成本）。

虽然不是合法的[前置交易](http://en.wikipedia.org/wiki/Front_running)，但由于 Reg NMS 报价和限价显示规则（规则[602](http://content.lawyerlinks.com/library/sec/sec_rules/reg_nms/17cfr242_602.htm) / [604](http://content.lawyerlinks.com/library/sec/sec_rules/reg_nms/17cfr242_604.htm)）中 500 毫秒以下的豁免，这确实为 BATS 成员提供了美妙的先行知识。

毋庸置疑，设计一种算法来利用这种预路由可见性是一个有趣的量化式问题。
