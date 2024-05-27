<!--yml

类别：未分类

日期：2024 年 5 月 17 日 23:38:39

-->

# Fokker-Planck 方程，费勒约束和边界条件–HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2013/05/04/fokker-planck-equation-feller-constraint-and-boundary-conditions/#0001-01-01`](https://hpcquantlib.wordpress.com/2013/05/04/fokker-planck-equation-feller-constraint-and-boundary-conditions/#0001-01-01)

Fokker-Planck 正向方程是校准随机波动模型的局部波动率扩展的重要工具，例如 Heston 模型的局部波动率扩展。但是边界条件的处理——特别是在零瞬时方差时——是非常困难的，如果费勒约束

![\sigma² \le 2\kappa\theta](img/93659630c1c3500de6d47b5e11f2bd05.png)

对于方差的平方根过程 ![\nu ](img/055272eff19b00f433d1c4d5cb2f1743.png)

![d\nu_t = \kappa(\theta-\nu_t)dt + \sigma\sqrt{\nu_t}dW ](img/4af261bfcf0d5287fd2ea27975a5833a.png)

被违反。相应的 Fokker-Planck 正向方程

*![\frac{\partial p}{\partial t} = \frac{\sigma²}{2}\frac{\partial²}{\partial \nu²}(\nu p) - \frac{\partial}{\partial \nu}\left(\kappa\left(\theta-\nu \right ) p\right) ](img/b58a476db8bdff063eb53607c0e1c9f0.png)

描述了概率密度函数*p*的时间演变和在原点处的边界 ![\nu=0 ](img/d4ad13d9f0f911ea45f9f15351ce64ff.png) 如果费勒约束被违反，即可能立即达到。在这种情况下，Fokker-Planck 方程[1]的稳态解

![p_\nu = \frac{\eta^\eta}{\Gamma(\eta)}\frac{\nu^{\eta-1}}{\theta^\eta}e^{-\eta\nu/\theta},\ \eta=\frac{2\kappa\theta}{\sigma²}](img/d887394694b61252aaa8ff46de38b6e4.png)

随！[`hpcquantlib.wordpress.com/2013/05/04/fokker-planck-equation-feller-constraint-and-boundary-conditions/#0001-01-01`](https://hpcquantlib.wordpress.com/2013/05/04/fokker-planck-equation-feller-constraint-and-boundary-conditions/#0001-01-01)

![\lim_{\nu\to 0} p_\nu^{s} \sim \nu^{\eta-1} = \nu^{-\alpha},\ \alpha=1-\frac{2\kappa\theta}{\sigma²} ](img/cf9a00ebd5b6559f676b0a2cbb10a988.png)

和原点处的零流边界条件

![\left.\left[ \frac{\sigma²}{2}\frac{\partial}{\partial \nu} (\nu p) + \kappa(\nu-\theta)p\right]\right|_{\nu=0} = 0 ](img/0a363d806048f3f15d07d14e9f90bfd1.png)

变得难以在数值上进行跟踪。将偏微分方程重写为 ![q_\nu = v^\alpha p_\nu](img/4ab282ce2879403aab30aae349f96e54.png) 有助于缓解问题[2]。

![\frac{\partial q}{\partial t} = \nu\frac{\sigma²}{2}\frac{\partial²}{\partial \nu²} q + \kappa(\nu+\theta)\frac{\partial}{\partial \nu}q + \frac{2\kappa²\theta}{\sigma²}q ](img/2d758c4bd2f314a097974730bb6d8b6a.png)

*q*中对应的零流边界条件读作如下

![\left.\left[ \nu\frac{\sigma²}{2}\frac{\partial}{\partial \nu} q + \kappa\nu q\right]\right|_{\nu=0} = 0 ](img/1d9af5d4fcf08f5782f5c8f3da45a731.png)

为了应用边界条件，第一步是在非均匀网格上在空间方向上离散化变换后的 Fokker-Planck 方程 ![\nu_i](img/c12f6546d6c0d88be936cfac37126542.png)

![\frac{\partial q_i}{\partial t} = \alpha_iq_{i-1}+\beta_iq_i+\gamma_iq_{i+1]} ](img/052394286b32b6291c58862678e83ba2.png)

with

![\begin{array}{rcl} h_i &=& \nu_{i+1}-\nu_i \\ \zeta_i &=& h_{i-1}h_i \\ \zeta^p_i &=& h_i(h_{i-1}+h_i) \\ \zeta^m_i &=& h_{i-1}(h_{i-1}+h_i) \\ \alpha_i &=& \frac{1}{\zeta^m_i}\left(\sigma²\nu_i-\kappa(\theta+\nu_i)h_i)\right) \\ \beta_i &=& \frac{1}{\zeta_i}\left( -\sigma²\nu_i+\kappa(\theta+\nu_i)(h_i-h_{i-1}) \right ) +\frac{2\kappa²\theta}{\sigma²} \\ \gamma_i &=& \frac{1}{\zeta^p_i}\left( \sigma²\nu_i + \kappa(\theta+\nu_i)h_{i-1} \right ) \end{array} ](img/0135cfe1b2b8691f89e19f28a0c4d414.png)

接下来的步骤是使用二阶前向离散化[3]来离散化零流边界条件导数![\frac{\partial q}{\partial \nu}](img/11bebc0e82b87839f6f36d1430b5729b.png)。

