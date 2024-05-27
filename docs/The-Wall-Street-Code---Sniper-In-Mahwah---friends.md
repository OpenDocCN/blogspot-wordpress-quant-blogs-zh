<!--yml

分类：未分类

日期：2024-05-18 14:25:08

-->

# 《华尔街代码》——Sniper In Mahwah &朋友们

> 来源：[`sniperinmahwah.wordpress.com/2013/11/05/the-wall-street-code/#0001-01-01`](https://sniperinmahwah.wordpress.com/2013/11/05/the-wall-street-code/#0001-01-01)

《华尔街代码》昨晚以荷兰语在荷兰 VRPO 频道播出，现在英文版可在 YouTube 频道[VPROinternational](http://www.youtube.com/user/VPROinternational)上找到。这是 Marije Meerman 继 2010 年的《量化：华尔街的炼金术士》和 2012 年的《金钱与速度：黑箱之内》之后，关于金融市场的第三部纪录片。《华尔街代码》可以说是《金钱与速度》的续集，因为主要讨论的是高频交易和算法代码，这些代码让某些股票交易订单“超越”其他订单，从而能够以更高的价格向传统投资者出售几微秒前购买的股票，同时在这些投资者的订单簿上赚取双倍。

《华尔街代码》*聚集了一批相当有趣的参与者，到目前为止他们在银幕上出现的次数并不多（如果排除掉在《金钱与速度》中已经出现的 Nanex 的 Eric Hunsader）。因此，我们看到了资深人士 Thomas Peterffy，在康涅狄格州的家中被拍摄，回顾了他于 1980 年代末为纳斯达克终端设计的著名机器人，该机器人在纪录片中短暂出现：*

![](https://sniperinmahwah.wordpress.com/wp-content/uploads/2013/11/capture-d_c3a9cran-2013-11-05-c3a0-08-22-32.png)

© VPRO，《华尔街代码》片段

最生动的时刻可能是当 Peterffy 拿出他那著名的触控板——我在*[6](http://www.zones-sensibles.org/index.php?mod=auteurs&a=06)*中谈到过的——为美国股票交易所于 1983 年制造的。这是第一次在银幕上看到这款 iPad 的前身：*

*![](https://sniperinmahwah.wordpress.com/wp-content/uploads/2013/11/capture-d_c3a9cran-2013-11-05-c3a0-07-24-23.png)

© VPRO，《华尔街代码》片段

“*其他人用他们的头脑*”，彼得菲用他的匈牙利口音笑着展示他的机器。他重申了对市场公平的执着，以及分享代码的重要性，以便所有参与者都能在平等的基础上 - 这与高盛的做法截然相反，后者在 Sergey Aleykinov 事件中[暴露](http://www.vanityfair.com/business/2013/09/michael-lewis-goldman-sachs-programmer)从开源代码中获益，同时修改并声称拥有修改权，这显然违反了开源的伦理。

（偶然还是必然？就在纪录片播出前夕，此处提到的博客首次迎来了 Interactive Brokers LLC 的访问……

![2013-11-05 屏幕截图](https://sniperinmahwah.wordpress.com/wp-content/uploads/2013/11/capture-d_c3a9cran-2013-11-05-c3a0-07-51-45.png)

……碰巧是托马斯·彼得菲的公司。

高盛确实有所涉及，因为*华尔街代码*长时间采访了 Haim Bodek，一位前交易开发者，Scott Patterson（在纪录片中接受采访的《华尔街日报》记者）在*黑暗水池*中讲述了他的故事（Bodek，如今反对高频交易者，在交易订单变革方面发表了[一些非常有趣的论文](http://haimbodek.com/research.html)）。Bodek 和他的编程同事们的最后画面，他们成立了一个对冲基金，有点像冰岛的氛围……但这是 20 年后。

Haim Bodek 还曾在另一位高频交易老兵（芝加哥人）Blair Hull 的公司工作过，Hull Trading Company 后来被高盛以 4.8 亿美元收购（高盛最初想购买托马斯·彼得菲的公司，但被拒绝了）。我在[*5*](http://www.zones-sensibles.org/index.php?mod=auteurs&a=08)中详细介绍了 Blair Hull 的职业生涯，他的职业生涯始于拉斯维加斯，然后在 1980 年代的芝加哥商品交易所取得了辉煌成就。Hull 在*华尔街代码*中透露了一些关于那个时代的有趣细节，并公正地强调市场电子化的复杂性主要源于监管机构制定的规则。

电影中最引人注目的时刻之一可能是当 Dave Lauer（前高盛和 Citadel 员工）提到 2010 年 5 月 6 日的“闪电崩盘”，以及当天的曲线图 literally 从控制屏幕上跳出来。当然，也谈到了高频信息传输的链条，特别是从芝加哥（Nanex 对 Aurora 的 *data center* 进行了短暂的外部参观）到新泽西州，纳斯达克在 Carteret 设立：

![芝加哥-纽约](https://sniperinmahwah.wordpress.com/wp-content/uploads/2013/11/capture-d_c3a9cran-2013-11-05-c3a0-07-39-47.png)

© VPRO，摘自“华尔街代码”

正如高频交易中常有的情况，就传输时间而言，很难准点：电影中提到的 4.2 毫秒现在已经过时了，因为昨天我们了解到[ McKayBrothers & Quincy Data](http://www.hftreview.com/pg/blog/mike/read/127139/market-data-at-the-speed-of-light)使得 CME/CBOT 和 Nasdaq 之间的传输时间现在只需要 4.09 毫秒（比真空中光速还要慢 0.14 毫秒），从机架到机架（即从算法到算法）。

每个人对*华尔街代码*的质量评价可能都不一样，这个节目只覆盖了高频交易相关问题的一小部分（并且这部分内容带有偏见），最有趣的部分可能是 Bodek 关于机器引起的订单复杂性的讨论（我将来会回来讨论这个问题），这种复杂性本可以在时空角度上进一步突出。在深入*华尔街代码*之前，观看之前的纪录片*金钱与速度*可能是有用的。最后，值得注意的是，目前法国正在制作关于高频交易的三个纪录片。
