<!--yml

类别：未分类

日期：2024-05-18 06:19:10

-->

# 微软堆栈实时风险解决方案？ | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2009/11/29/microsoft-stack-real-time-risk-solution/#0001-01-01`](https://mdavey.wordpress.com/2009/11/29/microsoft-stack-real-time-risk-solution/#0001-01-01)

## 微软堆栈实时风险解决方案？

在实时风险领域似乎有很多机会。对于像微软这样的公司，他们可能想要获得金融垂直领域的很大一部分份额，目前还不清楚他们是否理解这个问题或者是否有解决方案。如果你看看我最近博客上提到的那些实时风险产品公司，有许多竞争者可能会或可能不会被银行在接下来一年左右的时间里构建的解决方案所采用。不幸的是，我认为在这个产品领域还没有明确的赢家，似乎没有一个产品能解决 80%的问题。

如果我们看看问题领域，我们知道我们需要处理大量的动态数据（交易、市场等），我们需要绘制曲线，实时计算交易/头寸风险，最后我们需要以适当的方式展示这些数据，并允许深入钻取和分析数据——[利润与损失（P&L）归因](http://pnlexplained.com/PEP_PnL_Explained_FAQ.html)。

所以现在我们转向微软，以及它能为解决这个问题提供什么。今天它有[分析服务](http://www.microsoft.com/sqlserver/2005/en/us/Analysis-Services.aspx)，提供 OLAP 但不是向量数据库，而且我认为它对桌面来说不够实时 😦 然而，我认为如果愿意尝试一个证明概念（POC）的一部分，可能是解决方案的一部分：采用 StreamInsight，可能使用[Dryad](http://blogs.technet.com/windowshpc/archive/2009/07/15/dryad-and-dryadlinq-on-hpc-server.aspx)连接到 HPC，将 Windows Server AppFabric 缓存用于交易/风险数据，并可能考虑构建一个[内存中](http://it.toolbox.com/blogs/crm-realms/inmemory-olap-vs-traditional-olap-27467)的 cube，这个 cube 基于通过 Silverlight/WPF 应用程序呈现的分布式数据集构建——本质上是在 AppFabric 缓存之上构建[StreamCube](http://www.panopticon.com/products/streamcube_olap_data_visualization.htm)。

托斯滕在 2009 年 PDC 会议上的 session 提供了一些关于如何在实时风险（RTR）架构中使用 StreamInsight 的见解。尽管他的市场推动者演示没有聚合风险，但它确实展示了如何使用多层 StreamInsight 架构——在会议的第 41 分钟。我怀疑你希望将 SQL Server 2008 Analysis Services（OLAP）数据库也喂给那些绿色 StreamInsight 服务器，以便进行 MDX 即席查询，第三层处理客户端应用程序请求以根据动态查询推动 RTR 数据。我认为会议的第 46 分钟提供了一个很好的 RTR 视角。

~ mdavey 于 2009 年 11 月 29 日。

发布在[交易](https://mdavey.wordpress.com/category/trading/)

标签：[微软](https://mdavey.wordpress.com/tag/microsoft/)
