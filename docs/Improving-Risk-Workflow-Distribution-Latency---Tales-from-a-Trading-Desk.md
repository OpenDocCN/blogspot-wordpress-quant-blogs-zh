<!--yml

类别：未分类

日期：2024-05-18 06:03:24

-->

# 改善风险工作流分布延迟 | 交易桌旁的故事

> 来源：[`mdavey.wordpress.com/2013/08/05/improving-risk-workflow-distribution-latency/#0001-01-01`](https://mdavey.wordpress.com/2013/08/05/improving-risk-workflow-distribution-latency/#0001-01-01)

## 改善风险工作流分布延迟

微软最近发表的一篇研究论文《加速分布式请求-响应工作流》，“Speeding up Distributed Request-Response Workflows”，讨论了在 Bing 上关于延迟分布工作流的一些相关性，这对于金融行业的风险计算有一定的关联。直接无环图（DAG）通常是风险计算解决方案的一部分——这涉及到当某些底层市场输入发生变化时，需要重新计算哪些交易，以及集群中的服务器和有助于生成结果的汇总。鉴于成本降低与持续减少延迟的需求，Kwiken 框架从端到端的角度看待延迟改进和成本，可能为金融行业提供一些有趣的学习点。文中还讨论了两种新的延迟减少技术：一种新的超时策略，以部分答案换取延迟；以及用于追赶滞后查询的方法。

~ mdavey 于 2013 年 8 月 5 日发表。

发布在 [HPC](https://mdavey.wordpress.com/category/hpc/)