![\left.\left[ \nu\frac{\sigma²}{2}\frac{\partial}{\partial \nu} q + \kappa\nu q\right]\right|_{\nu=\nu_{i-1}} \approx a_iq_{i-1} + b_iq_{i} + c_iq_{i+1} = 0 ](img/01399fbc2ae0d6d714bf008fc437b389.png)

with

![\begin{array}{rcl} \eta_i &=& \frac{1}{h_{i-1}h_i(h_{i-1}+h_i)} \\ a_i &=& - \eta\frac{\sigma²}{2}\nu_{i-1}\left((h_{i-1}+h_i)²-h_{i-1}² \right ) + \kappa\nu_{i-1} \\ b_i &=& \eta\frac{\sigma²}{2}v_{i-1}\left(h_{i-1}+h_i \right )² \\ c_i &=& -\eta\frac{\sigma²}{2}v_{i-1} h_{n-1}² \end{array} ](img/c540f2408bef666ed132179df9cf15b6.png)

现在边界![\nu_0](img/c15610bd2db7c127cda5ec48aff90fe0.png)处的值![q_{0}](img/a52fdb7a3f8e9d957152a2263d914281.png)可以用![q_1](img/ca4cb4f59bf32dddd72682afec2b6653.png)和![q_2](img/dab963ffb5426e3685a6abd100531c72.png)的形式表达。

![q_{0} = \frac{-b_1q_{1} - c_1q_{2}}{a_1}](img/236b4898ffa5bf9978c4d9a99653a73a.png)

这个方程可以用于从转换后的福克-普朗克方程的离散化中去除边界值![q_0](img/b23f0e755ad8fabd34fc6590bb55461e.png)。同样的方法可以用于上边界![\nu_{max}](img/31fc6a7a428dbb82341675dddc6aa113.png)的零流边界条件，也可以用于原始福克-普朗克方程。

方块根过程的以下参数将用于测试不同的边界条件。

![\kappa=2.5,\ \theta=0.2,\ \sigma\in\{0.2, 2.0\} ](img/c13a22f00113af9cb5659055da00b5f2.png)

均匀网格![\nu_{min} \le \nu_i \le \nu_{max}](img/dbbcf66c05263beade9d15da56fe4da0.png)有 100 或 1000 个网格点，并且福克-普朗克方程的稳态解![p^s_{\nu_i}](img/7b2ca8c3be6d531b92bc8b4aa6afc130.png)被选为网格点上的起始配置。边界![v_{min}, v_{max}](img/2b5cf020ff4da7df9b5445c59263e4dc.png)通过累积分布函数的逆来定义，使得

![\int_0^{v_{min}}p^s_\nu d\nu = \int_{v_{max}}^\infty p_\nu^s d\nu = 1\% ](img/8e2e38444493ee965ddeddccaacf9612.png).

网格覆盖了 98%的分布，如果边界条件满足且没有离散化误差，则该值随时间不会改变。 为了测试离散化误差的量级，我们让初始解在 Crank-Nicolson 方案中使用 100 个时间步长演化一年。 结果解 ![q_{i,t=1} = v_i^\alpha p_{i,t=1}](img/c2ac86d37a48c930f4f4c0d2328aac36.png) 被插值为三次样条，得到函数 ![q_\nu](img/0e1e31233d7ed40e4830e4dbe82eaf65.png)。 值

![\int_{vmin}^{v_{max}}q_\nu\nu^{-\alpha} d\nu - 98\% ](img/8df08b98ef82e823bf3f170ecbbf7544.png)

作为边界条件的离散化误差的质量指标。

如下图所示，如果 ![\sigma](img/d2e0f91b4f9ab5cb8554a898295d118c.png) 很小，那么原始的 Fokker-Planck 方程比在 ![q=v^\alpha p](img/1aa7c27506ffb3d46a4d2b7f5592b626.png)中的变换的 Fokker-Planck 方程显示出更小的离散化误差。 但是，如果 ![\sigma](img/d2e0f91b4f9ab5cb8554a898295d118c.png) 变大，尤其是如果 Feller 约束被违反，那么变换的 Fokker-Planck 方程的解显然优于原始解。 根据这个例子的经验法则，如果 ![\frac{2\kappa\theta}{\sigma²} \ge 2.5](img/3debfe345dc692bb14237168597e3397.png)，应使用原始的 Fokker-Planck 方程，否则应使用变换后的方程。

![plot](https://hpcquantlib.wordpress.com/wp-content/uploads/2013/05/plot.png)

可以用相同的技术来解决 Heston 模型的 Fokker-Planck 方程。 数值测试的代码可在最新的[QuantLib](http://www.quantlib.org)版本中从 SVN[trunk](http://sourceforge.net/p/quantlib/code/HEAD/tree/)获取。 该图基于测试 FDHestonTest :: testSquareRootEvolveWithStationaryDensity。

[1] A. Dragulescu, V. Yakovenko, [Heston 模型中随机波动性的收益概率分布](http://arxiv.org/pdf/cond-mat/0203046)

[2] V. Lucic, [通过 PDE 方法计算混合模型中密度的边界条件](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1191962)

[3] P. Lermusiaux, [数值流体力学](http://ocw.mit.edu/courses/mechanical-engineering/2-29-numerical-fluid-mechanics-fall-2011/index.htm)，讲座笔记 14，第 5 页*
