<!--yml
category: 未分类
date: 2024-05-18 06:03:41
-->

# x64 Compute Cluster | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2005/12/21/x64-compute-cluster/#0001-01-01](https://mdavey.wordpress.com/2005/12/21/x64-compute-cluster/#0001-01-01)

## x64 Compute Cluster

It’s curious to see that [Windows Compute Cluster Edition](http://www.microsoft.com/windowsserver2003/ccs/sysreqs.mspx) requires an x64\. I’m not aware of any other grid computing product that forces the same requirements. Unclear why Microsoft has forced this hardware requirement, as it effectively rules out a lot of hardware investment banks might want to use, and seems to only benefit the hardware manufacturers.

Compute Cluster Administrator isn’t too bad. It’s a Microsoft management Console (MMC) 3.0 snap-in which provides node management, To Do list, performance monitoring of nodes (basically a consolidated perfmon view) and remote desktop sessions.

The [Compute Cluster Pack](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/ccpsdk/ccp/microsoft_compute_cluster_pack.asp) has a [COM API](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/ccpsdk/ccp/microsoft_compute_cluster_pack.asp) for job scheduling – no .NET :(.

Keep in mind that Visual Studio 2005 supports [OpenMP](http://msdn2.microsoft.com/en-us/library/tt15eb9t.aspx), whereas Computer Cluster is based on [MPI](http://www.microsoft.com/windowsserver2003/ccs/overview.mspx).

~ by mdavey on December 21, 2005.

Posted in [HPC](https://mdavey.wordpress.com/category/hpc/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)