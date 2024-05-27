<!--yml

分类：未分类

日期：2024 年 5 月 18 日 06:34:11

-->

# Druid 开源 | 交易台的故事

> 来源：[`mdavey.wordpress.com/2012/10/29/druid-goes-open-source/#0001-01-01`](https://mdavey.wordpress.com/2012/10/29/druid-goes-open-source/#0001-01-01)

## Druid 开源

很有趣看到 MetaMarkets 将 Druid 推向了开源世界。Druid 的历史很有趣，特别是 MetaMarkets 在构建 Druid 之前走过的道路。

对于 Druid 特别好的是分布式内存数据引擎，允许 JavaScript 客户端检索实时数据 – 我 [假设](http://metamarkets.com/platform/) “事件数据可以实时流式传输” [意味着](http://metamarkets.com/2011/node-js-and-the-javascript-age/) 通过 [Node.js](http://metamarkets.com/2012/node-js-for-the-enterprise/) 进行 web 推送。

Druid 特点：

+   **分布式架构。** 使用 MVCC 交换协议的可交换的只读数据段。每个段的复制减轻了热段的负载。支持内存和内存映射版本。

+   **实时摄取。** 实时摄取与代理服务器相结合，可以查询实时和历史数据。随着数据老化，实时数据自动迁移到历史数据。

+   **基于列的速度优化。** 数据按列布局，因此扫描仅限于正在搜索的特定数据。压缩减少了整体数据占用空间。

+   **快速过滤。** 使用 CONCISE 压缩的位图索引。

+   **操作简易性。** 由于复制而容错。支持滚动部署和重启。允许简单地扩展和缩减 – 只需添加或删除节点。

总的来说，从技术角度看，Druid 对于上述所有方面都很有趣，从业务角度看，可能用于实时风险和电子商务销售情报分析和可视化。

~ 由 mdavey 于 2012 年 10 月 29 日发布。

Posted in [JavaScript](https://mdavey.wordpress.com/category/languages/javascript/)
