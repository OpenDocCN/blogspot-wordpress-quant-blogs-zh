<!--yml

类别：未分类

日期：2024-05-18 06:03:41

-->

# x64 计算集群 | 交易台的故事

> 来源：[`mdavey.wordpress.com/2005/12/21/x64-compute-cluster/#0001-01-01`](https://mdavey.wordpress.com/2005/12/21/x64-compute-cluster/#0001-01-01)

## x64 计算集群

有趣的是，[Windows 计算集群版](http://www.microsoft.com/windowsserver2003/ccs/sysreqs.mspx) 需要 x64\. 我不清楚是否还有其他要求相同的网格计算产品。微软为什么要强制这个硬件要求，因为这实际上排除了许多投资银行可能想要使用的硬件，并且似乎只有硬件制造商受益。

计算集群管理员并不算太糟糕。这是一个 Microsoft 管理控制台（MMC）3.0 的插件，提供节点管理、待办事项列表、节点的性能监控（基本上是一个合并的 perfmon 视图）和远程桌面会话。

[计算集群包](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/ccpsdk/ccp/microsoft_compute_cluster_pack.asp) 有一个用于作业调度的 [COM API](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/ccpsdk/ccp/microsoft_compute_cluster_pack.asp) - 没有 .NET :(。

请记住，Visual Studio 2005 支持 [OpenMP](http://msdn2.microsoft.com/en-us/library/tt15eb9t.aspx)，而计算集群基于 [MPI](http://www.microsoft.com/windowsserver2003/ccs/overview.mspx)。

~ by mdavey on December 21, 2005.

发表在 [HPC](https://mdavey.wordpress.com/category/hpc/) 中

标签：[微软](https://mdavey.wordpress.com/tag/microsoft/)
