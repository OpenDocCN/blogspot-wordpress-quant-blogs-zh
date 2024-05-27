<!--yml

分类: 未分类

日期：2024-05-12 17:38:55

-->

# 与 CSSA 的 Ernest Chan 博士的访谈

> 来源：[`cssanalytics.wordpress.com/2020/11/09/an-interview-with-dr-ernest-chan/#0001-01-01`](https://cssanalytics.wordpress.com/2020/11/09/an-interview-with-dr-ernest-chan/#0001-01-01)

![](https://cssanalytics.files.wordpress.com/2020/11/ernest-chan.png)

“我的很多想法都是基于逻辑的”

[在上一篇文章中](https://cssanalytics.wordpress.com/2020/10/29/momentum-trading-strategies-course/)，我回顾了 Quantra（[QuantInsti](https://www.quantinsti.com/?utm_source=david_varadi&utm_medium=affiliate&utm_campaign=CSSA) 的一个部门）的[动量交易策略课程](https://quantra.quantinsti.com/course/momentum-trading-strategies?utm_source=david_varadi&utm_medium=affiliate&utm_campaign=mts_course)。这是我最近进行的一次教育旅程的一部分，旨在提高我的量化技能水平。我接下来将要审查的课程是由 Ernie Chan 博士教授的[Python 中的均值回归策略](https://quantra.quantinsti.com/course/python-mean-reversion-strategies-ernest-chan?utm_source=david_varadi&utm_medium=affiliate&utm_campaign=CSSA)。我个人已经阅读了 Ernie 的书籍[“机器交易”](https://www.amazon.com/Machine-Trading-Deploying-Computer-Algorithms-ebook/dp/B01N7NKVG0)，这本书写得非常好，充满了有趣而实用的想法。我也一直关注他非常受欢迎的[博客](http://epchan.blogspot.com/)，该博客是揭示统计套利策略（如配对交易）的先驱。Chan 博士是思想领袖和行业专家，任何从事量化领域的人都不可避免地在某种形式上接触到他的工作。我联系他进行采访，以了解如何在现代时代思考量化模型的一些见解。对于不熟悉 Chan 博士工作的人，我提供了他非常出色（而且广泛）的行业和教育背景。 

**行业背景:** Chan 博士是 [PredictNow.ai](https://www.predictnow.ai/) 的创始人，这是一个金融机器学习 SaaS，并且是 [QTS Capital Management, LLC.](https://www.qtscm.com/) 的管理成员，这是一个商品池操作员和交易顾问。他的主要关注点是开发统计模型和先进的计算机算法，以在大量数据中找到模式和趋势。他将自己在统计模式识别方面的专业知识应用于项目，从 IBM 研究的文本检索，到 Morgan Stanley 的客户关系数据挖掘，以及在 Credit Suisse、Mapleridge Capital Management 和其他对冲基金进行的统计套利交易策略研究。

**教育背景**

陈博士是‘算法期权交易’领域的行业专家，并在许多国际论坛上进行了研讨会和讲座。除了是 QuantInsti 的教员外，他的学术成果还可在 Quantra 和主要网络门户上找到。陈博士还是西北大学数据科学硕士项目的兼职教员。他在金融和机器学习方面的课程和出版物可在[www.epchan.com](https://www.epchan.com/workshops/)上找到。欧尼是《“量化交易：如何打造自己的算法交易业务”》、《“算法交易：获胜策略及其原理”》和《“机器交易”》的作者，均由 John Wiley & Sons 出版。他在 epchan.blogspot.com 上维护着一个流行的博客“量化交易”。欧尼在康奈尔大学获得了物理学博士学位。

**与欧尼·陈博士的采访**

**1) 你认为传统因子投资和使用技术指标的交易策略在现代环境中是否有利可图？ **

我们不使用机器学习来生成交易信号，而是用来确定基本传统定量策略生成的现有交易信号的盈利概率。这种策略可以是一个因子模型，也可以是基于简单技术指标的模型。然后可以使用这个盈利概率来确定订单大小，如果概率太低，订单大小可以为零。

因子和技术指标仍然对基本策略至关重要。我不认为机器学习能够取代人类的直觉和理解能力。实际上，它应该被用来增强这种理解和风险管理能力。机器学习算法的输入只是因子和技术指标。

**2) 如果你能在动量和均值回归交易之间选择，你会选择哪个，为什么？**

我会同时交易这两种策略。否则，投资组合将不会是市场中性，因为动量策略通常是短贝塔，而均值回归策略是长贝塔。此外，动量策略是长“gamma”和“vega”，而均值回归策略则是短的。请注意，我在这些期权希腊字母周围加了引号，因为我们实际上并没有交易期权或隐含波动率。我在这里使用这些术语是为了表示尾部波动性和实现波动性的增加。

**3) 为什么交易者应该强烈考虑在交易中使用机器学习，而不是手工编码他们自己的定量系统或使用更简单的统计工具？对于不熟悉编码的交易者来说，你认为最好的入门方式是什么？**

传统的量化策略太容易被其他同样聪明的交易员复制，因此它们所获得的α衰减更快。机器学习策略有如此多的参数和细微差别，以至于没有两个交易员可能拥有相同的策略。对于不擅长机器学习或编程的交易员，可以从像[predictnow.ai](http://predictnow.ai/)这样的无代码机器学习服务开始。

**4) 您认为新手尝试设计自己的机器学习模型的最大挑战是什么？**

机器学习需要充足且正确地构建特征作为输入。我见过很多新手尝试给机器学习算法使用 4 或 5 个输入。他们应该至少使用 100 个输入。

**5) 在选择机器学习模型的类型时，您是否更倾向于使用神经网络还是 KNN 或决策树？如果是，为什么？**

决策树，或者更先进的版本叫随机森林，是交易的首选机器学习方法。这是因为它所要拟合的参数没有神经网络那么多，从而减少了数据窥探偏见的危险。此外，决策树的输出是一堆条件决策规则，比神经网络使用的非线性函数要容易解释得多。另一方面，KNN 或逻辑回归太简单 - 它们无法捕捉不同输入特征和输出回报之间大量的非线性依赖关系。

**6) 许多交易员和市场评论家注意到市场似乎比过去要不同得多。市场似乎要快得多，并且会以出乎意料的方式对新闻做出反应。鉴于您在算法交易方面的丰富经验，您在过去几年内获得了哪些新趋势或见解？您是否根据这些做了具体调整或重新校准了模型？**

市场模式通常会在短期内偏离“正常”（如 6 个月至 1 年），但它们通常会恢复到正常状态。人们需要多样化，以便在这些时期加强一些策略，尽管其他策略会受到影响。这种制度更替也可以在一定程度上通过机器学习来检测或预测。

***感谢厄尼进行的采访！***
