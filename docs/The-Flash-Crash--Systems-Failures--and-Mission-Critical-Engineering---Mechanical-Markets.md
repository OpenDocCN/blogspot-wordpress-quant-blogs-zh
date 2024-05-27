<!--yml

category: 未分类

date: 2024-05-18 06:43:23

-->

# The Flash Crash, Systems Failures, and Mission-Critical Engineering | 机械市场

> 来源：[`mechanicalmarkets.wordpress.com/2015/05/06/flash-crash-systems-failures-mission-critical-engineering/#0001-01-01`](https://mechanicalmarkets.wordpress.com/2015/05/06/flash-crash-systems-failures-mission-critical-engineering/#0001-01-01)

闪崩是由不同的 IT 系统之间的复杂相互作用引起的。其中一些系统以不优雅的方式失败，而其他系统则无法应对这些失败。我希望我们不是仅仅对计算机现在如何管理我们的交易基础设施表示担忧，而是花时间理解计算机管理的系统比我们的金融市场要* mission-critical*得多。

我一直在从事交易系统的工作，并认识到稳定市场的重要性。我认为任何连接到市场的软件都应该有多个独立的安全检查层。事实上，我会主张我们有*现在*更大的风险检查。[算法交易公司很清楚](http://www.reuters.com/article/2012/10/17/us-knightcapital-results-idUSBRE89G0HI20121017)如果他们的安全措施失败会发生什么。但是，对高频交易(HFT)和交易所来说，最糟糕的事情通常是破产。 [1]

确实，普通投资者可能会在 IT 故障中受到损失，但希望在这些情况下错误的交易可以被撤销。同样真实的是，交易员非法相互操纵市场*操纵市场*，可能会欺诈无辜的投资者。鉴于闪崩的惊人系统故障，值得我们反思与生活中其他领域的拙劣自动化相关的风险。我甚至无法开始详述我们过去 50 年中遇到的所有的严重的 IT 故障，但以下是一些（无特定顺序）使得闪崩看起来微不足道的事故：

1.  2003 年东北大停电。[复杂的事件间相互作用，包括软件故障，导致超过 5000 万人断电，*造成许多死亡*](http://www.reuters.com/article/2012/01/27/us-blackout-newyork-idUSTRE80Q07G20120127)。

1.  [Therac-25 放射治疗设备](http://courses.cs.vt.edu/professionalism/Therac_25/Therac_1.html)。据称，这款设备存在缺陷的软件安全保障导致了至少 6 名癌症患者接受了致命或几乎致命的辐射剂量。

1.  包括某些[凯迪拉克](http://www.zdnet.com/article/cadillacs-recalled-over-software-bug/)在内的汽车安全气囊部署控制软件的问题。

1.  2014 年比利时选举中电子投票存在问题[。](https://joinup.ec.europa.eu/community/osor/news/bug-belgian-voting-machine-should-have-been-found)大约有 2000 名选民受到影响，但我猜测受到闪电崩盘影响的交易员人数可能不到这个数字。

1.  臭名昭著的丰田“非预期加速”[问题](http://abcnews.go.com/Blotter/toyota-pay-12b-hiding-deadly-unintended-acceleration/story?id=22972214&singlePage=true)可能是由有缺陷的软件引起的，[一些专家](http://betterembsw.blogspot.com/2014/09/a-case-study-of-toyota-unintended.html)表示，这个问题已经导致了数十人死亡。

1.  一颗苏联卫星的软件缺陷[据报道](http://www.washingtonpost.com/wp-srv/inatl/longterm/coldwar/shatter021099b.htm)触发了警报，称美国发射了 5 枚洲际弹道导弹。幸运的是，人类操作员怀疑这是一次误报，在启动雷达确认发射之前没有作出反应。

这远非一个完整的列表，而且我们通常甚至不知道是否有错误的 IT 技术 contributed to a [fatal accident](http://news.bbc.co.uk/2/hi/uk/8438659.stm)。我认为许多金融专业人士都受到[职业病](http://en.wikipedia.org/wiki/D%C3%A9formation_professionnelle)的影响。[2]的事实是，尽管闪电崩盘引起了轩然大波，但在大局来看，它几乎没有造成什么严重的后果。

闪电崩盘非常短暂地导致[大约 1 万亿美元](http://graphics.wsj.com/flash-crash-timeline/)的证券市值损失。这也触发了一场媒体风暴，这可能使一些零售投资者持有现金，并错过了危机后的股市复苏。对于那天亏钱的活跃交易员来说，毫无疑问，闪电崩盘是一件大事。但现实是，市场在几分钟内就恢复了，许多荒谬价值的意外交易也被取消了。闪电崩盘在今天至少在美国股票市场发生的可能性也要小得多，因为我们有了在市场波动性足够大时暂停交易的熔断机制。

随着计算机系统的日益普及，我希望我们能从闪电崩盘中吸取一些教训。与交易所不同，生命关键系统的设计者们在检测到问题时，没有关闭系统几分钟的奢侈。金融市场电子基础设施无法承受一点压力固然令人沮丧，但幸运的是，这样的事故吸引了媒体的关注，而没有造成任何生命的损失。闪电崩盘的周年纪念日提醒我们，所有关键系统都需要智能监管，最重要的是，这是向保持我们安全的工程师表示感谢的机会。

1 对于高频交易（HFT）公司来说，一些交易员违反合规规定并犯罪可能是更糟糕的事情。但我不会真的称这为 IT 故障，尽管随着合规性[日益自动化](http://www.bloombergview.com/articles/2015-04-08/algorithms-will-make-jpmorgan-less-bad)，也许有一天情况会改变。

2 我寻找过这个术语的英文对等词，最接近的我发现是“职业心理障碍”，这听起来比我希望的要更极端一些。
