<!--yml

分类：未分类

date: 2024-05-12 19:34:20

-->

# Magic Ink II | 编码市场

> 来源：[`etrading.wordpress.com/2012/03/22/magic-ink-ii/#0001-01-01`](https://etrading.wordpress.com/2012/03/22/magic-ink-ii/#0001-01-01)

## Magic Ink II

### 2012 年 3 月 22 日

我[之前发过文](https://etrading.wordpress.com/2012/03/01/magic-ink/)介绍过 Bret Victor 的 Magic Ink。现在我读完了这篇相当长的论文。在后半部分，Victor 详细讲述了信息应用——包括大多数金融应用——应该如何实现。信息应用需要从用户行为的历史中学习：Victor 以自己在 BART 调度应用中的实现为例说明了这一点。他指出，尽管机器学习已经进行了数十年的研究，但我们仍然没有将那些研究成果封装得整洁、易于使用的抽象概念，这对于普通应用开发者来说是不够的。这不应该是一个问题，因为我们已经有了各种计算机科学研究领域（如文件系统、排序算法、GUI 等）的很好用的抽象概念。

在 Victor 方案中，信息应用的另一个主要支柱是上下文敏感性。他有力地论证了通过一个动态绑定的组件模型来实现这一点，这个模型与[Brad Cox 20 年前倡导的模型](http://virtualschool.edu/cox/pub/PSIR/)相似。 Plus ca change !

最后，Victor 讨论了信息应用应该运行在哪种设备上。他描述的听起来像是 iPad。记住，iPad 是在 2010 年推出的，而 Victor 写 Magic Ink 是在 2006 年。所以他的预见性是非常惊人的。
