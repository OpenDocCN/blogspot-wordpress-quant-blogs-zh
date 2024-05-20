<!--yml
category: 未分类
date: 2024-05-17 23:32:07
-->

# Fokker-Planck Forward Equation for the Heston Model – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2013/02/10/fokker-planck-forward-equation-for-the-heston-model/#0001-01-01](https://hpcquantlib.wordpress.com/2013/02/10/fokker-planck-forward-equation-for-the-heston-model/#0001-01-01)

Consider the stochastic differential equation of the Heston model for the dynamics of the log-spot ![x_t = \ln S_t](img/16f746d6b95837f7e9cfec20abd14a6d.png)

![\begin{array}{rcl} dx_t &=& \left(r_t - q_t - \frac{\nu_t}{2}\right)dt + \sqrt\nu_t dW^{x}_t \nonumber \\ d\nu_t&=& \kappa\left(\theta-\nu_t \right ) dt + \sigma\sqrt\nu_t dW^{\nu}_t \nonumber \\ \rho dt &=& dW^{x}_tdW^{\nu}_t \end{array} ](img/53a92059f4ae5536232c2c5457f4c828.png)

The Fokker-Planck partial differential forward equation describes the time evolution of the probability density function ![p(x_t,\nu_t,t)](img/a8ed804ebd6f4de152f21323df199521.png)

![\frac{\partial p}{\partial t} = \frac{1}{2}\frac{\partial^2}{\partial x^2}(\nu p) + \frac{\partial^2}{\partial x \partial \nu} (\rho\sigma\nu p) + \left(\frac{\nu}{2} -r_t+q_t\right)\frac{\partial}{\partial x} p + \frac{\sigma^2}{2}\frac{\partial^2}{\partial \nu^2}(\nu p) - \frac{\partial}{\partial \nu}\left(\kappa\left(\theta-\nu \right ) p\right) ](img/213b494588ce90f2ab6725cb349bc52d.png)

with the initial condition

![p(x,\nu,t=0) = \delta(x-x_0)\delta(\nu-nu_0) ](img/2a97247fba0ae47fa73e458cffe40f0e.png)

where ![\delta](img/1367ac0656a0a771a7b2a9480c1a7e6f.png) denotes the Dirac delta distribution. A semi-closed form solution for this problem is presented in [1]. When solving the Fokker-Planck forward equation special care must be taken with respect to the boundary conditions, especially if the Feller constraint

![\sigma^2 \le 2\kappa\theta](img/93659630c1c3500de6d47b5e11f2bd05.png)

is violated. In this case the boundary at the origin ![\nu = 0](img/5e7becccce05c432fbb22a2f1c915fd5.png) is instantaneously attainable. A generalisation of Feller’s zero-flux boundary condition should be applied at the origin [2].

![\left.\left[ \frac{\sigma^2}{2}\frac{\partial}{\partial \nu} (\nu p) + \kappa(\nu-\theta)p + \rho\nu\sigma\frac{\partial p}{\partial x}\right]\right|_{\nu=0} = 0, \ \forall x\in \mathbb{R}^+ ](img/4858e2cc2e2eb5d9e31ece43e33931b2.png)

A three point forward differentiation formula can be used to calculate a second order accurate approximation of the partial derivative ![\partial_\nu](img/bea4548488ff53cf932046bc50387cfb.png) for ![\nu=0](img/b0f9e4f656181ec3176658771a8755b1.png) [3].

The diagram below shows the solution of the forward equation for the model

![\small{T=1.0, S_0=1,r=0.1, q=0.05, \kappa=2.0, \theta=0.4, \rho=-0.75, v_0=1.2, \sigma=0.4}](img/ff9030e7a12cd4832cb29c4396cebaf0.png)

[![plot.399](img/73bed71852a5b2f6f645ac41b509ab60.png)](https://hpcquantlib.wordpress.com/wp-content/uploads/2013/02/plot-399.png)

The Feller constraint is violated for ![\sigma=2.0](img/a011583fe3d04361e0b8d1aae28b2bb0.png) and this changes the shape of the solution completely.

[![plot.799](img/1071b912f7c57e8c3e2008d30e3fdc7d.png)](https://hpcquantlib.wordpress.com/wp-content/uploads/2013/02/plot-7992.png)The code for this example is available [here](http://hpc-quantlib.de/src/heston_fpe.zip) and it is based on the latest [QuantLib](http://quantlib.org) version from the SVN [trunk](http://sourceforge.net/p/quantlib/code/HEAD/tree/). It also depends on [RInside](http://dirk.eddelbuettel.com/code/rinside.html) and [Rcpp](http://cran.r-project.org/web/packages/Rcpp/index.html) to generate the plots. In addition the zip contains a short movie clip of the time evolution of the solution for ![\sigma=2.0](img/a011583fe3d04361e0b8d1aae28b2bb0.png).

[1] A. Dragulescu, V. Yakovenko, [Probability distribution of returns in the Heston model with stochastic volatility](http://arxiv.org/pdf/cond-mat/0203046)

[2] V. Lucic, [Boundary Conditions for Computing Densities in Hybrid Models via PDE Methods](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1191962)

[3] K. A. Kopecky, [Numerical Differentiation](http://www.karenkopecky.net/Teaching/eco613614/Notes_NumericalDifferentiation.pdf)