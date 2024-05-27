可以使用 Mathematica 计算非中心卡方分布的前 n 个矩![\mu_i(d, \lambda), i=0,..,n](img/30af049efdcd30a39895904a3e63e19e.png)，并将其导出为纯 C 代码，以便集成到 QuantLib 中。

![ \begin{array}{rcl} z_{k, i} &=& z_{k-1, i+1} + \alpha_k z_{k-1,i} - \beta_k z_{k-2,i} \\ \nonumber \alpha_{k+1} &=& \frac{z_{k-1,k}}{k-1,k-1}-\frac{z_{k,k+1}}{z_{k,k}} \\ \nonumber \beta_{k+1} &=& \frac{z_{k,k}}{z_{k-1,k-1}}\\ \nonumber z_{-1,i} &=& 0 \\ \nonumber z_{0,i} &=& \mu_i = \int_0^\infty x^i\chi_{d,\lambda}^{'2}(x) dx \\ \nonumber \alpha_1 &=& -\frac{\mu_1}{\mu_0} \\ \nonumber \beta_1 &=& \mu_0 = 1\end{array} ](img/5ff276f77e9371ffc817d70da94af577.png)

![ \nu_t = \frac{\sigma² (1- e^{-\kappa t})}{4\kappa} \chi_d^{'2}\left(\frac{4\kappa e ^{-\kappa t}}{\sigma²(1-e^{-\kappa t})}\nu_0\right)](img/6d453b703272cfde72c815758cd7aea4.png)

<!--yml

# 具有平方根核过程的 CLV 模型 - HPC-QuantLib

> 类别：未分类

Collocating Local Volatility（CLV）模型的核心过程[1]定义了模型的前期偏斜动态。虽然 Ornstein-Uhlenbeck 过程具有一些良好的分析特性，但有时对前期偏斜动态的控制力度不够。平方根过程

![d\nu_t=\kappa(\theta-\nu_t) dt + \sigma \sqrt{\nu_t}dW_t ](img/f5bcf96d62120c9cf7fc549d3c0b5f71.png)

是一种有前景的核心，以更好地控制前期偏斜。首先，对于平方根过程，精确抽样非常容易。给定![\nu_0](img/c15610bd2db7c127cda5ec48aff90fe0.png)，![\nu_t](img/c56c88dfcf2d52e0221304d7c3dd90f9.png)的概率密度函数为

来源：[`hpcquantlib.wordpress.com/2016/11/02/the-clv-model-with-a-square-root-kernel-process/#0001-01-01`](https://hpcquantlib.wordpress.com/2016/11/02/the-clv-model-with-a-square-root-kernel-process/#0001-01-01)

其中![\chi_d^{'2}](img/d001df63428660a5acdceef1a172fd1e.png)表示自由度为 d 的非中心卡方分布，非中心参数

![d=\frac{4\theta\kappa}{\sigma²}](img/bb8ea86ea02539e4e1f82d43172284c6.png)

日期：2024-05-17 23:26:53

![ \lambda = \frac{4\kappa e^{-\kappa t}}{\sigma²(1-e^{-\kappa t})}\nu_0 ](img/0f91941ec7244e8e2f4f349363631bd1.png)

boost 库提供了非中心卡方累积分布函数的逆的高效准确实现，该函数可用于精确的蒙特卡罗抽样方案。

最佳的拟合点由高斯求积点给出，其由对应正交多项式的零点定义。正交多项式由递推关系定义，拟合点由对角线为![\{\alpha_i\}](img/42689b0d62841508524b832adddc8bd9.png)和副对角线为![\{\sqrt{\beta_i}\}](img/37ac220896fb9d4b4443fd4244e759b9.png)的对称三对角矩阵的特征值给出。同样，这些向量由递推关系定义[2]

-->

-->

```
m[n_] := CForm[ Expectation[X^n, X \[Distributed]
NoncentralChiSquareDistribution[d, lambda]] // Simplify]

```

使用双精度解决递推关系通常是病态的。因此，结果方程将使用 Boost.Multiprecision 包的 cpp_dec_float 后端（仅标头且无依赖性）来解决。结果已根据[3]中的提案进行了测试。对于任何合理数量的插值点，精度高达 100 位似乎是足够的。另一方面，即使使用 100 位，计算速度也非常快。特征值计算使用标准双精度进行。

实施校准例程的方式与 Ornstein-Uhlenbeck 核过程相同。尽管涉及多精度算术，与其他结构化模型相比，校准速度快且准确。

**示例：前期波动率偏斜**

+   市场价格由 Heston 模型给出

![S_0=100, r=0.1, q=0.05, \nu_0=0.09, \kappa=1.0, \theta=0.06, \sigma=0.4, \rho=-0.75](img/5b939a0cb5329020a11b678c9cdd5460.png).

+   SquareRoot-CLV 核过程参数由以下给出

![\kappa=0.2, \theta=0.09, \sigma=0.1, x_0=0.09](img/ca696a25fdb6b8f07a1aa226b0b6a7e8.png)

下图显示了从 0.5 到 2 变化的摩尼尼斯的前期欧式期权的隐含波动率，并在重设日期后六个月到期。

![circlvforwardskew1](img/7dbf509dfb1f32a4a785efdd995ff863.png)

相同的图，但使用平方根核过程的以下参数

![\kappa=0.1, \theta=0.09, \sigma=0.1, x_0=0.25](img/64c895d94dc2a288e9822239cb513de1.png)

![circlvforwardskew2](img/03960a1c1378af347046250d7823009f.png)

源代码可在[此处](http://hpc-quantlib.de/src/squarerootclvmodel.zip)获取。该代码处于早期阶段，需要进行更多测试/清理才能进行拉取请求。下一步将是校准这样的 CIR-CLV 模型到 Heston 随机局部波动率模型的前期偏斜动态。

[1] A. Grzelak，2016，[CLV 框架-高效定价的新视角](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2747541)

[2] M. Morandi Cecchi 和 M. Redivo Zaglia，[计算系数](http://ac.els-cdn.com/0377042793901522/1-s2.0-0377042793901522-main.pdf?_tid=643d5dca-a05d-11e6-9a56-00000aab0f27&acdnat=1478023545_cf7c87cba4cc9e37a136e68a2564d411) [的循环公式](http://ac.els-cdn.com/0377042793901522/1-s2.0-0377042793901522-main.pdf?_tid=643d5dca-a05d-11e6-9a56-00000aab0f27&acdnat=1478023545_cf7c87cba4cc9e37a136e68a2564d411) [用于数值积分的时刻和](http://ac.els-cdn.com/0377042793901522/1-s2.0-0377042793901522-main.pdf?_tid=643d5dca-a05d-11e6-9a56-00000aab0f27&acdnat=1478023545_cf7c87cba4cc9e37a136e68a2564d411) [修改后的时刻。](http://ac.els-cdn.com/0377042793901522/1-s2.0-0377042793901522-main.pdf?_tid=643d5dca-a05d-11e6-9a56-00000aab0f27&acdnat=1478023545_cf7c87cba4cc9e37a136e68a2564d411)

[3] Walter Gautschi，[如何以及如何不检查高斯积分公式。](https://www.cs.purdue.edu/homes/wxg/selected_works/section_08/084.pdf)
