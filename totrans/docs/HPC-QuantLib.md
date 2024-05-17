<!--yml
category: 未分类
date: 2024-05-17 23:43:36
-->

# HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com#0001-01-01](https://hpcquantlib.wordpress.com#0001-01-01)

Aim: Develop an exponentially-fitted Gauss-Laguerre quadrature rule to price European options under the Heston model, which outperforms given Gauss-Lobatto, Gauss-Laguerre and other pricing method implementations in QuantLib.

Status quo: Efficient pricing routines for the Heston model

![\begin{array}{rcl} d \ln S_t&=& \left(r_t - q_t - \frac{\nu_t}{2}\right)dt + \sqrt\nu_t dW^{S}_t \nonumber \\ d\nu_t&=& \kappa\left(\theta-\nu_t \right ) dt + \sigma\sqrt\nu_t dW^{\nu}_t \nonumber \\ \rho dt &=& dW^{S}_tdW^{\nu}_t \end{array}](img/7bb998b60af889698cbc7da23e39455e.png)

are based on the integration over the normalized characteristic function in the Gatheral formulation

![\phi_t(z) = \exp\left\{\frac{v_0}{\sigma^2}\frac{1-e^{-Dt}}{1-Ge^{-Dt}}\left(\kappa-i\rho\sigma z-D\right) + \frac{\kappa\theta}{\sigma^2}\left(\left(\kappa-i\rho\sigma z-D\right)t-2\ln\frac{1-Ge^{-Dt}}{1-G}\right) \right\}](img/579b82b565b9de252e33440e65e2414a.png)

![\begin{array}{rcl} D&=&\sqrt{\left(\kappa - i\rho\sigma z\right)^2+\left(z^2+iz\right)\sigma^2} \nonumber \\ G&=&\displaystyle\frac{\kappa -i\rho\sigma z-D}{\kappa -i\rho\sigma z + D}\end{array}](img/e77612059b60e5dc57ad01a117bfe2f4.png)

in combination with a Black-Scholes control variate to improve the numerical stability of Lewis’s formula [1][2][3]. The normalized characteristic function of the Black-Scholes model is given by

![\phi^{BS}_T(z)=e^{-\frac{1}{2}\sigma_{BS}^2 T (z^2 + iz)} ](img/af848a6610ddd0dcd89bc0f92e65175c.png)

and the price of a vanilla call option can then be calculated based on

![\begin{array}{rcl} C(S_0, K, T)&=&BS\left(S_0, K, T, \sigma_{BS}\right) \nonumber \\ &+& \frac{\sqrt{Se^{(r-q)T}K}e^{-rT}}{\pi}\displaystyle\int\limits_{0}^{\infty}{\Re\left( \frac{\phi^{BS}_T\left(u-\frac{i}{2}\right) - \phi_T\left(u-\frac{i}{2}\right)}{u^2+\frac{1}{4}} e^{i u \left(\ln\frac{S}{K}+(r-q)T\right) } \right)  \mathrm{d}u}\end{array}](img/a29f81e4c4761634ab7b01cd74092f2a.png)

where ![BS\left(S_0, K, T, \sigma_{BS}\right)](img/7a540b78e38573509ae5522e932ac68c.png) is the corresponding Black-Scholes price. Different choices for the volatility of the control variate are discussed in the literature. For the following examples the volatility will be defined by either

![\sigma_{BS}^2 = \frac{1}{\kappa T}\left(1-e^{-\kappa T}\right)\left(\nu_0-\theta\right) + \theta](img/789c0caab2971ab81c62176376e538cc.png)

or

![\displaystyle \sigma_{BS}^2 = -\frac{8}{T} \ln{\Re\left(\phi_T\left(-i/2\right)\right)}](img/51ac91fa5db2e8bbe7beb5d4cbb63e69.png).

The first one matches the overall variance for ![\sigma=0](img/34a8165faaaa3fe8484c329f7064507e.png) whereas the latter one matches the values of the characteristic functions at the starting point ![z=-i/2](img/06d58b4dcf2b1cfce97f5c0d674c61a2.png) of the integration. Usually the latter choice gives better results. Looking at the integrand above one can directly spot a weak point in the algorithm for deep in the money/deep out of the money options. In this case the integrand becomes a highly oscillating function due to the term

