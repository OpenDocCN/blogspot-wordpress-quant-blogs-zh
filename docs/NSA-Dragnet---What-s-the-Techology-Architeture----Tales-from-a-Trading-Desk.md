<!--yml

分类：未分类

日期：2024-05-18 06:02:58

-->

# NSA 大规模搜索——技术架构 | 交易桌面故事

> 来源：[`mdavey.wordpress.com/2013/08/11/nsa-dragnet-whats-the-techology-architeture/#0001-01-01`](https://mdavey.wordpress.com/2013/08/11/nsa-dragnet-whats-the-techology-architeture/#0001-01-01)

## NSA 大规模搜索——技术架构是什么？

我们中的大多数人可能已经读过一些关于斯诺登和国家安全局（NSA）数据收集的内容。美国公民自由联盟（ACLU）最近的[文章](http://www.aclu.org/blog/national-security/guide-what-we-now-know-about-nsas-dragnet-searches-your-communications)，"了解国家安全局对你通信的大规模搜索"，提供了通常的高级视图，包括 NSA 可以使用的数据收集、分析和搜索功能。像可能的其他许多软件工程师一样，我对使用的架构和技术感到好奇，具体是数据存储，实时处理与离线处理相比如何等等。

仅基于 ACLU 的文章，我们可以做出以下（错误的）假设：

+   假设网络嗅探是数据收集的来源之一，根据 X-KEYSCORE 的“位置”幻灯片，听起来数据在其收集地本地存储。

+   通过 UpStream 电缆嗅探进行数据收集，我会假设这会打破数据，包括内容和元数据（IP 地址、电子邮件地址、关键词等），并存储数据以进行进一步处理，或仅用于搜索检索。

+   PRISM 数据收集听起来更像是一个应用嗅探，如前两点所述，路由到基础设施中。再次不清楚 PRISM 的数据存储是否每个 PRISM 嗅探本地，还是回到一个单一的数据仓库。

+   你可以看到像[hadoop](http://hadoop.apache.org/)这样的开源社区的类似技术如何帮助 NSA 处理收集的数据。然而，跨越多个位于全球的数据中心会带来一些延迟。

+   “监听任何人，从你或你的会计师”应该不会因为 NSA 有明确的应用和网络嗅探而感到震惊，实际上，这是一种[连续查询](http://coherence.oracle.com/display/COH31UG/Continuous+Query)针对 NSA 的数据源，以获取所需数据的实时视图。

以上内容基于我刚刚下飞机的航班，但我很好奇，是否阅读此博客的任何人都找到了关于 NSA 处理“大数据”问题的假设技术 further writing

~ mdavey 于 2013 年 8 月 11 日。

发布在[未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签：[大数据](https://mdavey.wordpress.com/tag/bigdata/)，[NSA](https://mdavey.wordpress.com/tag/nsa/)
