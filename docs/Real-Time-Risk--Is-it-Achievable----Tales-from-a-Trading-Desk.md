<!--yml

分类：未分类

日期：2024-05-18 06:11:21

-->

# 实时风险，这是可行的吗？|交易桌旁的故事

> 来源：[`mdavey.wordpress.com/2009/11/13/realtime-risk-can-it-be-done/#0001-01-01`](https://mdavey.wordpress.com/2009/11/13/realtime-risk-can-it-be-done/#0001-01-01)

## 实时风险，这是可行的吗？

在 Eurostar 上度过数小时会让人思考“事情”。实时风险一直是这些“事情”的一部分。 [Natixis](http://www.quartetfs.com/casestudies/activepivotnatixiscasestudy.pdf)有一个案例研究，提供了如何使用各种产品（包括[Gigaspaces](http://vehera.jsn-server7.com/LiddleBlog/?p=440)）实现实时/日内风险和 P&L 的信息。像大多数问题一样，解决方案要么是完全定制构建，要么是产品或混合型。然而，我怀疑所有实时风险解决方案都需要内存立方体，才能有机会实时提供数据。遗憾的是，Natixis 的案例研究没有提供任何线索，从交易 booking 到交易员桌面上的风险更新之间的延迟。

复杂事件处理（CEP）似乎在实时风险领域也很重要。Aleri [Live](http://www.aleri.com/products/aleri-live-olap) OLAP 是这样一个产品，它提供了[实时](http://www.aleri.com/solutions/capital-markets/real-time-profit-loss) P&L。Aleri 的 CEP 引擎相当不错，但我对他们的 Live OLAP 服务器没有看法。我相信 Aleri 已经有一段时间提供 Live OLAP 产品了，因此很想知道他们是否在过去一年看到了增长。微软可能还想考虑如何定位 StreamInsight，因为 StreamInsight 与[分析服务器](http://www.microsoft.com/sqlserver/2005/en/us/Analysis-Services.aspx)结合在一起，这至少能让他们进入 Aleri Live OLAP 领域。

[Waters](http://www.watersonline.com/public/showPage.html?page=817413)和买方[技术](http://db.riskwaters.com/public/showPage.html?page=867170)有一个有趣的观点；“尽管实时风险管理在理论上仍然只是可能的，但自从 2 月底以来，供应商看到这一领域的兴趣大幅增加。希望采用这种风险计算的公司大多是大型和中型银行。”

~ mdavey 于 2009 年 11 月 13 日。

发布在[交易](https://mdavey.wordpress.com/category/trading/)

标签：[Microsoft](https://mdavey.wordpress.com/tag/microsoft/)
