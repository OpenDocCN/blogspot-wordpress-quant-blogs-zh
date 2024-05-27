<!--yml

category: 未分类

date: 2024-05-13 00:15:22

-->

# SABR 模型的有限差分求解器 - HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2019/01/11/finite-difference-solver-for-the-sabr-model/#0001-01-01`](https://hpcquantlib.wordpress.com/2019/01/11/finite-difference-solver-for-the-sabr-model/#0001-01-01)

尽管基于一个相当简单的随机微分方程

![\begin{array}{rcl} \displaystyle dF_t &=& \alpha_t F_t^\beta dW_t \\ \nonumber d\alpha_t &=& \nu \alpha_t dZ_t \\ \nonumber \rho dt &=& <dW_t, dZ_t> \end{array}](img/47f376178554f45c17eb815238974e7b.png)

相应的偏微分方程

![\displaystyle \frac{\partial u}{\partial t} - \frac{\nu²}{2}\frac{\partial u}{\partial x} + \frac{1}{2}e^{2x}F_t^{2\beta}\frac{\partial² u}{\partial F²}+\frac{\nu²}{2}\frac{\partial² u}{\partial x²}+\rho\nu e^{x_t}F_t^\beta\frac{\partial² u}{\partial F \partial x} -ru = 0 ](img/f9d758067f04ecadb094460842f201c6.png)

对于使用变量转换![x_t = \ln \alpha_t](img/ae304008116ffa91bf6949deda15d7ba.png)、以及伊藤引理和费曼-卡尔公式导出的 SABR 模型，进行数值求解相当困难。部分问题在于底层的过程，如果![\nu](img/cafd388c0e801cfe79db6142b0511d49.png)为零，则对应到一个常弹性方差（CEV）模型。这个模型根据![\beta](img/5e11b317f8192df3c4b3952a8bb706c4.png)的值和边界条件表现出多种不同的行为。作者在[1]中对这个主题进行了全面的概述。为了限制可能的模型数量，让我们定义

![\displaystyle X\left(F_t\right) = X_t=\frac{F_t^{2(1-\beta)}}{\alpha²(1-\beta)²} \ \wedge \  \delta=\frac{1-2\beta}{1-\beta}](img/04768925906145d1cdcd7c0a5ca72e06.png)

and assume absorbing boundary conditions at ![X=0](img/a524ae337c36d7dcea7505818949fd39.png) if ![\delta < 2](img/80ac2ceded793106f743af6be261d02b.png). 针对有限差分方案的一个实现，第一步是找到离散化网格的有效限制。这些限制可以从底层过程的累积分布函数中推导出来。

![\textrm{Pr}(F \le F_t | F_0) = \begin{cases} 1-{\chi '}^{2}\left( \frac{X_0}{t}; 2-\delta, \frac{X_t}{t}\right), & \textrm{if} \ \delta < 2 \\ \nonumber 1 - {\chi '}^{2}\left( \frac{X_t}{t}; \delta, \frac{X_0}{t}\right), & \textrm{if}  \ \delta > 2 \end{cases} ](img/128f3e3c4856a7f40490d2be20462c1d.png).

请注意在第一种情况下![X(F_t)](img/af6855ccdd123ebb57f6ac3a1c2ed7af.png)![\delta<2](img/80ac2ceded793106f743af6be261d02b.png) 出现在非中心卡方分布![{\chi '}^{2}](img/ed83c0e2bf1afcdb555871a2cd3b3bd3.png) 的非中心参数中，因此只能通过数值根查找算法来计算其逆。Sankaran 的非中心卡方分布近似![{\chi '}^{2}](img/350ed103f48bcd711f1c4e5348fca9ce.png)可用于加速此方法[2]。在第二种情况下![\delta>2](img/48f88eee049d1ff29eeb97157d9b90c3.png) 方程的逆![\displaystyle \textrm{Pr}(F \le F_t | F_0) = q](img/dcdd880b7f5c005875518c96d3dec4ce.png)可计算如下:

