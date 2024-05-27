<!--yml

category: 未分类

date: 2024-05-17 23:41:02

-->

# 摆动期权：线性规划与动态规划 II – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2011/06/04/swing-option-linear-vs-dynamic-programming-ii/#0001-01-01`](https://hpcquantlib.wordpress.com/2011/06/04/swing-option-linear-vs-dynamic-programming-ii/#0001-01-01)

为了更好地了解蒙特卡罗/线性规划和有限差分法/动态规划之间的区别，我们评估了一种更真实的具有每小时支付概况的摆动期权，该概况基于德国每小时的远期曲线。这个远期曲线来自于[Kyos 示例下载页面](http://www.kyos.com/?content=65)。 Kluge 模型的参数化在[1]中概述。

以十二周为期限，示例摆动期权提供了![12*7*24=2016](img/5646a4e5fc3a2f4f07e39a9e1800ba5f.png)次执行机会。总体执行的摆动机会次数受到限制

![100 \le \sum_{i=1}^{2016} \beta_i \le 500](img/4a820d640b4437a9e9f7d3848bde26aa.png).

有限差分法（动态规划）的两个维度的大小已经确定。时间方向需要 2016 步，而“已执行操作”方向需要 500 步。加上另外两个方向 - 一个用于电价，另一个用于跳跃过程 - 而且没有进一步简化，这就构成了一个相当大的有限差分问题。基于蒙特卡罗的线性规划方法减轻了计算负担，但将导致摆动期权价格的上限。下图显示了相应的结果。

![](https://hpcquantlib.wordpress.com/wp-content/uploads/2011/06/plot4.png) [](https://hpcquantlib.wordpress.com/wp-content/uploads/2011/06/plot3.png)  [](https://hpcquantlib.wordpress.com/wp-content/uploads/2011/06/plot2.png)

代码在[这里](http://hpc-quantlib.de/src/fwdswing.zip)。它依赖于[GNU 线性规划套件](http://www.gnu.org/software/glpk/)，用于并行化的[Boost 线程](http://www.boost.org)库，以及在撰写本文时最新的[QuantLib](http://www.quantlib.org)版本来自[SVN 主干](http://sourceforge.net/p/quantlib/code/HEAD/tree/)。如果您想直接从 C++程序生成图形，还需要[R](http://www.r-project.org/)、[RCPP](http://cran.r-project.org/web/packages/Rcpp/index.html)和[RInside](http://cran.r-project.org/web/packages/RInside/index.html)。为了利用所有 CPU 核心，请使用-DNTHREADS=(CPU 核心数量)编译器开关。此外，要运行该程序，您必须从[Kyos 网页](http://www.kyos.com/?content=65)下载德国电力远期曲线，并将其转换为以下格式的文本文件 EEX_2010-2013.txt

2010 年 10 月 4 日 36.73 32.09 27.32 23.22 25.71 35.60 47.32 …

2010 年 10 月 5 日 38.12 31.12 22.76 25.65 27.87 34.60 50.01 …

[1] T. Kluge, [电力衍生品定价：摆动期权及其他](http://eprints.maths.ox.ac.uk/246/1/kluge.pdf)
