<!--yml

分类：未分类

日期：2024-05-17 23:40:50

-->

# VPP 定价 IV：对完全预见性的方差缩减 – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2011/08/12/vpp-pricing-iv-variance-reduction-for-perfect-foresight/#0001-01-01`](https://hpcquantlib.wordpress.com/2011/08/12/vpp-pricing-iv-variance-reduction-for-perfect-foresight/#0001-01-01)

尽管*完全预见性*仅提供了真实 VPP 价值的上限，但差异通常可以忽略不计，并且与基于有限差分方法或最小二乘蒙特卡罗的“精确”定价相比，实施工作量较小。 *完全预见性*是在问题包含时间积分约束时与线性规划优化器结合使用的方法选择。因此，值得测试两种标准方差缩减技术的效率，即对偶抽样和准蒙特卡罗（QMC）与布朗桥一起。这两种方法在[1]中有详细解释，对偶抽样在第 4.2 章，准蒙特卡罗在第五部分。随机化 QMC 用于计算 QMC 的误差估计，如在第 5.4 章中概述的那样。

使用上一节[VPP 定价 III](https://hpcquantlib.wordpress.com/2011/08/07/vpp-pricing-iii-exact-pricing-based-on-finite-difference-methods/)的参数化，QMC 结合布朗桥在 6 个月合同中明显优于其他算法，如下图所示。 代码可在[此处](http://hpc-quantlib.de/src/vpp5.zip)获取。它依赖于最新的[QuantLib](http://www.quantlib.org/)版本，源自[SVN 主干](http://sourceforge.net/p/quantlib/code/HEAD/tree/)或即将发布的 QuantLib 1.2 版本。如果您想生成图表，还需要[R。](http://www.r-project.org/) [](https://hpcquantlib.wordpress.com/wp-content/uploads/2011/08/plot1.png) ![](https://hpcquantlib.wordpress.com/wp-content/uploads/2011/08/plot2.png)![](https://hpcquantlib.wordpress.com/wp-content/uploads/2011/08/plot3.png)

[1] P. Glasserman，《金融工程中的蒙特卡罗方法》。 ISBN-0387004513
