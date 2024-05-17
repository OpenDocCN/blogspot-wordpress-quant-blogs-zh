<!--yml
category: 未分类
date: 2024-05-18 06:03:24
-->

# Improving Risk Workflow Distribution Latency | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/08/05/improving-risk-workflow-distribution-latency/#0001-01-01](https://mdavey.wordpress.com/2013/08/05/improving-risk-workflow-distribution-latency/#0001-01-01)

## Improving Risk Workflow Distribution Latency

A recently [published](http://research.microsoft.com/pubs/192571/kwiken_sigcomm13.pdf) research paper by Microsoft, “Speeding up Distributed Request-Response Workflows”, which discusses latency distribution workflows on Bing offers some correlations with regards to risk calculations in the financial vertical.  Direct Acyclic Graphs (DAG)’s are often part of the solution to risk calculation – as part of the dependencies with regards to what trades need to be re-calculated when some underlying market input is changes, to the servers in a cluster and the aggregations that aid result generation.  Given the cost reduction coupled with the ongoing need to reduce latency, Kwiken, a framework that takes an end-to-end view of latency improvements and costs probably offers some interesting learning points that finance can leverage.  Two new latency reduction techniques are also discussed: a new timeout policy tp trade off partial answers for latency and catching-up for laggard queries.

~ by mdavey on August 5, 2013.

Posted in [HPC](https://mdavey.wordpress.com/category/hpc/)