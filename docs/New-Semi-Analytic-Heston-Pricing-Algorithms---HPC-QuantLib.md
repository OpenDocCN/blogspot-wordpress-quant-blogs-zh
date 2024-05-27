<!--yml

分类：未分类

date: 2024-05-13 00:12:49

-->

# 新的半解析 Heston 定价算法 - HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2017/05/07/newer-semi-analytic-heston-pricing-algorithms/#0001-01-01`](https://hpcquantlib.wordpress.com/2017/05/07/newer-semi-analytic-heston-pricing-algorithms/#0001-01-01)

QuantLib 中 Heston 模型的定价引擎已经有些过时。同时，新的更好的算法已经在文献中得到发展和讨论。欢迎参阅 [1][2] 进行全面审查。是时候翻新现有的引擎了。

Heston 模型由以下股票对数的随机微分方程定义

![\begin{array}{rcl} d \ln S_t&=& \left(r_t - q_t - \frac{\nu_t}{2}\right)dt + \sqrt\nu_t dW^{S}_t \nonumber \\ d\nu_t&=& \kappa\left(\theta-\nu_t \right ) dt + \sigma\sqrt\nu_t dW^{\nu}_t \nonumber \\ \rho dt &=& dW^{S}_tdW^{\nu}_t \end{array}](img/7bb998b60af889698cbc7da23e39455e.png)

Gatheral 形式中的归一化特征函数为

![\phi_t(z) = \exp\left\{\frac{v_0}{\sigma²}\frac{1-e^{-Dt}}{1-Ge^{-Dt}}\left(\kappa-i\rho\sigma z-D\right) + \frac{\kappa\theta}{\sigma²}\left(\left(\kappa-i\rho\sigma z-D\right)t-2\ln\frac{1-Ge^{-Dt}}{1-G}\right) \right\}](img/579b82b565b9de252e33440e65e2414a.png)

![\begin{array}{rcl} D&=&\sqrt{\left(\kappa - i\rho\sigma z\right)²+\left(z²+iz\right)\sigma²} \nonumber \\ G&=&\displaystyle\frac{\kappa -i\rho\sigma z-D}{\kappa -i\rho\sigma z + D}\end{array}](img/e77612059b60e5dc57ad01a117bfe2f4.png)

Andersen 和 Piterbarg [3] 引入了一个 Black-Scholes 控制变量，以提高 Lewis 公式（2001 年）对香草看涨期权价格的数值稳定性

![\begin{array}{rcl} C(S_0, K, T)&=&BS\left(S_0, K, T, \sigma_{BS}\right) \nonumber \\ &+& \frac{\sqrt{Se^{(r-q)t}K}e^{-rt}}{\pi}\displaystyle\int\limits_{0}^{\infty}{\Re\left( \frac{\phi^{BS}_T\left(u-\frac{i}{2}\right) - \phi_T\left(u-\frac{i}{2}\right)}{u²+\frac{1}{4}} e^{i u \left(\ln\frac{S}{K}+(r-q)T\right) } \right)  \mathrm{d}u}\end{array}](img/1de9ba5864c76669e051677209a00460.png)

其中香草期权的 Black-Scholes 价格 ![BS\left(S_0, K, T, \sigma_{BS}\right)](img/7a540b78e38573509ae5522e932ac68c.png) 具有波动率 ![\sigma_{BS}](img/babcd5b93d361ec65726e3dbaf6fcdd0.png) 和特征函数

![\phi^{BS}_T(z)=e^{-\frac{1}{2}\sigma_{BS}² T (z² + iz)} ](img/af848a6610ddd0dcd89bc0f92e65175c.png)

为了实现最优控制变量，提出了不同的香草期权波动率方案：

+   ![\sigma_{BS}² = \nu_0](img/7ac94af4c1aca949bf2c55faccc14ca3.png)

