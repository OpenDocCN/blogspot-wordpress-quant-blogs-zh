<!--yml

分类：未分类

日期：2024 年 05 月 18 日 06:00:26

-->

# Glitch：即时编程 | 来自交易台的故事

> 来源：[`mdavey.wordpress.com/2013/10/01/glitch-live-programming/#0001-01-01`](https://mdavey.wordpress.com/2013/10/01/glitch-live-programming/#0001-01-01)

## Glitch：即时编程

微软研究中对[编程](http://research.microsoft.com/pubs/201333/rem13.pdf)进行了有趣的阅读，正如该论文引用的，[Bret](http://worrydream.com/) Victor 的作品已经被考虑进来了。现在我们需要做的就是等待 n 年，也许 Glitch 将在 Visual Studio 中见到天日。

> 对输入更改通常由响应式和增量构造处理，这些构造使用起来很麻烦，表达能力有限，而程序代码的更改在执行期间通常根本不处理，使得对“实时编程”的支持变得更加复杂。我们提出，代码和输入的更改应该得到自动管理，类似于垃圾回收消除了内存管理作为程序员的显式关注点。我们的编程模型 Glitch 通过逐渐重新执行程序执行的节点，在输入/代码状态更改时变得不一致时，实现了这种管理时间。与许多响应式模型不同，Glitch 支持有表达力的共享状态过程化编程，但有一个附加条件：对共享状态的操作必须是可撤销的和可交换的，以确保重新执行的效率和最终一致性。尽管如此，像编译器这样的复杂程序也可以用平庸的编程样式写成。

~ 作者 mdavey 于 2013 年 10 月 1 日。

发布在[编程语言](https://mdavey.wordpress.com/category/languages/)分类中
