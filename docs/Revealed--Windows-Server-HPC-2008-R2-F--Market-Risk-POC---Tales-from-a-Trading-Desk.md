<!--yml

类别：未分类

日期：2024-05-18 06:13:44

-->

# 揭示：Windows Server HPC 2008 R2 F#市场风险 POC | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2010/04/29/revealed-windows-server-hpc-2008-r2-f-market-risk-poc/#0001-01-01`](https://mdavey.wordpress.com/2010/04/29/revealed-windows-server-hpc-2008-r2-f-market-risk-poc/#0001-01-01)

所以，以下是我最新的概念验证（POC）的全部荣耀。利用我之前博客中提到的所有内容，是时候看看我们是否能够从 Excel [Runner](http://www.theregister.co.uk/2010/04/07/microsoft_hpc_server_r2_beta_2/)HPC 世界迈出步伐了。下面的图表基本上提供了一个高层次的架构，我希望它能提供利用 Windows Server 2008 HPC 计算市场风险的有用指南。

从我模拟的市场（以及市场策略引擎 POC）获取数据，交易将提交到 HPC 集群，其中我几个月前博客中提到的 F#现金流/现值代码将作为服务运行，处理交易并生成现值数字。显然，为了计算现金流，我需要适当的市场数据和曲线。对于这个最初的 POC，我将预先将 AppFabric 缓存填充这些数据，并将速度对象键与交易数据一起传递给 HPC SOA。进一步的 POC 将研究定时更新这些数据，并在特定间隔内更新 Velocity，从而强制重新计算投资组合——现实世界场景。

之前的一篇文章已经讨论过需要 HPC 自定义经纪人的原因，所以我不会再重复。同样，实时立方体（RTC）的设计。然而，每个 HPC 节点上的 VelocityClient 很重要，需要讨论。

集群需要部分无状态和部分有状态。这是为了减少在局域网中传输的数据量，结合将进行的市场风险处理类型。在集群上无状态可能更常见，因为运行作业/服务的进程通常在完成后会被关闭。即使进程没有关闭，也必须考虑到进程因某种原因崩溃的情况。因此，在无状态集群中，所有数据都会发送到每个节点，每次都发送，但这代价昂贵。

我们需要有状态的节点的原因是当我们进入捕捉市场数据/曲线的领域，以及重新计算投资组合时。考虑到我们已经捕捉到了数据，我们知道对于 x 个交易/头寸/投资组合，某些数据将会是相同的。因此，为了减少数据传输的开销，提高性能，我计划在市场风险节点上运行一个[VelocityClient](http://msdn.microsoft.com/en-us/magazine/dd861287.aspx) Windows 服务。这个 Windows 服务将做与服务名称完全相符的事情，作为一个节点的 VelocityCache，拉取特定的一组（可能按货币划分）的市场数据/曲线到节点上持续一段时间，然后刷新服务。如果我们将节点服务进程（F#）无限期地运行，那么我们可以废除 VelocityCache，但是如我之前所说，这不能应对进程崩溃的情况，这是可能发生的 :(。显然，并非所有节点都会缓存相同的市场数据/曲线——如之前的帖子所讨论的。

从高性能计算（HPC）集群中输出的数据将被用来填充实时通讯（RTC，之前的 POC），它也利用了 Windows Server AppFabric 的缓存，从而提供缓存通知，通过流服务器（在这个 POC 中是 Nirvana）实时更新 Silverlight 4 RIA。

我确信这个 HPC 设计中有缺陷，但目前看来是可行的，值得做一个 POC。显然，在完成这个 POC 后，我还有其他一些有趣的想法，其中一些不幸的是依赖于微软让我接触一些新技术 😉

![HPC](https://mdavey.wordpress.com/wp-content/uploads/2010/04/hpc.jpg)

~ mdavey 于 2010 年 4 月 29 日。

发布在[CEP](https://mdavey.wordpress.com/category/hpc/cep/)，[HPC](https://mdavey.wordpress.com/category/hpc/)

标签：[市场风险](https://mdavey.wordpress.com/tag/marketrisk/)，[微软](https://mdavey.wordpress.com/tag/microsoft/)
