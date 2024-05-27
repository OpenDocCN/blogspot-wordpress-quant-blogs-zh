<!--yml

category: 未分类

date: 2024-05-18 05:43:41

-->

# 代码所有权 | 来自一个交易台的故事

> 来源：[`mdavey.wordpress.com/2015/02/26/code-ownership/#0001-01-01`](https://mdavey.wordpress.com/2015/02/26/code-ownership/#0001-01-01)

## 代码所有权

杰伊·菲尔德在他的一篇有趣的[文章](http://blog.jayfields.com/2015/02/experience-report-weak-code-ownership.html)中对代码所有权进行了介绍，“经验报告：弱代码所有权”。"厨房里的厨师太多"不幸地是一个问题，我怀疑我们在中到大型项目上都看过太多次了。显而易见，要在 n 年的大型代码库上鼓励一致性是困难的——不幸的是，那些没有软件工程背景的利益相关者并没有真正理解这些问题。

主要代码所有权方法听起来很有趣，并让我想起了以前在涉及项目的服务器和客户端部分的小团队上采取的类似方法，每个团队都有一个主要所有者。显然，将项目分割成微服务的风格只能通过避免单个个人试图设置和管理大型代码库的代码所有权来帮助项目。

也许还值得注意克里斯·康利最近对配对编程和杀死[代码审查](http://eatcodeplay.com/why-we-killed-off-code-reviews/)的评论。我认为代码审查往往被过度宣传为一种灵丹妙药的解决方案。

> 我们现在充分理解了[分支和拉取请求](http://blog.codinghorror.com/the-multi-tasking-myth/)的额外开销。这不仅仅是检出一个分支、编写一个出色的拉取请求或者评审人每小时 `200 LOC` 的工作量。

~ mdavey，于 2015 年 2 月 26 日发布。

发布在[敏捷](https://mdavey.wordpress.com/category/agile/)分类中
