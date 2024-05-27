<!--yml

分类：未分类

日期：2024-05-18 05:32:20

-->

# 被 Python 3 困扰——HBase 和 Phoenix | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2016/05/11/stung-by-python-3-hbase-and-phoenix/#0001-01-01`](https://mdavey.wordpress.com/2016/05/11/stung-by-python-3-hbase-and-phoenix/#0001-01-01)

## 被 Python 3 困扰——HBase 和 Phoenix

深夜里的一次 Apache [HBase](https://hbase.apache.org/) 和 Apache [Phoenix](https://phoenix.apache.org/) 实验。围绕 Phoenix 的连接问题让我困惑不解。遵循了简单的[安装](https://phoenix.apache.org/installation.html)指南。我知道 HBase 正在运行，因为[简单](http://www.tutorialspoint.com/hbase/pdf/hbase_create_table.pdf)的表创建操作可以成功。然而，Phoenix 就是不愿意返回数据 😦

解决方法。将 Python3 降级至 Python2.7。问题解决

~ mdavey 于 2016 年 5 月 11 日。

发布在 [HPC](https://mdavey.wordpress.com/category/hpc/) ， [编程语言](https://mdavey.wordpress.com/category/languages/)
