<!--yml

category: 未分类

date: 2024-05-18 13:50:33

-->

# 协方差、相关性和 RMT | Quantivity

> 来源：[`quantivity.wordpress.com/2011/06/05/covariance-correlation-and-random-matrix-theory/#0001-01-01`](https://quantivity.wordpress.com/2011/06/05/covariance-correlation-and-random-matrix-theory/#0001-01-01)

正如以前通过[basket prediction](https://quantivity.wordpress.com/2010/08/22/high-frequency-prediction-via-rmt-pca/)所举例的，Quantivity 正在越来越频繁地使用随机矩阵理论（RMT），特别是在投资组合/篮子协方差和相关性分析的背景下跨越所有交易频率。虽然无疑是夸张的，但 RMT 开始感觉像 1990 年代的 PCA。

下面是对 RMT 文献的调查，以激发读者的兴趣。读者被要求在评论中提出额外的相关文献。随后的帖子可能会根据读者的兴趣进一步探讨 RMT 的实际应用细节。

要开始，以下是 RMT 的现代书籍长度的处理：

以下是扩展调查文章（分别专注于理论和数值分析），可在线获取：

以下是按发布时间顺序排列的应用 RMT 文章：

+   [金融相关性矩阵的噪声修饰](http://arxiv.org/abs/cond-mat/9810255)，Laloux 等人 (1998)

+   [金融时间序列交叉相关性的普遍和非普遍性质](http://arxiv.org/abs/cond-mat/9902283)，Plerou 等人 (1999)

+   [随机矩阵理论和金融相关性](http://ideas.repec.org/p/sfi/sfiwpa/500053.html)，Utsugi 等人 (1999)

+   从股价波动中识别商业部门，Gopikrishnan 等人 (2000)

+   [金融数据交叉相关性的随机矩阵方法](http://arxiv.org/abs/cond-mat/0108023)，Plerou 等人 (2001)

+   [股票市场相关性的动态](http://arxiv.org/abs/cond-mat/0103606)，Drozdz 等人 (2001)

+   [噪声协方差矩阵和组合优化](http://arxiv.org/abs/cond-mat/0111503)，Pafka 和 Kondor (2001)

+   [噪声协方差矩阵和组合优化 II](http://arxiv.org/abs/cond-mat/0205119)，Pafka 和 Kondor (2002)

+   [金融市场交叉相关性的随机矩阵理论分析](http://arxiv.org/abs/cond-mat/0312643)，Utsugi、Ino 和 Oshikawa (2003)

+   [金融相关性矩阵中的信号和噪声](http://arxiv.org/abs/cond-mat/0312496)，Burda 和 Jurkiewicz (2004)

+   [金融协方差矩阵的指数加权和基于随机矩阵理论的过滤](http://arxiv.org/abs/cond-mat/0402573)，Pafka、Potters 和 Kondor (2004)

+   [用于组合优化的随机矩阵理论：一种稳定性方法](http://www.sciencedirect.com/science/article/pii/S0378437103011841)，Sharifi 等人 (2004)

+   [随机矩阵理论在金融中的应用：旧图案和新拼图](http://arxiv.org/abs/physics/0507111)，Potters，Bouchaud 和 Laloux（2005 年）

+   [组合优化中的随机矩阵滤波](http://ideas.repec.org/p/arx/papers/physics-0509235.html)，Papp 等人（2005 年）

+   [股票市场相关矩阵的大部分不是纯噪音](http://www.sciencedirect.com/science/article/pii/S0378437105005716)，Kwapien 等人（2005 年）

+   [金融相关性分析中的非对称矩阵](http://arxiv.org/abs/physics/0605115)，Kwapien 等人（2006 年）

+   [使用增强协方差矩阵进行风险评估](http://www.if.pw.edu.pl/~jholyst/data/07110411514812005.pdf)，Urbanowicz，Richmond 和 Holyst（2007 年）

+   [随机但并非完全：金融时间序列的收益和相关矩阵的参数化](http://arxiv.org/abs/physics/0701025)，Martins（2007 年）

+   [基于随机矩阵理论的金融时间序列中的拓扑性质](http://arxiv.org/abs/0709.2209)，Eom 等人（2007 年）

+   [金融交叉相关中的经验与随机矩阵理论](http://arxiv.org/abs/0711.0644)（2007 年），Drozdz，Kwapien 和 Oswiecimka

+   [最大生成树、资产图和随机矩阵去噪在金融网络动态分析中的应用](http://arxiv.org/abs/0806.4714)，Heimo，Kaski 和 Saramaki（2008 年）

+   [去趋势交叉相关分析：分析两个非平稳时间序列的新方法](http://prl.aps.org/abstract/PRL/v100/i8/e084102)，Podobnik 和 Stanley（2008 年）

+   [随机矩阵理论在金融中的应用：简要回顾](http://arxiv.org/abs/0910.1205)，Bouchaud 和 Potters（2009 年）

+   [金融市场相关性的时间演化](http://arxiv.org/abs/1011.3225)，Fenn 等人（2010 年）

+   [金融时间序列中的交叉相关动态](http://arxiv.org/abs/1002.0321)，Conlon 等人（2010 年）

这些文章很好地说明了过去十年中 RMT 在应用上的演变，无论是在广度还是在复杂性上。
