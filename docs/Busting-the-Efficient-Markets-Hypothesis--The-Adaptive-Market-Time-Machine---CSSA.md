<!--yml

类别：未分类

日期：2024-05-12 18:49:08

-->

# 打破有效市场假说：自适应市场时光机 | CSSA

> 来源：[`cssanalytics.wordpress.com/2009/09/14/busting-the-efficient-markets-hypothesis-the-adaptive-market-time-machine/#0001-01-01`](https://cssanalytics.wordpress.com/2009/09/14/busting-the-efficient-markets-hypothesis-the-adaptive-market-time-machine/#0001-01-01)

在这一系列的帖子中，我将挑战有效市场假说，并介绍一种使用无偏自适应学习算法的方法论。我将展示出，一个没有先验信息或假设的学习算法可以在短期数据中找到有利可图的模式，并且轻松地击败市场，风险更低。这个“自适应市场时光机”将从 1955 年开始交易标准普尔 500 指数，除了过去 5 个交易日的运行序列之外，没有其他工具。时光机不是一个黑匣子，它进行实验并使用任何科学家或任何精通“量化取向”的交易员都可以执行的基本统计学。进一步增加实验的真实性的是，与今天大多数技术分析工具不同，运行数据是交易员在 1955 年实际上可能使用的信息。

有效市场假说（EMH）理论是学术界对投资行业的可怕批评。它大致陈述，没有人可以期望在长期内系统地胜过市场，那些成功的人只是幸运而已。有关现代学术评论和 EMH 的优秀背景，请阅读安德鲁·罗（Andrew Lo）的这篇论文：[`web.mit.edu/alo/www/Papers/EMH_Final.pdf`](http://web.mit.edu/alo/www/Papers/EMH_Final.pdf)

交易员和投资组合经理经常会回答说，有效市场假说在实践中不起作用-他们已经回测了几种策略，这些策略在长期内一直击败市场。有效市场假说的高级祭司和创始人会回答说，他们只是进行**数据挖掘**-也就是说，他们偶然发现了过去有效的规则或一小部分规则，但这并不意味着这些规则在未来也会有效。这是一个非常有效的观点：我们如何知道这个过程是以一种实际上在真实生活中推广的方式进行的？简单的样本外或前向测试是不够的-您可能会验证特定策略是健壮的，但不能验证回测过程和方法如何适用于各种方法/指标。也就是说，**研究过程本身必须是可推广的**，否则您只是验证了一个在实践中有效的策略存在着强大的效应。这并不意味着使用相同的方法/研究过程将能够发现和验证也会在样本外有效的新效应。

还有其他难以看到的陷阱：我们如何确定回测不是简单地偏向于特定的市场环境？当趋势跟随主导“最佳”策略时，将是以趋势为导向，但你怎么知道它们开始失败了？你如何知道体制是否在改变？唯一真正知道的方法是如果你能模仿智能和深思熟虑的回测过程，并创建一台机器，它既不具备先验知识，也不偏向于任何特定的策略。然后，你会带着那台机器在新环境中进行测试和交易。其中最好的自适应过程示例是利用每日跟踪策略，并首次由迈克尔·斯托克斯在 MarketSci 进行详细介绍：[`marketsci.wordpress.com/2008/11/19/the-simple-made-powerful-with-adaptation/`](http://marketsci.wordpress.com/2008/11/19/the-simple-made-powerful-with-adaptation/) 对这个概念在股市中的唯一且实质性的学术文章是由一些加拿大教授撰写的（可能是因为其晦涩），我强烈推荐你阅读：[`docs.google.com/gview?a=v&q=cache:lBeGPkJ5TMMJ:www.fma.org/SLC/Papers/cnPKR161m.pdf+Can+Machine+Learning+Challenge+the+Efficient+Market+Hypothesis%3F&hl=en&gl=ca`](http://docs.google.com/gview?a=v&q=cache:lBeGPkJ5TMMJ:www.fma.org/SLC/Papers/cnPKR161m.pdf+Can+Machine+Learning+Challenge+the+Efficient+Market+Hypothesis%3F&hl=en&gl=ca) 经过了大量阅读，并测试了机器学习和神经网络，我可以告诉你，自适应市场时间机器完全不同。它做出决策的方式和结果是直观的 - 不像神经网络能发现人类不可能理解的关系。与机器学习不同，它不使用复杂的非线性回归技术。这项技术最类似于粒子群优化，但有着明显的差异。但在根本上，它进行统计测试，并利用非常稳健的进化机制来了解什么是有效的，以及事物如何变化。更多关于时间机器的内容将在下一篇文章中详细介绍。
