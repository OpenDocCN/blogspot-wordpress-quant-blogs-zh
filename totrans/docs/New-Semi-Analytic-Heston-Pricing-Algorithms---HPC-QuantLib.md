<!--yml
category: 未分类
date: 2024-05-13 00:12:49
-->

# New Semi-Analytic Heston Pricing Algorithms – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2017/05/07/newer-semi-analytic-heston-pricing-algorithms/#0001-01-01](https://hpcquantlib.wordpress.com/2017/05/07/newer-semi-analytic-heston-pricing-algorithms/#0001-01-01)

The pricing engines for the Heston model in QuantLib have aged a bit. Meanwhile newer and better algorithms have been developed and discussed in the literature. For a comprehensive review please see [1][2]. Time to refurbish the existing engines.

The Heston model is defined by the following stochastic differential equation of the log spot

![\begin{array}{rcl} d \ln S_t&=& \left(r_t - q_t - \frac{\nu_t}{2}\right)dt + \sqrt\nu_t dW^{S}_t \nonumber \\ d\nu_t&=& \kappa\left(\theta-\nu_t \right ) dt + \sigma\sqrt\nu_t dW^{\nu}_t \nonumber \\ \rho dt &=& dW^{S}_tdW^{\nu}_t \end{array}](img/7bb998b60af889698cbc7da23e39455e.png)

The normalized characteristic function in the Gatheral formulation is given by

![\phi_t(z) = \exp\left\{\frac{v_0}{\sigma^2}\frac{1-e^{-Dt}}{1-Ge^{-Dt}}\left(\kappa-i\rho\sigma z-D\right) + \frac{\kappa\theta}{\sigma^2}\left(\left(\kappa-i\rho\sigma z-D\right)t-2\ln\frac{1-Ge^{-Dt}}{1-G}\right) \right\}](img/579b82b565b9de252e33440e65e2414a.png)

![\begin{array}{rcl} D&=&\sqrt{\left(\kappa - i\rho\sigma z\right)^2+\left(z^2+iz\right)\sigma^2} \nonumber \\ G&=&\displaystyle\frac{\kappa -i\rho\sigma z-D}{\kappa -i\rho\sigma z + D}\end{array}](img/e77612059b60e5dc57ad01a117bfe2f4.png)

Andersen and Piterbarg [3] introduced a Black-Scholes control variate to improve the numerical stability of Lewis’s formula (2001) for the price of a vanilla call option

![\begin{array}{rcl} C(S_0, K, T)&=&BS\left(S_0, K, T, \sigma_{BS}\right) \nonumber \\ &+& \frac{\sqrt{Se^{(r-q)t}K}e^{-rt}}{\pi}\displaystyle\int\limits_{0}^{\infty}{\Re\left( \frac{\phi^{BS}_T\left(u-\frac{i}{2}\right) - \phi_T\left(u-\frac{i}{2}\right)}{u^2+\frac{1}{4}} e^{i u \left(\ln\frac{S}{K}+(r-q)T\right) } \right)  \mathrm{d}u}\end{array}](img/1de9ba5864c76669e051677209a00460.png)

with the Black-Scholes price ![BS\left(S_0, K, T, \sigma_{BS}\right)](img/7a540b78e38573509ae5522e932ac68c.png) of a vanilla call option with volatility ![\sigma_{BS}](img/babcd5b93d361ec65726e3dbaf6fcdd0.png) and the characteristic function

![\phi^{BS}_T(z)=e^{-\frac{1}{2}\sigma_{BS}^2 T (z^2 + iz)} ](img/af848a6610ddd0dcd89bc0f92e65175c.png)

Different proposals for the volatility of the vanilla option have been brought up in order to achieve an optimal control variate:

