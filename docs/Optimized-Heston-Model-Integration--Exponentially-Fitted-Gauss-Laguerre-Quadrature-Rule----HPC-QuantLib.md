<!--yml

category: 未分类

date: 2024-05-13 00:11:53

-->

# Optimized Heston Model Integration: Exponentially-Fitted Gauss-Laguerre Quadrature Rule. – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2020/05/17/optimized-heston-model-integration-exponentially-fitted-gauss-laguerre-quadrature-rule/#0001-01-01`](https://hpcquantlib.wordpress.com/2020/05/17/optimized-heston-model-integration-exponentially-fitted-gauss-laguerre-quadrature-rule/#0001-01-01)

Aim: Develop an exponentially-fitted Gauss-Laguerre quadrature rule to price European options under the Heston model, which outperforms given Gauss-Lobatto, Gauss-Laguerre and other pricing method implementations in QuantLib.

Status quo: Efficient pricing routines for the Heston model

![\\begin{array}{rcl} d \\ln S\_t&=& \\left(r\_t - q\_t - \\frac{\\nu\_t}{2}\\right)dt + \\sqrt\\nu\_t dW^{S}\_t \\nonumber \\\\ d\\nu\_t&=& \\kappa\\left(\\theta-\\nu\_t \\right ) dt + \\sigma\\sqrt\\nu\_t dW^\\nu\_t \\nonumber \\\\ \\rho dt &=& dW^{S}\_tdW^\\nu\_t \\end{array}](img/7bb998b60af889698cbc7da23e39455e.png)

are based on the integration over the normalized characteristic function in the Gatheral formulation

![\\phi\_t(z) = \\exp\\left\\{\\frac{v\_0}{\\sigma\²}\\frac{1-e^{-Dt}}{1-Ge^{-Dt}}\\left(\\kappa-i\\rho\\sigma z-D\\right) + \\frac{\\kappa\\theta}{\\sigma\²}\\left(\\left(\\kappa-i\\rho\\sigma z-D\\right)t-2\\ln\\frac{1-Ge^{-Dt}}{1-G}\\right) \\right\\}](img/579b82b565b9de252e33440e65e2414a.png)

![\\begin{array}{rcl} D&=&\\sqrt{\\left(\\kappa - i\\rho\\sigma z\\right)\²+\\left(z\²+iz\\right)\\sigma\²} \\nonumber \\\\ G&=&\\displaystyle\\frac{\\kappa -i\\rho\\sigma z-D}{\\kappa -i\\rho\\sigma z + D}\\end{array}](img/e77612059b60e5dc57ad01a117bfe2f4.png)

in combination with a Black-Scholes control variate to improve the numerical stability of Lewis’s formula [1][2][3]. The normalized characteristic function of the Black-Scholes model is given by

![\\phi\^{BS}\_T(z)=e^{-\\frac{1}{2}\\sigma\_{BS}² T (z\² + iz)} ](img/af848a6610ddd0dcd89bc0f92e65175c.png)

and the price of a vanilla call option can then be calculated based on

![\\begin{array}{rcl} C(S\_0, K, T)&=&BS\\left(S\_0, K, T, \\sigma\_{BS}\\right) \\nonumber \\\\ &+& \\frac{\\sqrt{Se^{(r-q)T}K}e^{-rT}}{\\pi}\\displaystyle\\int\\limits\_{0}^{\\infty}{\\Re\\left( \\frac{\\phi\^{BS}\_T\\left(u-\\frac{i}{2}\\right) - \\phi\_T\\left(u-\\frac{i}{2}\\right)}{u\²+\\frac{1}{4}} e^{i u \\left(\\ln\\frac{S}{K}+(r-q)T\\right) } \\right)  \\mathrm{d}u}\\end{array}](img/a29f81e4c4761634ab7b01cd74092f2a.png)

where ![BS\\left(S\_0, K, T, \\sigma\_{BS}\\right)](img/7a540b78e38573509ae5522e932ac68c.png) is the corresponding Black-Scholes price. Different choices for the volatility of the control variate are discussed in the literature. For the following examples the volatility will be defined by either

