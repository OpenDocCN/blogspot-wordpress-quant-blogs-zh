<!--yml

类别：未分类

日期：2024-05-18 04:47:02

-->

# 智能交易：人工免疫系统与金融应用？

> 来源：[`intelligenttradingtech.blogspot.com/2010/02/artificial-immune-systems-and-financial.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2010/02/artificial-immune-systems-and-financial.html#0001-01-01)

目前流行的一个术语是 AIS 或人工免疫系统。它是一种本质上试图复制我们自身天然免疫系统算法的生物启发分类系统。我们的身体有各种识别外来入侵者的防御机制。其中一种防御机制是利用构建在我们基因组中的病原体相关分子模式，这样我们就可以识别外来病原体并对其做出反应。这种能够区分自我和非自我的概念，实际上是从我们的天然生物防御中借鉴的一个主要主题。

这个想法是我们可以学会识别不正常的物体并对它们做出反应。一个很好的例子是 SPAM 检测。我们希望能够识别出好的（已知的）邮件和（未知的）坏的邮件，并利用 AIS 避免寄生 SPAM。

目前最常用的 AIS 系统是负选择算法。它本质上是通过训练分类器生成负样本随机，如果这个负样本（想象一个 2D 网格上的坐标）随机生成的位置（使用一些距离度量，如欧几里得或马哈拉诺比斯距离）靠近一个已知的好的例子，那么它就被拒绝。本质上，我们是为分类器随机生成负样本。

![图](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi1co2vpaA80sKbC4xCRF0Elj3FQY5V-_WmlCg6G0JgYdAawwoe-ARahpfVBoFXIOyYuaHRM8vousbGSAra5cou9o7ZErX3owcj9qbJDgJWahw2ua5CB2oGwjitSXnk5lx13PODK05bRgI/s1600-h/AIS_example.jpg)

图 1. AIS 类型分类的基本概念

虽然它已经在一些信用检测等应用中被使用，但在基于 AI 的算法中，你会发现还有很多其他算法可能做同样的工作或更好。在交易系统中，我们可能想要识别异常的时间序列行为并根据这些信息做出决策，然而，使用统计控制方法可能更容易确定这些信息。

总之，尽管这个想法听起来很有希望，但我还没有看到很多实践中的优秀例子，这些例子对于交易系统来说无法通过现有的 AI 算法来实现。

[人工免疫系统](http://www.artificial-immune-systems.org/)

该网站上有很多优秀的阅读材料，还有一个 Weka 插件，可以供跟随 Weka 教程的读者使用此算法。
