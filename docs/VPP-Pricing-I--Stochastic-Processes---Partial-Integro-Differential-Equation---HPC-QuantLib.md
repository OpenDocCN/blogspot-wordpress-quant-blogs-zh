<!--yml

category: 未分类

date: 2024-05-13 00:14:43

-->

# VPP 定价 I：随机过程与偏积分微分方程 – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2011/06/13/vpp-pricing-i-stochastic-processes-partial-integro-differential-equation/#0001-01-01`](https://hpcquantlib.wordpress.com/2011/06/13/vpp-pricing-i-stochastic-processes-partial-integro-differential-equation/#0001-01-01)

虚拟电厂（VPP）定价算法的基础是电价和天然气价格的联合随机过程。而不是直接为火花价差定义随机微分方程，然后火花价差由电价和天然气价格与 VPP 加热速率的差值给出。

Kluge 模型将用于定义电价过程[1]，指数 Ornstein-Uhlenbeck 将描述天然气价格[2]。

![\begin{array}{rcl} P_t &=& \exp(p_t + X_t + Y_t) \\ dX_t &=& -\alpha X_tdt + \sigma_x dW_t^x \\ dY_t &=& -\beta Y_{t-}dt+J_tdN_t \\ \omega(J) &=& \eta e^{-\eta J} \\ G_t &=& \exp(g_t + U_t) \\ dU_t &=& -\kappa U_tdt+\sigma_udW_t^u \\ \rho &=& \mathrm{corr} (dW_t^x, dW_t^u) \end{array} ](img/3768dc187d2f6603d1486e83db42175e.png)

其中![N_t](img/c6d44fd3b9c210c1d0e71a4a31edb3dc.png)是具有跳跃强度![\lambda](img/4a42b8a415b6b944138e18b71269a40a.png)的泊松过程。为了匹配电力远期曲线![F_0^t](img/421429e49cb430d88afd689dbfe570cc.png)，季节函数![p_t](img/cc857dceaf2cce62952d13ed185808ee.png)由以下方式给出[1]：

![p_t = \ln F_0^t -X_0 e^{-\alpha t}-Y_o e^{-\beta t} -\frac{\sigma_x²}{4\alpha}\left(1-e^{-2\alpha t} \right ) - \frac{\lambda}{\beta}\ln\left( \frac{\eta-e^{-\beta t}}{\eta-1}\right), \eta\ge 1 ](img/548ed5dae1a1d0ea73e1335fad1cefad.png)

为了与天然气远期曲线![H_0^t](img/504a5aed47ba8963503203fba9869fbe.png)保持一致，季节函数![g_t](img/70df1b7221b3a8610b98be43534c9da8.png)由以下方式定义：

![g_t = \ln H_0^t -U_0 e^{-\kappa t}-\frac{\sigma_u²}{4\kappa}\left(1-e^{-2\kappa t} \right )](img/0714df32e939de28523fe51be31d4443.png)

Feynman-Kac 定理可应用于推导相应的三维偏积分微分方程。

![\begin{array}{rcl} rV&=&\frac{\partial V}{\partial t}+\frac{\sigma_x²}{2}\frac{\partial² V}{\partial x²}-\alpha x\frac{\partial V}{\partial x}-\beta y \frac{\partial V}{\partial y} \\[6pt]&+&\frac{\sigma_u²}{2}\frac{\partial² V}{\partial u²}- \kappa u\frac{\partial V}{\partial u} +\rho\sigma_x\sigma_u\frac{\partial² V}{\partial x\partial u}\\[6pt] &+&\lambda\int_\mathbb{R}\left(V(x,y+z,u,t)-V(x,y,u,t) \right )\omega(z)dz \\ \end{array}](img/7f253ce1b580c8eb2d310af36b53214c.png)

In general at least one further dimension is needed to keep track of the state of the virtual power plant. Therefore solving this model using finite difference methods will lead to a four-dimensional PIDE problem.

以下图表显示了基于免费提供的[Kyos 示例远期曲线](http://www.kyos.com/?content=65)的电力和天然气价格的一年路径示例。 样本参数化受到[1]影响电力过程和[2]影响天然气过程。

![\beta=200, \eta=2.5, \lambda=4, \alpha=7, \sigma_x=1.4, \kappa=4.45, \sigma_u=\sqrt{1.3}, \rho=70\%](img/c230c94b41b29da82370f3cd9dbef901.png)

![](https://hpcquantlib.files.wordpress.com/2011/06/plot5.png)

代码可在[这里](http://hpc-quantlib.de/src/vpp1.zip)获得。 它依赖于最新的[QuantLib](http://www.quantlib.org/)版本，来自[SVN trunk](http://sourceforge.net/p/quantlib/code/HEAD/tree/)。 如果您想直接从 C ++程序生成图表，还需要[R](http://www.r-project.org/)，[RCPP](http://cran.r-project.org/web/packages/Rcpp/index.html)和[RInside](http://cran.r-project.org/web/packages/RInside/index.html)。

[1] T. Kluge，[定价摆动期权和其他电力衍生品](http://eprints.maths.ox.ac.uk/246/1/kluge.pdf)

[2] G. Fusai，A. Roncoroni，[在量化金融中实施模型：模型和案例](http://www45.essec.edu/professorsCV/showRef.do?bibID=364)，第十九章，ISBN：978-3-540-22348-1
