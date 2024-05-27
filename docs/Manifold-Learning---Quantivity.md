<!--yml

分类：未分类

日期：2024-05-18 13:51:54

-->

# 流形学习 | Quantivity

> 来源：[`quantivity.wordpress.com/2011/05/08/manifold-learning-differential-geometry-machine-learning/#0001-01-01`](https://quantivity.wordpress.com/2011/05/08/manifold-learning-differential-geometry-machine-learning/#0001-01-01)

量化猜测游戏之一是猜测[RenTech](https://www.renfund.com/vm/index.vm)（例如，参见有趣的*5 年*[NP 帖子](http://www.nuclearphynance.com/Show%20Post.aspx?PostIDKey=4851&PageIndex=12)），特别是考虑到[吉姆·西蒙斯](http://en.wikipedia.org/wiki/James_Harris_Simons)（参见他在[arXiv](http://arxiv.org/find/math/1/au:+Simons_J/0/1/0/all/0/1)上的最近关于微分同调群的工作）迷人的背景。忽视公开评论，其真实性显然值得怀疑，仔细考虑历史招聘趋势和相应的员工背景是有启发性的。虽然这种猜测很有趣，但潜在的相关性在于*帮助筛选研究探索*。

具体来说，有几个主题是一致的：

+   基础设施/执行：计算机科学家们讨论了大规模离线和在线数据管理、风险管理、多场所执行以及最佳执行问题（尤其对于流动性提供和统计套利）的平凡现实。

+   应用数学：“自然科学家”，强调现代物理学（其中大部分建立在[微分几何](http://en.wikipedia.org/wiki/Differential_geometry)和[统计力学](http://en.wikipedia.org/wiki/Statistical_mechanics)之上），考虑到大量的数学和统计建模，这是合理的。

+   高维度：从高维空间进行分析和信号生成，这对于许多交易问题可以优雅地在这种背景下进行表述是合理的；此外，过去 20 年学术界建立的纯数学和应用数学的深厚基础；此外，考虑到吉姆的学术背景（例如，参见[陈省身-西蒙斯](http://en.wikipedia.org/wiki/Chern%E2%80%93Simons_theory)理论），这是显而易见的。

+   混合模型：RenTech 通过小规模收购和内部发展壮大，表明“预测模型”（历史上被称为“基本系统”）不是一个，而是一系列异质模型的集合，这些模型动态叠加和混合；考虑到市场体制（[市场体制](https://quantivity.wordpress.com/2010/02/15/trading-the-unobservable/)）和过去 20 年 Medallion 稳定的表现，这是合理的。

+   [计算语言学](http://en.wikipedia.org/wiki/Computational_linguistics) / [自然语言处理](http://en.wikipedia.org/wiki/Natural_language_processing): 许多顶尖人才起源于语音识别，其中过去 30 年的许多进展都是基于应用的[信号处理](http://en.wikipedia.org/wiki/Signal_processing)和[统计信息论](http://en.wikipedia.org/wiki/Information_theory)（例如[统计机器翻译的数学](http://acl.ldc.upenn.edu/J/J93/J93-2003.pdf)，由 Brown, Pietra 和 Mercer 撰写）；一个特别一致的主题是[隐马尔可夫模型](http://en.wikipedia.org/wiki/Hidden_Markov_model)（追溯到 Baker 在 1975 年开发的龙系统的混合，以及[因果滤波](http://en.wikipedia.org/wiki/Causal_filter)（参见[Berlekamp](http://math.berkeley.edu/~berlek/bus.html)，他与[Kelly](http://en.wikipedia.org/wiki/John_Larry_Kelly,_Jr.))合作）。

鉴于这个背景，让我们回到这一点：[帕尔塔·尼约吉](http://people.cs.uchicago.edu/~niyogi/) 在过去的几年里（在他不幸去世之前）多次就*流形学习*这个主题发表演讲。例如，他在[AMS/MAA/SIAM 联合会议](http://jointmathematicsmeetings.org/meetings/national/jmm/2124_intro.html)上与合作伙伴[米哈伊尔·别林金](http://www.cse.ohio-state.edu/~mbelkin/)一起介绍了[从几何角度看待学习理论和算法](http://sms.cam.ac.uk/media/545)。

流形学习特别有趣，因为它位于上述许多主题的交汇处。特别是，展示主题是：*“几何启发的学习：非线性、非参数、高维”*。这应该会引起共鸣。

摘要告诉我们更多内容：

> 越来越多的时候，我们在非常高维的空间中遇到机器学习问题。我们按照直觉进行，尽管自然数据存在于非常高的维度中，但它们的自由度相对较少。将数据建模为位于或接近高维空间中的低维流形的一种方法可以形式化这种直觉。这种观点导致了一类“流形启发”的新算法和围绕它们分析的新理论问题。这些算法中的一个中心构建是一个由数据生成的图或单纯形复合体，我们将这些与底层流形的几何形状相关联。将考虑嵌入、聚类、分类和半监督学习的应用。

换句话说，*在微分几何的背景下制定机器学习*。最常用的一个应用就是[非线性维度降低](http://en.wikipedia.org/wiki/Nonlinear_dimensionality_reduction)。这显然与定量建模有关。

对于那些想要挑战数学的读者，考虑以下内容：

根据读者的兴趣，后续的文章可能会更深入地探讨这个话题。
