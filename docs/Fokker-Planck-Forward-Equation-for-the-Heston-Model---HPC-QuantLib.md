<!--yml

类别：未分类

日期：2024-05-17 23:32:07

-->

# Heston 模型的 Fokker-Planck 正向方程–HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2013/02/10/fokker-planck-forward-equation-for-the-heston-model/#0001-01-01`](https://hpcquantlib.wordpress.com/2013/02/10/fokker-planck-forward-equation-for-the-heston-model/#0001-01-01)

考虑 Heston 模型的随机微分方程，用于描述对数价格的动态 ![x_t = \ln S_t](img/16f746d6b95837f7e9cfec20abd14a6d.png)

![\begin{array}{rcl} dx_t &=& \left(r_t - q_t - \frac{\nu_t}{2}\right)dt + \sqrt\nu_t dW^{x}_t \nonumber \\ d\nu_t&=& \kappa\left(\theta-\nu_t \right ) dt + \sigma\sqrt\nu_t dW^{\nu}_t \nonumber \\ \rho dt &=& dW^{x}_tdW^{\nu}_t \end{array} ](img/53a92059f4ae5536232c2c5457f4c828.png)

Fokker-Planck 正向偏微分方程描述了概率密度函数的时间演变 ![p(x_t,\nu_t,t)](img/a8ed804ebd6f4de152f21323df199521.png)

![\frac{\partial p}{\partial t} = \frac{1}{2}\frac{\partial²}{\partial x²}(\nu p) + \frac{\partial²}{\partial x \partial \nu} (\rho\sigma\nu p) + \left(\frac{\nu}{2} -r_t+q_t\right)\frac{\partial}{\partial x} p + \frac{\sigma²}{2}\frac{\partial²}{\partial \nu²}(\nu p) - \frac{\partial}{\partial \nu}\left(\kappa\left(\theta-\nu \right ) p\right) ](img/213b494588ce90f2ab6725cb349bc52d.png)

具有初始条件

![p(x,\nu,t=0) = \delta(x-x_0)\delta(\nu-nu_0) ](img/2a97247fba0ae47fa73e458cffe40f0e.png)

其中 ![\delta](img/1367ac0656a0a771a7b2a9480c1a7e6f.png) 表示狄拉克δ分布。针对此问题的半封闭解法在[1]中提出。解决 Fokker-Planck 正向方程时，特别要注意边界条件，特别是费勒约束时

![\sigma² \le 2\kappa\theta](img/93659630c1c3500de6d47b5e11f2bd05.png)

被违反。在这种情况下，边界处的原点 ![\nu = 0](img/5e7becccce05c432fbb22a2f1c915fd5.png) 瞬间可达。在原点应用费勒零通量边界条件的泛化 [2]。

![左边[ \frac{\sigma²}{2}\frac{\partial}{\partial \nu} (\nu p) + \kappa(\nu-\theta)p + \rho\nu\sigma\frac{\partial p}{\partial x}\right]\right|_{\nu=0} = 0, \ \forall x\in \mathbb{R}^+ ](img/4858e2cc2e2eb5d9e31ece43e33931b2.png)

可以使用三点前向差分公式计算对于 ![\nu=0](img/b0f9e4f656181ec3176658771a8755b1.png) 的偏导数 ![\partial_\nu](img/bea4548488ff53cf932046bc50387cfb.png) 的二阶精确近似 [3]。

下图展示了该模型的正向方程的解。

![\small{T=1.0, S_0=1,r=0.1, q=0.05, \kappa=2.0, \theta=0.4, \rho=-0.75, v_0=1.2, \sigma=0.4}](img/ff9030e7a12cd4832cb29c4396cebaf0.png)

![plot.399](https://hpcquantlib.wordpress.com/wp-content/uploads/2013/02/plot-399.png)

狄拉克约束在![\sigma=2.0](img/a011583fe3d04361e0b8d1aae28b2bb0.png)下被违反，这完全改变了解决方案的形状。

![plot.799](https://hpcquantlib.wordpress.com/wp-content/uploads/2013/02/plot-7992.png)这个例子的代码在[这里](http://hpc-quantlib.de/src/heston_fpe.zip)可以找到，基于最新的[QuantLib](http://quantlib.org)版本来自 SVN 的[trunk](http://sourceforge.net/p/quantlib/code/HEAD/tree/)。它还依赖于[RInside](http://dirk.eddelbuettel.com/code/rinside.html)和[Rcpp](http://cran.r-project.org/web/packages/Rcpp/index.html)来生成图表。另外，zip 文件还包含一个关于![\sigma=2.0](img/a011583fe3d04361e0b8d1aae28b2bb0.png)时间演变解决方案的短视频剪辑。

[1] A. Dragulescu, V. Yakovenko, [Heston 模型中随机波动率的回报概率分布](https://arxiv.org/pdf/cond-mat/0203046)

[2] V. Lucic, [混合模型中通过 PDE 方法计算密度的边界条件](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1191962)

[3] K. A. Kopecky, [数值微分](http://www.karenkopecky.net/Teaching/eco613614/Notes_NumericalDifferentiation.pdf)