![e^{i u \left(\ln\frac{S}{K}+(r-q)T\right) }](img/c95782add722b2cd78bc791fc29f32c0.png).

Second, when using Gauss-Laguerre quadrature the overlap of the weight function ![e^{-x}](img/a7b767139add140fb7f9e058e1b2c60c.png) with the characteristic function becomes sub-optimal for very short maturities or small effective volatilities as can be seen with the Black-Scholes characteristic function already.

Third, for very small ![\sigma](img/d2e0f91b4f9ab5cb8554a898295d118c.png) the integrand becomes prone to subtractive cancellation errors.

The last issue is easy to overcome by using the second order Taylor expansion of the normalized characteristic for small ![\sigma](img/d2e0f91b4f9ab5cb8554a898295d118c.png). The corresponding mathematica script can be seen [here](https://github.com/klausspanderen/HestonExponentialFitting/blob/master/mathematica/heston_expansion.nb).

Rescaling the integrand improves the second issue by rewriting the integral in terms of ![x = \eta u](img/aaa4b05fd0f4251b2e8b4322a68243d5.png) with

![\eta = \max\left(0.01, \min\left(10, \frac{1}{\sqrt{8(1-e^{-\kappa t})(v_0-\theta)/\kappa + \theta t}}\right)\right)](img/37a3840bc771ff92fefd01cd3710538c.png)

The first problem, the highly oscillating integrand, can be tackled with the exponentially fitted Gauss-Laguerre quadrature rule [4]. The numerical integration of two smooth functions ![f_1(x)](img/d26f9fea14d5215d3872120b2ef2e310.png) and ![f_2(x)](img/1aaf37be720215aa70469f5af7a0b725.png) with

![I = \displaystyle \int_0^\infty e^{-x} \left(f_1(x) \sin(\mu x) + f_2(x)\cos(\mu x)\right)\mathrm{dx} = \int_0^\infty f(x)\mathrm{dx}](img/23ee0cb51a20b23dd34c239da90cec50.png)

is approximated by a Gauss-Laguerre quadrature rule of the form

![I \approx \sum_i^N w_i(\mu) f(x_i(\mu))](img/463444e759b201ec9eb8e38a920b7406.png).

In this use case the frequency ![\mu](img/9490e276005995b211909e54b860be4f.png) is

![\mu =\ln\frac{S}{K}+(r-q)T](img/4ac3514d108ed8c8a2811a2f135cacdf.png),

and the weights ![w_i](img/fc546c6cc29bfda565ce1c16bbda3848.png) and nodes ![x_i](img/8f45c962de64c5d9724b2cce9f75df2f.png) of the Gauss-Laguerre quadrature rule become functions of the frequency ![\mu](img/9490e276005995b211909e54b860be4f.png). The algorithm outlined in [4] is too slow to be used at runtime and in the original form only usable up to ![N=8](img/0713bd8b396423b556897fa9d49a54b1.png). In order to use it for the Heston model we pre-calculate the weights and nodes for a defined set of frequencies ![\{0 \leq \mu_i\ \leq 50\}](img/62ec5a82721242219a2e00f6e98f72e9.png). The closest pre-calculated value ![\mu_j](img/a075e75d60cc4f53293bd6afce89bbcb.png) for a given frequency ![\mu](img/9490e276005995b211909e54b860be4f.png) is then used to evaluate the integral. Of course it would be optimal to use the weights and nodes for ![\mu](img/9490e276005995b211909e54b860be4f.png) instead of ![\mu_j](img/a075e75d60cc4f53293bd6afce89bbcb.png) but it is far, far better than assuming ![\mu=0](img/bb64a3927666587e35cae58f72986038.png) as it is done within the conventional Gauss-Laguerre quadrature rule.

Two techniques are key to get to larger N for the pre-calculated weights and nodes:

*   Start the algorithm with ![\mu=0](img/bb64a3927666587e35cae58f72986038.png) to get the standard Gauss-Laguerre weights/nodes and gently increase ![\mu](img/9490e276005995b211909e54b860be4f.png) afterwards. Use the old weights and nodes from the previous up to 20 steps to generate the next starting vector for the Newton solver based on the Lagrange interpolating polynomials.
*   Increase “numerical head room” by using the [boost multi-precision](https://www.boost.org/doc/libs/1_73_0/libs/multiprecision/doc/html/index.html) package instead of double precision. This is only relevant for the pre-calculation. The resulting weights and nodes are stored as normal double precision values.

The source code to generate the weights and nodes for the exponential fitted Gauss-Laguerre quadrature rule is available [here](https://github.com/klausspanderen/HestonExponentialFitting/blob/master/exponential_fitting/ef_laguerre.cpp).

The reference results for the comparison with the other Heston pricing methods are generated using a [boost multi-precision version](https://github.com/klausspanderen/HestonExponentialFitting/tree/master/ql/pricingengines/vanilla) of the Gauss-Laguerre pricing algorithm of order *N=2000*. Comparison with the results for *N=1500* and *N=2500* ensures the correctness of the results. The exponentially fitted Gauss-Laguerre quadrature rule is always carried out using *N=48* nodes, corresponding to only 48 valuations of the characteristic function. First example model is

![\displaystyle s=1.0, t=1,v_0=0.04, \kappa=2.5,\theta=0.06, \sigma=0.75,\rho=-0.1](img/fc92c2c5ac5ac355b3324dcdf80f6f03.png)

![expfit1](img/e294e1d4d28df38f78f17053ab9b2ecd.png)

Exponential fitting outperforms the other methods especially when taking the total number of characteristic function valuations into consideration. As expected the method works remarkable well for deep OTM/ITM options and ensures that the absolute pricing error stays below ![10^{-15}](img/b76a7a9e0092f8a1913e4d5d37865b4f.png) for an extremely large range of option strikes. Next round, same model but ![t =10, \rho=-0.75](img/754f2fb61d8e11bf7428bb3041e6c452.png).

![expfit2](img/7f84095748fe9957bf88ec99a5d85089.png)

Again the pricing error for exponential fitting stays below ![10^{-14}](img/cf2338e02a673f39f00df3fce4773674.png) for all moneynesses between -15 and 15 and well below the other methods. Next test, same model but very short maturity with ![t=\frac{1}{365}](img/78da107c5367e1a2a9c4c741ed684464.png). The COS-method with 250 calls of the characteristic function and exponential fitting with *N=48* are close together and outperform all other methods.

![expfit3](img/233adb00d52b683757a5db0d172aeaef.png)

The same graphs are shown for a variety of different Heston parameters being used in the literature in the following [document](https://hpcquantlib.wordpress.com/wp-content/uploads/2020/05/heston_catalog-3.pdf). The exponentially fitted Gauss-Laguerre quadrature rule with only 64 nodes solves the problem almost always with ![\epsilon < 10^{-13}](img/3fa7f83a92a6d80baab287cade1b3b38.png) for moneynesses between -20 and 20 and maturities between one day and 10 years and outperforms the other methods, especially when taking the number of characteristic function calls needed into consideration. This method can also be extend to larger number of nodes.

The QuantLib implementation of the algorithm is part of the [PR#812](https://github.com/lballabio/QuantLib/pull/812).

[1] Lewis, A. [A simple option formula for general jump-diffusion and other exponential Lévy processes](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=282110)

[2] F. Le Floc’h, [Fourier Integration and Stochastic Volatility Calibration.](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2362968)

[3] L. Andersen, and V. Piterbarg, 2010,  Interest Rate Modeling, Volume I: Foundations and Vanilla Models,  Atlantic Financial Press London.

[4] D. Conte, L. Ixaru, B. Paternoster, G. Santomauro, [Exponentially-fitted Gauss–Laguerre quadrature rule for integrals over an unbounded interval.](https://www.sciencedirect.com/science/article/pii/S0377042713003385)