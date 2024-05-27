<!--yml

分类：未分类

日期：2024-05-18 06:26:29

-->

# 粗略计数器：分析 Linux 在多核上的可扩展性 | 来自交易台的故事

> 来源：[`mdavey.wordpress.com/2013/04/23/sloppy-counters-analysis-of-linux-scalability-to-many-cores/#0001-01-01`](https://mdavey.wordpress.com/2013/04/23/sloppy-counters-analysis-of-linux-scalability-to-many-cores/#0001-01-01)

## 粗略计数器：分析 Linux 在多核上的可扩展性

来自[论文](http://pdos.csail.mit.edu/papers/linux:osdi10.pdf)第 7 页：

> 我们的解决方案，称为粗略计数器，基于这样的直觉：每个核心可以持有少量对对象的备用引用，希望可以将这些引用的所有权赋予在该核心上运行的线程，而无需修改全局引用计数。更具体地说，粗略计数器将一个逻辑计数器表示为单个共享中央计数器和一组每个核心计数的备用引用。当一个核心将粗略计数器增加 V 时，它首先尝试通过将其每个核心计数减少 V 来获取备用引用。如果每个核心计数大于或等于 V，表示有足够的本地引用，则减少成功。否则，核心必须从中央计数器获取引用，因此它将共享计数器增加 V。当一个核心将粗略计数器减少 V 时，它释放这些引用作为本地备用引用，将其每个核心计数增加 V。

结论指出，只要您知道要修改什么，并且熟悉标准的并行编程技术🙂，就可以通过更改应用程序代码（或内核）来消除大多数内核性能瓶颈。

~ by mdavey on 2013 年 4 月 23 日。

Posted in [语言](https://mdavey.wordpress.com/category/languages/)
