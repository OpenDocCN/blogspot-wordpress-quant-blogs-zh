<!--yml

分类：未分类

日期：2024-05-18 08:07:06

-->

# 一个用 Python 编写的 Eviews 工作文件阅读器 | 量化角落

> 来源：[`quantcorner.wordpress.com/2015/10/05/reading-eviews-workfiles-with-python/#0001-01-01`](https://quantcorner.wordpress.com/2015/10/05/reading-eviews-workfiles-with-python/#0001-01-01)

**»’** **2016 年 3 月 20 日更新：下面描述的 Eviews 工作文件阅读器也适用于 Eviews9 工作文件。

»’**

*顺带一提……*

在下面的视频中，我展示了我用**Python**编写的**Eviews**工作文件（***.wf1**）阅读器的实际操作。

对于**Eviews**工作文件格式几乎没有任何信息（毕竟这是专有的…）。我在互联网上唯一找到的资源位于这里：[EViews 工作文件格式](http://ricardo.ecn.wfu.edu/~cottrell/eviews_format/)。但是，我不能说它实际上有多大帮助。老实说，我对**Eviews**文件的结构以及数据如何（必须？）被提取（“算法”）的理解非常不同。这可能与**Eviews**版本有关。我处理的工作文件是用**Eviews 8**创建的。

目前，我编写的**Python**类将所有时间序列作为一个**pandas.DataFrame**对象返回。或者，它可以根据用户的需要返回特定系列（或一组系列）。这很容易实现。

**Eviews**工作文件中包含的一些信息尚未“解码”，例如对象最后更新的日期。这是我甚至都没有尝试过的事情。我在这里唯一愿意做的就是将**Eviews**的时间序列/观察值导出到**Python**中。

Et voilà！

[`www.youtube.com/embed/0Z841f8EHlU?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=es&autohide=2&wmode=transparent`](https://www.youtube.com/embed/0Z841f8EHlU?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=es&autohide=2&wmode=transparent)

视频
