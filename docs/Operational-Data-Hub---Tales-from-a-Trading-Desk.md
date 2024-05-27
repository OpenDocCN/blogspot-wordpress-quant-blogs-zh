<!--yml

分类：未分类

日期：2024-05-18 05:31:12

-->

# 运营数据枢纽 | 交易桌面故事

> 来源：[`mdavey.wordpress.com/2016/06/10/operational-data-hub/#0001-01-01`](https://mdavey.wordpress.com/2016/06/10/operational-data-hub/#0001-01-01)

## 运营数据枢纽

虽然有偏爱 [Marklogic](http://www.marklogic.com/blog/eliminate-data-silos-multi-model-database/) 的成分，“用多模型数据库摧毁数据孤岛”提供了一个有趣的视角。几个有趣的收获：

> 新数据仓库项目的 60% 成本用于 ETL，公司每年在创建关系数据孤岛上的花费高达 360 亿美元。

意料之中地，“语义元数据”概念被提出，同时呼吁使用 ELT 替代 ETL。

避免 ETL 地狱的三大方法：

1.  一个基于 [语义](http://www.marklogic.com/what-is-marklogic/features/semantics/) 的三元组存储/仅图形架构

1.  仅文档存储架构

1.  一种结合文档存储和三元组存储的多模型方法

对于第二种方案，“为预期之外的数据结构进行防御性编程”是基于我所见到的真实情况。

同意第三种方案是最佳选择，集两种世界之所长（文档存储和本体论）。并非马克洛根专家，以多种方式出现，似乎这与结合 [MongoDB](https://www.mongodb.com/) 或类似产品与 [D2RQ](http://d2rq.org) 类似？

~ mdavey 于 2016 年 6 月 10 日。

发布于 [数据](https://mdavey.wordpress.com/category/data/) 分类

标签：[本体论](https://mdavey.wordpress.com/tag/ontology/)
