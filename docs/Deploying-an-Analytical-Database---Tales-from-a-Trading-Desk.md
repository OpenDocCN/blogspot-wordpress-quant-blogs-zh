<!--yml

类别：未分类

日期：2024-05-18 05:29:38

-->

# 部署分析数据库 | 交易台的故事

> 来源：[`mdavey.wordpress.com/2016/09/16/deploying-an-analytical-database/#0001-01-01`](https://mdavey.wordpress.com/2016/09/16/deploying-an-analytical-database/#0001-01-01)

## 部署分析数据库

O’Reilly 有一篇简短但有趣的[文章](https://www.oreilly.com/ideas/5-mistakes-to-avoid-when-deploying-an-analytical-database)，“部署分析数据库时要避免的 5 个错误”。

第一点基本上就是在糖果店里的工程师的情况。在决定技术栈之前停下来思考一下，看看它是否真的有帮助。🙂

从我的角度来看，第四点至关重要。描述这一点的最佳[TLA](https://en.wikipedia.org/wiki/Three-letter_acronym)是与旧的 ETL 世界相比的[ELT](https://en.wikipedia.org/wiki/Extract,_load,_transform)范式。从源系统中提取所有数据元素，并存储在您的分析数据库中。零信息丢失。

由 mdavey 于 2016 年 9 月 16 日发布。

发布在[HPC](https://mdavey.wordpress.com/category/hpc/)中

标签：[大数据](https://mdavey.wordpress.com/tag/bigdata/)，[机器学习](https://mdavey.wordpress.com/tag/machinelearning/)
