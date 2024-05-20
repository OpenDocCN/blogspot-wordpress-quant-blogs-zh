<!--yml
category: 未分类
date: 2024-05-17 23:30:53
-->

# Richardson Extrapolation for American Options – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2012/06/10/richardson-extrapolation-for-american-options/#0001-01-01](https://hpcquantlib.wordpress.com/2012/06/10/richardson-extrapolation-for-american-options/#0001-01-01)

Popular finite difference schemes like the one-dimensional Crank-Nicholson scheme or multi dimensional operating splitting methods like the Hundsdorfer-Verwer scheme often achieve second order convergence in ![\Delta t](img/35bff8105c8314c62070030cd46f8a1c.png) for typical partial differential equations in financial engineering. Unfortunately if these schemes are used together with dynamic programming to price America options the second order convergence is destroyed by the first order convergence of the dynamic programming step.

The Richardson extrapolation is a simple numerical gem to increase the convergence order of a numerical method. Say a numerical method has the following convergence behavior

![f(\Delta t) = f_0 + \alpha \cdot (\Delta t)^n + O((\Delta t)^{n+1}) ](img/9494255d5ef2da3a60d4f8ecc90f202e.png) .

Please note that this is a more restrictive requirement than to assume that the numerical method is of order *n* because ![\alpha](img/86ceb19e0d1d39c689d6601fd46650ae.png) does not depend on ![\Delta t](img/35bff8105c8314c62070030cd46f8a1c.png). Now the formula

![R(x, \Delta t) = \frac{x^n f\left(\frac{\Delta t}{x}\right)-f(\Delta t)}{x^n-1} = f_0 + O((\Delta t)^{n+1}) ](img/61a914424f58647e72dd50ef590106bd.png)

also has

![\lim_{\Delta t\rightarrow 0} R(x,\Delta t) = f_0 ](img/e122534998d71446282043df314626fe.png)

but the order of convergence of ![R(x, \Delta t)](img/df54f5183a31ab276e6f5e360d3f01c6.png) is  *n+1*. The order does not depend on the particular value of *x* but often *x* is chosen to be two. This simple trick can be extended to the case where *n* is unknown or the Richardson extrapolation can be used *m* times to increase the order of convergence to *n+m* [2].

Lets apply the Richardson extrapolation to the pricing of an American Put under the Heston stochastic differential equation. The corresponding partial differential equation

![0 = \frac{\partial u}{\partial t} + \frac{1}{2}S^2v\frac{\partial^2 u}{\partial S^2}+\rho\sigma S\nu \frac{\partial^2 u}{\partial S\partial \nu} + \frac{1}{2}\sigma^2\nu \frac{\partial^2 u}{\partial \nu^2} + rS\frac{\partial u}{\partial S} + \kappa(\theta - \nu)\frac{\partial u}{\partial \nu} -r u ](img/95a5ff3857be332a7e1487df4894904e.png)

is solved using the Hundsdorfer-Verwer scheme [1]. The early exercise condition is impressed using dynamic programming after every time step. The parameters of the experiment are

![\small{T=1, K=10, S_0=11, r=0.1, \nu_0=0.0625, \kappa=5, \theta=0.16, \sigma=0.9, \rho=0.1}](img/8a9ceb6a6ee6b2ceb9928f4cbbb88408.png) .

As can be seen in the diagram below even though the Richardson extrapolation is a simple formula it increases the convergence by one order from *1.0* to approx. *2.1*. If the order is not known a priori then the resulting order is still *1.4*.

[![](img/3d4df409c8ec94324b1bfe0fa6178781.png "plot")](https://hpcquantlib.wordpress.com/wp-content/uploads/2012/06/plot.png)

The source code is available [here](http://hpc-quantlib.de/src/richardson.zip). It depends on the latest QuantLib version from the [SVN trunk](http://sourceforge.net/p/quantlib/code/HEAD/tree/).

[1] Karel in ’t Hout, [ADI finite difference schemes for the Heston model with correlation.](http://win.ua.ac.be/~kihout/ADI_Heston_lecture.pdf)

[2] Eric Hung-Lin Liu, [Fundamental Methods of Numerical Extrapolation with Applications](http://ocw.mit.edu/courses/mathematics/18-304-undergraduate-seminar-in-discrete-mathematics-spring-2006/projects/xtrpltn_liu_xpnd.pdf).