![F_t= \left[{t \left({\chi'}²\right)}^{-1} \left(1-q; \delta, \frac{X_0}{t}\right)  \alpha²(1-\beta)²\right]^{\frac{1}{2(1-\beta)}}](img/86867f2fe848ba93436b6c130fa2f9b7.png)

可以使用 boost 库进行计算。此外，围绕重要点进行自适应网格细化和在到期日[3]的特殊点周围进行单元平均的实施改善了 CEV 有限差分方案的准确性。![F_T](img/7f085e69b6bb3607bb8f532ade50591c.png)只有在![\delta>2](img/48f88eee049d1ff29eeb97157d9b90c3.png)或等效的情况下![\beta>1](img/c298f856bf9a1a36e84d9c4b580a3ce4.png) 才是一个局部鞅。在这种情况下，看涨期权权价平价如下[1]:

![P_{\delta>2} = C_{\delta>2} + K - F_0\Gamma\left(-\nu; \frac{X_0}{2t}\right)](img/c23b003525fc32fe420360dc30b67adc.png)

并且作为实现边界条件和有限差分方案的试金石。

方差方向![x_t=\ln \alpha_t](img/ae304008116ffa91bf6949deda15d7ba.png) 符合布朗运动，因此离散化是直接的。像 Craig-Sneyd 或 Hundsdorfer-Verwer [4]这样的操作分割方案是专门设计来解决二维偏微分方程的。

有限差分求解器现在可用于将不同的近似与正确的模型行为进行比较，也可用于将其与高精度的 Monte-Carlo 模拟[2]进行比较。模型配置[5]

![F_0=1.0, \alpha=0.35, \beta=0.25, \nu=1.0, \rho=0.25, T=2.0](img/c135481b2aa7ee9e4eba40d40ae17348.png)

应充当一个测试平台。如下图所示，蒙特卡洛结果与有限差分方法的结果非常接近。Hagan 等标准公式以及 Le Floc’h-Kennedy [6]对数正态公式与正确的隐含波动率存在显著偏差。![implvol](img/163ae001da6390c0946673ad1433e057.png)

近似不是无套利的。小行权价格的概率密度转为负数。如下图所示，Hagan 的公式对比 Le Floc’h-Kennedy 公式具有更大的行权价格，展示了这种行为。如预期的，有限差分解决方案不会产生负概率。

![propdensity2.png](img/dbf612e4d0905b46838a62f278746a1e.png)关于 Floc’h-Kennedy 近似的说明，该公式在 ATM 行权水平附近变得数值不稳定，因此在货币性上使用二阶泰勒展开

![m=\frac{F}{K}-1.0 \in \{-0.0025, 0.0025\}](img/b4e6694ce8fa8280589921bdaa9c0f9d.png)

以下图表展示了二阶泰勒展开和使用 IEEE-754 双精度评估的公式之间的差异。

![taylor](img/ce847784f3dc93e75d5b30dce92b0ae9.png)

源代码是 PR＃589 的一部分，可在[此处](https://github.com/lballabio/QuantLib/pull/589)获取。

[1] D.R. Brecher, A.E. Lindsay: [CEV 过程的结果，过去和现在。](https://www.fincad.com/sites/default/files/wysiwyg/Resources-Wiki/cev-process-working-paper.pdf)

[2] B. Chen, C.W. Oosterlee, H. Weide, [SABR 的高效无偏模拟方案](http://ta.twi.tudelft.nl/mf/users/oosterle/oosterlee/SABRMC.pdf) [随机波动率模型。](http://ta.twi.tudelft.nl/mf/users/oosterle/oosterlee/SABRMC.pdf)

[3] K. in’t Hout: [详细解释金融中的数值偏微分方程](https://www.palgrave.com/de/book/9781137435682)

[4] K. in’t Hout, S. Foulon: [ADI 有限差分方案用于具有相关性的 Heston 模型的期权定价。](http://www.math.ualberta.ca/ijnam/Volume-7-2010/No-2-10/2010-02-06.pdf)

[5] P. Hagan, D. Kumar, A. Lesnieski, D. Woodward: [无套利 SABR.](http://janroman.dhis.org/finance/SABR/Arbitrage-Free%20SABR.pdf)

[6] F. Le Floc’h, G. Kennedy: [通过简单展开明确 SABR 校准](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2467231).