![\\sigma\_{BS}² = \\frac{1}{\\kappa T}\\left(1-e^{-\\kappa T}\\right)\\left(\\nu_0-\\theta\\right) + \\theta](img/789c0caab2971ab81c62176376e538cc.png)

or

![\\displaystyle \\sigma\_{BS}² = -\\frac{8}{T} \\ln{\\Re\\left(\\phi\_T\\left(-i/2\\right)\\right)}](img/51ac91fa5db2e8bbe7beb5d4cbb63e69.png).

第一个与![\sigma=0](img/34a8165faaaa3fe8484c329f7064507e.png)的整体方差相匹配，而后者与积分起点![z=-i/2](img/06d58b4dcf2b1cfce97f5c0d674c61a2.png)处的特征函数值相匹配。通常后者选择会得到更好的结果。观察上面的积分函数，可以直接发现算法在深度实值/深度虚值期权中的一个弱点。在这种情况下，由于术语

![e^{i u \left(\ln\frac{S}{K}+(r-q)T\right) }](img/c95782add722b2cd78bc791fc29f32c0.png)。

第二，当使用 Gauss-Laguerre 规则时，权重函数![e^{-x}](img/a7b767139add140fb7f9e058e1b2c60c.png)与特征函数的重叠对于非常短期的到期时间或小的有效波动性来说是最优的，正如 Black-Scholes 特征函数所示。

第三，对于非常小的![\sigma](img/d2e0f91b4f9ab5cb8554a898295d118c.png)，积分的函数容易受到减法抵消误差的影响。