*   ![\sigma_{BS}^2 = \nu_0](img/7ac94af4c1aca949bf2c55faccc14ca3.png)
*   ![\sigma_{BS}^2 = \frac{1}{\kappa t}\left(1-e^{-\kappa t}\right)\left(\nu_0-\theta\right) + \theta](img/b6298ad4724d204bf2a507c70d4d1660.png)
*   ![\sigma_{BS}^2 = c_2](img/31b7724e5a2431897429fcdb04d930d4.png) with ![c_2](img/8de07e0ce5a8488d46add26b04e95db8.png) the second cumulant of ![\ln \frac{F}{K}](img/09fe352c30db9e119e89321c5cd029ca.png) [1].

The diagram below shows the resulting integrand for the different control variate volatilities, the Heston model parameters

![r=7.5\%, q=5\%, S_0=100, \nu_0=0.08, \rho=-80\%,\sigma=0.5, \kappa=4, \theta=0.05](img/57eebc588a72bbdd75f87f40fd528bab.png)

and for a vanilla call option with strike ![K=200](img/41aca03c616c2e5f4eb5072f3a4ae864.png) and maturity ![t=2.0](img/55d255484c530b33eb2c8decec022c12.png).

![control_variate](img/f9f0a0d654821d2c2f0d96b6cb74b816.png)

The best choice depends on the Heston- and option parameters but it seems that

![\sigma_{BS}^2 = \frac{1}{\kappa t}\left(1-e^{-\kappa t}\right)\left(\nu_0-\theta\right) + \theta](img/b6298ad4724d204bf2a507c70d4d1660.png)

is a good option for a large variety of parameters. A direct comparison of the integrand with and without control variate shows how effective the control variate is.

![control_comparison](img/0f5cfe684756355c37ad462e29d55bd5.png)

The central trick of Andersen-Piterbarg is now to truncate Lewis’s infinite integral at a finite ![u_{max}](img/a86dcfd76fe79e4ff4fdf256bc0a91d6.png) such that the remaining part is smaller than a given threshold based on the following inequation

![\displaystyle\int_{u_{max}}^\infty \left\vert \frac{\phi_B(u-\frac{i}{2}) - \phi(u-\frac{i}{2})}{u^2+\frac{1}{4}} \right\vert du \le e^{-C_\infty u_{max}}\displaystyle\int_{u_{max}}^\infty \frac{1}{u^2} du](img/128518b9a8a2e17563f3f17706aa3cf7.png)

Please see the original paper or [2] for further details on how to get from here to an algorithm for ![u_{max}](img/a86dcfd76fe79e4ff4fdf256bc0a91d6.png), especially for short dated options.

As Andersen and Piterbarg have pointed out, the simple trapezoidal rule works surprisingly well to carry out the resulting integral if a control variate is used. Alan Lewis’s [test cases](https://forum.wilmott.com/viewtopic.php?f=34&t=90957&hilit=heston#p620396) with high precision Heston reference prices should serve as a test bed here, in particular the call with strike 100\. The Gauss-Laguerre method is very thankful for this particular test case but the point here is that the trapezoidal rule converges much faster than the higher order Simpson rule or the even more complex adaptive Gauss-Lobatto method.

![convergence_speed](img/1dc2a71795ce0a21c0885efe28d60c4d.png)

The diagram below compares the recently added COS engine with the Andersen-Piterbarg method using the trapezoid rule for this test-case. The Andersen-Piterbarg method is more accurate for a similar number of points.

![convergence_comparison](img/1cb61bc3936f7a05a65f8ea18b12695e.png)

The implementation is part of the pull request [#251](https://github.com/lballabio/QuantLib/pull/251).

[1] M. Schmelzle, [Option Pricing Formulae using Fourier Transform: Theory and Application.](http://pfadintegral.com/docs/Schmelzle2010%20Fourier%20Pricing.pdf)

[2] F. Le Floc’h, [Fourier Integration and Stochastic Volatility Calibration.](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2362968)

[3] L. Andersen, and V. Piterbarg, 2010,  Interest Rate Modeling, Volume I: Foundations and Vanilla Models,  Atlantic Financial Press London.