+   ![\sigma_{BS}² = \frac{1}{\kappa t}\left(1-e^{-\kappa t}\right)\left(\nu_0-\theta\right) + \theta](img/b6298ad4724d204bf2a507c70d4d1660.png)

+   ![\sigma_{BS}² = c_2](img/31b7724e5a2431897429fcdb04d930d4.png) 其中 ![c_2](img/8de07e0ce5a8488d46add26b04e95db8.png) 是 ![ln \frac{F}{K}](img/09fe352c30db9e119e89321c5cd029ca.png) 的第二累积量 [1]。

下图显示了不同控制变量波动率和 Heston 模型参数的结果被积函数。

![r=7.5\%, q=5\%, S_0=100, \nu_0=0.08, \rho=-80\%,\sigma=0.5, \kappa=4, \theta=0.05](img/57eebc588a72bbdd75f87f40fd528bab.png)

并且对于执行价为![K=200](img/41aca03c616c2e5f4eb5072f3a4ae864.png)和到期日为![t=2.0](img/55d255484c530b33eb2c8decec022c12.png)的普通认购期权。

![控制变量](img/f9f0a0d654821d2c2f0d96b6cb74b816.png)

最佳选择取决于 Heston 和期权参数，但似乎

![\sigma_{BS}² = \frac{1}{\kappa t}\left(1-e^{-\kappa t}\right)\left(\nu_0-\theta\right) + \theta](img/b6298ad4724d204bf2a507c70d4d1660.png)

对于各种参数而言，这是一个很好的选择。有控制变量和没有控制变量时，对函数被积函数进行直接比较，展示了控制变量的有效性。

![对照比较](img/0f5cfe684756355c37ad462e29d55bd5.png)

Andersen-Piterbarg 的核心技巧是将 Lewis 的无限积分截断至有限的![u_{max}](img/a86dcfd76fe79e4ff4fdf256bc0a91d6.png)，使得剩余部分小于基于下列不等式的给定阈值

![\displaystyle\int_{u_{max}}^\infty \left\vert \frac{\phi_B(u-\frac{i}{2}) - \phi(u-\frac{i}{2})}{u²+\frac{1}{4}} \right\vert du \le e^{-C_\infty u_{max}}\displaystyle\int_{u_{max}}^\infty \frac{1}{u²} du](img/128518b9a8a2e17563f3f17706aa3cf7.png)

请参阅原始论文或[2]，了解如何从这里得到一个算法用于![u_{max}](img/a86dcfd76fe79e4ff4fdf256bc0a91d6.png)，特别是短期期权。

正如 Andersen 和 Piterbarg 所指出的，如果使用控制变量，简单的梯形法则在执行得到的积分时效果出奇的好。Alan Lewis 的[测试案例](https://forum.wilmott.com/viewtopic.php?f=34&t=90957&hilit=heston#p620396)，具有高精度 Heston 参考价格，应该作为测试的基础，特别是执行价为 100 的认购期权。Gauss-Laguerre 方法对这个特定测试案例非常感谢，但这里的重点是，梯形法则的收敛速度比高阶 Simpson 法则或甚至更复杂的自适应 Gauss-Lobatto 方法要快得多。

![收敛速度](img/1dc2a71795ce0a21c0885efe28d60c4d.png)

下图将最近新增的 COS 引擎与使用梯形法则的 Andersen-Piterbarg 方法进行了比较。对于相似数量的点，Andersen-Piterbarg 方法更为精确。

![收敛比较](img/1cb61bc3936f7a05a65f8ea18b12695e.png)

实现是 pull request [#251](https://github.com/lballabio/QuantLib/pull/251) 的一部分。

[1] M. Schmelzle，《利用 Fourier 变换的期权定价公式：理论与应用》。

[2] F. Le Floc’h，《傅里叶积分和随机波动率校准》。

[3] L. Andersen, and V. Piterbarg, 2010, 《利率建模，第一卷：基础和普通模型》，大西洋金融出版社，伦敦。
