<!--yml

分类：未分类

日期：2024-05-18 05:15:17

-->

# Magmasystems 博客：SQL Server 2005 性能优化提示

> 来源：[`magmasystems.blogspot.com/2006/11/sql-server-2005-performance-tips.html#0001-01-01`](http://magmasystems.blogspot.com/2006/11/sql-server-2005-performance-tips.html#0001-01-01)

[这里](http://www.microsoft.com/technet/prodtechnol/sql/bestpractice/oltp-performance-issues.mspx)

如果你正在进行大量的 OLTP 处理，这些提示对你的性能优化会有好处。大部分的提示也适用于 Sybase。

如果你在 OLTP 系统上进行大量的性能优化，雇佣一个真正的数据库调优专家来细致地审查你的系统是非常值得的。不幸的是，这种调整通常不会涉及到重构数据模型。这是因为许多应用都涉及到数据库的接触，那么你接下来就必须开始重构应用代码。

SQL Server 2005 随带了新的、易于使用的分析工具，我鼓励大家在开发新应用时充分利用它们。如果您是开发经理，一旦您的数据模型编写完成，尝试为 SQL Server 2005 专家的时间争取两周的资助。

此外，尝试让你的 SAN 正确地调整，并优化频繁使用的数据库索引与转子之间的互动。

比如硬件加速，比如固态硬盘呢？

赞誉送给

[这里](http://www.sql-server-performance.com/)

网站，专门致力于 SQL Server 性能优化的地方。

最后一点，如果您有一个涉及大量数据库访问的关键任务型应用，花点钱找一个懂得如何像调整 1964 年 Fender Strat 吉他那样调整数据库的 DB 架构师。

©2006 Marc Adler - 版权所有