最后一个问题通过使用归一化特征的二阶泰勒展开很容易克服，对于小的![\sigma](img/d2e0f91b4f9ab5cb8554a898295d118c.png)。相应的 mathematica 脚本可以在[这里](https://github.com/klausspanderen/HestonExponentialFitting/blob/master/mathematica/heston_expansion.nb)看到。

通过将积分变量重新缩放，可以改进第二个问题，通过将积分用![x = \eta u](img/aaa4b05fd0f4251b2e8b4322a68243d5.png)来重写。

![\eta = \max\left(0.01, \min\left(10, \frac{1}{\sqrt{8(1-e^{-\kappa t})(v_0-\theta)/\kappa + \theta t}}\right)\right)](img/37a3840bc771ff92fefd01cd3710538c.png)。

第一个问题，高度振荡的积分函数，可以通过指数拟合的 Gauss-Laguerre 规则[4]来解决。两个平滑函数![f_1(x)](img/d26f9fea14d5215d3872120b2ef2e310.png)和![f_2(x)](img/1aaf37be720215aa70469f5af7a0b725.png)的数值积分。

![I = \displaystyle \int_0^\infty e^{-x} \left(f_1(x) \sin(\mu x) + f_2(x)\cos(\mu x)\right)\mathrm{dx} = \int_0^\infty f(x)\mathrm{dx}](img/23ee0cb51a20b23dd34c239da90cec50.png)。

近似由 Gauss-Laguerre 规则的形式表示。

![I \approx \sum_i^N w_i(\mu) f(x_i(\mu))](img/9490e276005995b211909e54b860be4f.png)是

![\mu =\ln\frac{S}{K}+(r-q)T](img/4ac3514d108ed8c8a2811a2f135cacdf.png)。

以及高斯-拉盖尔数值积分规则的权重![w_i](img/fc546c6cc29bfda565ce1c16bbda3848.png)和节点![x_i](img/8f45c962de64c5d9724b2cce9f75df2f.png)成为频率![\mu](img/9490e276005995b211909e54b860be4f.png)的函数。在[4]中概述的算法运行时太慢，在原始形式下只能用于![N=8](img/0713bd8b396423b556897fa9d49a54b1.png)。为了使用它进行 Heston 模型，我们预计算了一组定义的频率![\{0 \leq \mu_i\ \leq 50\}](img/62ec5a82721242219a2e00f6e98f72e9.png)的权重和节点。对于给定的频率![\mu](img/9490e276005995b211909e54b860be4f.png)，最接近的预计算值![\mu_j](img/a075e75d60cc4f53293bd6afce89bbcb.png)被用来评估积分。当然，使用![\mu](img/9490e276005995b211909e54b860be4f.png)的权重和节点而不是![\mu_j](img/a075e75d60cc4f53293bd6afce89bbcb.png)

要有更大的预计算权重和节点 N，有两种关键技术：

+   从![\mu=0](img/bb64a3927666587e35cae58f72986038.png)开始算法，以获得标准高斯-拉盖尔权重/节点，然后缓缓增加![\mu](img/9490e276005995b211909e54b860be4f.png)。使用前 20 步的旧权重和节点，基于拉格朗日插值多项式生成牛顿求解器的下一个起始向量。

+   通过使用[boost 多精度](https://www.boost.org/doc/libs/1_73_0/libs/multiprecision/doc/html/index.html)包而不是双精度来增加“数值头部空间”。这仅与预计算有关。最终权重和节点以正常双精度值存储。

生成指数拟合高斯-拉盖尔数值积分规则的权重和节点的源代码[在此处](https://github.com/klausspanderen/HestonExponentialFitting/blob/master/exponential_fitting/ef_laguerre.cpp)可用。

使用[boost 多精度版本](https://github.com/klausspanderen/HestonExponentialFitting/tree/master/ql/pricingengines/vanilla)的 Gauss-Laguerre 定价算法生成了与其他 Heston 定价方法比较的参考结果，该算法阶数为*N=2000*。与*N=1500*和*N=2500*的结果比较确保了结果的正确性。指数拟合高斯-拉盖尔数值积分规则总是使用*N=48*个节点，对应于仅对特征函数进行 48 次估值。第一个示例模型是

![\公式 s=1.0, t=1,v_0=0.04, \kappa=2.5,\theta=0.06, \sigma=0.75,\rho=-0.1](img/fc92c2c5ac5ac355b3324dcdf80f6f03.png)

![expfit1](img/0233d07d373e9a6c45d459bce0c5a662.png)

指数拟合方法在考虑特征函数估值的总数时尤其优于其他方法。正如预期的那样，该方法对于深度 OTM/ITM 期权表现得非常出色，并确保绝对定价误差保持在![10^{-15}](img/b76a7a9e0092f8a1913e4d5d37865b4f.png)以下，适用于非常广泛的期权行权价范围。下一轮，模型不变，但![t =10, \rho=-0.75](img/754f2fb61d8e11bf7428bb3041e6c452.png)。

![expfit2](img/24387e0011045ffeeb56233722bd752b.png)

指数拟合的定价误差再次保持在![10^{-14}](img/cf2338e02a673f39f00df3fce4773674.png)以下，适用于-15 到 15 的所有资金度之间，远低于其他方法。下一次测试，模型不变，但非常短的到期时间![t=\frac{1}{365}](img/78da107c5367e1a2a9c4c741ed684464.png)。COS 方法与 250 次特征函数调用和指数拟合*N=48*相近，并且优于所有其他方法。

![expfit3](img/ca20cde3ef864d62a225515509875fe6.png)

以下文档中展示了各种不同 Heston 参数在文献中的应用情况。[文档](https://hpcquantlib.files.wordpress.com/2020/05/heston_catalog-3.pdf)。仅用 64 个节点的指数拟合高斯-拉格朗日数值积分规则解决了问题，对于-20 到 20 的资金度和一天到 10 年的到期时间，误差![\epsilon < 10^{-13}](img/3fa7f83a92a6d80baab287cade1b3b38.png)以内，并且优于其他方法，尤其是在考虑所需特征函数调用次数时。此方法也可以扩展到更多的节点。

算法在 QuantLib 中的实现是[PR#812](https://github.com/lballabio/QuantLib/pull/812)的一部分。

[1] Lewis, A. [A simple option formula for general jump-diffusion and other exponential Lévy processes](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=282110)

[2] F. Le Floc’h, [Fourier Integration and Stochastic Volatility Calibration.](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2362968)

[3] L. Andersen, and V. Piterbarg, 2010,  利率建模，第一卷：基础和 vanilla 模型，  大西洋金融出版社伦敦。

[4] D. Conte, L. Ixaru, B. Paternoster, G. Santomauro, [Exponentially-fitted Gauss–Laguerre quadrature rule for integrals over an unbounded interval.](https://www.sciencedirect.com/science/article/pii/S0377042713003385)
