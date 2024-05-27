→yaml

类别：未分类

日期：2024-05-12 17:38:39

→

# Mean-Reversion Trading Strategies in Python Course | CSSA

> 来源：[`cssanalytics.wordpress.com/2020/11/12/mean-reversion-trading-strategies-in-python-course/#0001-01-01`](https://cssanalytics.wordpress.com/2020/11/12/mean-reversion-trading-strategies-in-python-course/#0001-01-01)

![Quantra Logo](https://cssanalytics.files.wordpress.com/2020/11/quantra-logo-color.png)

本文包含联盟链接。联盟链接意味着 CSSA 可能会在您通过链接购买商品时获得补偿，而对您来说没有任何额外费用。CSSA 努力推广那些对我的业务有价值的产品和服务，以及那些我认为可以帮助您的*读者*的产品和服务。

在[上篇文章](https://cssanalytics.wordpress.com/2020/11/09/an-interview-with-dr-ernest-chan/)中，我采访了 Ernest Chan 博士，他是[Mean-Reversion Trading Strategies in Python Course](https://quantra.quantinsti.com/course/python-mean-reversion-strategies-ernest-chan?utm_source=david_varadi&utm_medium=affiliate&utm_campaign=CSSA)的作者，我将在本文中回顾这个课程。**对报名课程感兴趣的读者可以跟随这个[链接](https://quantra.quantinsti.com/course/momentum-trading-strategies?utm_source=david_varadi&utm_medium=affiliate&utm_campaign=mts_course)并使用优惠券代码：CSSA5 获得额外的 5%折扣**

该课程由[Quantra/QuantInsti](https://www.quantinsti.com/?utm_source=david_varadi&utm_medium=affiliate&utm_campaign=CSSA)提供，该机构为包括[动量交易策略](https://quantra.quantinsti.com/course/momentum-trading-strategies?utm_source=david_varadi&utm_medium=affiliate&utm_campaign=mts_course)在内的多种不同主题提供算法交易课程，我曾在[一篇先前的文章](https://cssanalytics.wordpress.com/2020/10/29/momentum-trading-strategies-course/)中介绍过这个课程。

**Python 中均值回归交易策略的评论**

![MR](https://cssanalytics.files.wordpress.com/2020/11/mr-2.png)

来源：Quantra/QuantInsti

很久以前，当我刚开始使用定量方法进行交易时，我和一个朋友尝试使用仅带有数据输出的 Excel 笔记本实施统计套利策略。虽然我对要做什么有一个合理的了解，但我既没有技术知识，也没有实践经验，或者编程/操作技能来正确地做这件事。虽然回测看起来很棒，但实际交易让它们看起来像沙漠中的海市蜃楼。不出所料，这种“半吊子”的操作是失败的。如果我能回到过去并参加这个课程，我可能成功的几率会大得多。这个课程教你初学者和高级统计套利技术，并展示如何使用 Python 代码直接连接到 Interactive Brokers。

课程讲师陈博士并非那种脱离现实的学术权威或金融经济学家，他们在纸上或课堂黑板上讨论套利机会。他是一位有着成功记录的对冲基金经理。因此，这门课程包含了所有重要的现实检验；从显而易见的如交易成本，到常被忽视的如考虑卖空的可获得性和借款成本，再到复杂的如在进行指数套利时保持非负权重的重要性，以避免通过股票特定风险增加暴露。**在我看来，这就是为什么量化分析师应该认真考虑在 Quantra/QuantInsti 上上课的原因，如果他们想要至少避免那些成本远高于课程费用的初学者错误的话。**

课程开始定义平稳性，然后将此与均值回归交易策略联系起来。呈现了各种统计检验，如 Augmented-Dickey-Fuller (ADF)检验，以及所需的数学和 Python 计算代码。然后介绍了使用 Bollinger Bands 或 Z 分数的基本均值回归策略，这些策略可以应用于平稳时间序列。这进一步扩展到创建实际头寸组合以及如何使用信号来管理这些头寸，同时计算损益。我喜欢这样一个事实，即在大多数交易者立即进行回测之前，提供了使用平稳性统计检验测试交易策略的原因的解释。

陈博士随后讨论了 Johansen 检验作为更 versatile 的检验方法，与 ADF 检验进行了比较，并展示了如何使用计算出的特征向量进行各种应用。内容包括如何对三只股票（一次三只）进行套利，以及对篮子套利。半衰期计算及其应用也是内容的重要组成部分（许多来源经常解释得不好，但这次不是）。我喜欢这门课程涵盖了风险管理，以及如何处理断开的对子——这是每个人都需要知道的东西。还提供了对交易最佳市场的指导。课程最后讨论了横截面均值回归策略，这在博客上已经有很多讨论了。Python 代码涵盖了课程中的所有内容，以及如何立即在 Interactive Brokers 中应用即插即用的方法。

总体来说，如果你想在统计套利方面入门，无论是在公司层面还是个人层面，这都是一份优秀的入门资料。虽然它没有展示任何秘诀，但它为你提供了所有技术上和实践上的编程知识，作为开发你自己的套利策略的基础。所以，如果你已经有非常丰富的经验，这门课程可能不适合你。但如果你在技术/实践方面经验不足，你一定要考虑参加这门课程。此外，还有一个 Quantra 社区帮助回答问题并建立网络。向 Chan 博士和 Quantra/QuantInsti 团队中的非常才华横溢的团队成员致敬，他们共同策划了这门课程。
