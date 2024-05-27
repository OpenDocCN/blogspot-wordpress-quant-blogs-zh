<!--yml

分类：未分类

日期：2024-05-18 05:46:11

-->

# 状态复制 | 交易桌旁的故事

> 来源：[`mdavey.wordpress.com/2014/09/30/state-replication/#0001-01-01`](https://mdavey.wordpress.com/2014/09/30/state-replication/#0001-01-01)

## 状态复制

一位同事向我推荐了几篇有趣的文章（[Replicant](http://hackingdistributed.com/2013/12/26/introducing-replicant/)），它们围绕状态复制展开。长期以来，我一直对状态复制感兴趣——在过去的几年里，我曾在不同的博客上写过关于它的内容。每个复制品都能够接受变化，并将变化传播到所有复制品以确保一致性，这是一个有趣的问题。这样的解决方案在分布式应用中提供了有趣的可扩展性选项。

[孟子](http://sysnet.ucsd.edu/~yamao/pub/mencius-osdi.pdf) 提供了我更感兴趣的内容——单/多领导者

作者：mdavey 日期：2014 年 9 月 30 日。

发布于 [未分类](https://mdavey.wordpress.com/category/uncategorized/)
