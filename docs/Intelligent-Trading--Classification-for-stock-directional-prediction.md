<!--yml

category: 未分类

date: 2024-05-18 04:47:17

-->

# 智能交易：用于股票方向预测的分类

> 来源：[`intelligenttradingtech.blogspot.com/2010/02/classification-for-prediction.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2010/02/classification-for-prediction.html#0001-01-01)

神经网络教程关注一种被称为回归的方法。机器学习中常用的另一种方法称为分类。这两种方法在识别从一组数据中学习最佳可能曲线方面有些相似。区别在于他们如何使用曲线从数据中学习。在回归的情况下，我们通常是在最小化每个示例与平均值之间的距离，而在分类的情况下，我们是通过区域来区分不同类别。

尽管下面的例子在任何意义上都可以被视为市场效率的一个例子（即在预测方面没有太多优势），但它用来阐述通过应用市场预测的基本分类思想。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhBqoeX-26wdGl8YojW6oj12iCEpDdcekCF8_IWSVz0MmX7KAi-40fVF5h2ZEcmQjgbWrT__80a2yxFsHZRPg35D4NMZEbf2jGHg4DL0dkIG9pMKOdkKR7sjlPsUyfsYnYMy7cxxuzEvpU/s1600-h/classa1.jpg)

Fig 1. 标普 500 周变化与 VIX 的变化

在上面的图中，我们看到标普 500 周回报与 VIX（波动性的代理）的常见散点图表示。利用回归的常见观察表明标普 500 与 VIX 负相关。或者从定性角度看，VIX 的大正值暗示 S&P 指数的负值变化；这是它常被称为恐慌指数（因为 VIX 的上升与 S&P 500 的负回报相关）的一个原因。如果我们运行一个回归，我们会通过斜率的 R² 值来定量描述这种相关性，正如在这里 visually，它是一个负值。

但是回归观察并没有说出关于未来预测的任何东西，它只说在任何给定的样本瞬间（在这个案例中，是周样本）两个值之间存在负相关关系。为了说明，设定预测问题的一种方法是使用标普 500 指数和 VIX 的当前变化来预测下一周的变化，使用分类方法。

图表显示了一周后的上升（UP）和下降（DN）变化，上升用绿色标签表示，下降用红色标签表示。注意，这里的预测结果是名义上的，而不是数字上的，这是分类和回归方案之间的另一个常见区别特征。部署分类方案的常用方法包括学习树、支持向量机，以及大多数也用于回归的工具。理想情况下，如果分类方案能够很好地区分类别，它会通过曲线或某种函数将样本内和样本外的类别分开，实现良好的分离。

不幸的是，当数据非常随机时，它无法很好地分离类别。

![图](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj1hGnosVsw72sDf7MVeILKqpUoYdg7Ag0T0wkat9zSPhhFvp8ZlnZlmU19OO_a7W9hm2F7zijJ0xWWRYp_Id4ap2-D_IX9MfmuCe2tI0LMdyL5Nu-qp8RSfpXxbNGt7dSjEhDGv3JGZz0/s1600-h/classplot1.jpg)

图 2. 标普 500 上升（UP）和下降（DN）与 VIX 的分类值图表

我们可以看到，上升（UP）和下降（DN）区域的重叠如此之大，以至于很难找到一个曲线对这些区域进行良好的分类。

我们使用一种常见的决策树学习方案 J.48，试图为分类器预测样本外的结果。

![图](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhwhLC8pK2reszc0Y_d2SUobWdiRfK6fiiCCOriy464e_i12euU0T2MNglMl_I8EhtXXHKarp3sAygbiAbv7zGSrFsABtoJyHN84iQHWx8MWbAgkCNgw_nWhvmcHJHVPRTcEiZkeOtJ5UY/s1600-h/wekaclassout.jpg)

图 3. 样本外分类结果

使用 66%的样本内（训练）方案，如神经网络（NN）示例所示，我们发现预测学习者的样本外成功率为 53%。如果我们把这个结果与一个简单的朴素学习者（通常作为一个基准）进行比较，后者使用最后一个结果作为预测，我们会得到相同的结果。这说明利用我们所拥有的信息，市场已经证明了对这种简单的预测方法是有效的。

分类概念可以扩展到其他应用（如政权检测、系统选择、人工免疫系统或使用多元输入属性），但这里的目标是为机器学习中最重要的学习概念之一提供一个简单的介绍。分类也可以采用监督或无监督的方法——在这个例子中，采用的是监督学习（通过示例进行训练）。
