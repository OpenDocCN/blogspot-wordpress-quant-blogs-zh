<!--yml
category: 未分类
date: 2024-05-17 23:31:46
-->

# Probability Distribution of the Heston Model, Part I – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2014/02/04/probability-distribution-of-the-heston-model-part-i/#0001-01-01](https://hpcquantlib.wordpress.com/2014/02/04/probability-distribution-of-the-heston-model-part-i/#0001-01-01)

The Heston model is defined by the following stochastic differential equation of the log spot ![x_t = \ln S_t](img/16f746d6b95837f7e9cfec20abd14a6d.png)

![\begin{array}{rcl} dx_t &=& \left(r_t - q_t - \frac{\nu_t}{2}\right)dt + \sqrt\nu_t dW^{x}_t \nonumber \\ d\nu_t&=& \kappa\left(\theta-\nu_t \right ) dt + \sigma\sqrt\nu_t dW^{\nu}_t \nonumber \\ \rho dt &=& dW^{x}_tdW^{\nu}_t \end{array}](img/46584958a24c5f18bfc916096f9530da.png)

To a significant extent the popularity of the Heston model is based on the fact that semi-closed formulas for vanilla European options exist using the characteristic function of the model. The time evolution of the probability density function ![p(x_t, v_t, t)](img/df31c0d48a44ef0e47298b2eed31c734.png) is given by the corresponding Fokker-Planck equation [1]

![\frac{\partial p}{\partial t} = \frac{1}{2}\frac{\partial^2}{\partial x^2}(\nu p) + \frac{\partial^2}{\partial x \partial \nu} (\rho\sigma\nu p) + \left(\frac{\nu}{2} -r_t+q_t\right)\frac{\partial}{\partial x} p + \frac{\sigma^2}{2}\frac{\partial^2}{\partial \nu^2}(\nu p) - \frac{\partial}{\partial \nu}\left(\kappa\left(\theta-\nu \right ) p\right) ](img/213b494588ce90f2ab6725cb349bc52d.png)

with the initial condition

![p(x,\nu,t=0) = \delta(x-x_0)\delta(\nu-\nu_0) ](img/b527e0b4eb45f8a4ad9c56ce20e725e8.png)

The reduced probability density function

![p(x_t, t \mid x_0,\nu_0) = \int_0^\infty p(x_t, \nu_t, t) d\nu ](img/0ba3892e69cf8f478f7293e0124f328f.png)

for this initial value problem can be calculated using a semi-closed integral formula [2]

![\begin{array}{rcl} \Gamma &=& \kappa+i\rho\sigma p_x \\ \Omega &=& \sqrt{\Gamma^2 + \sigma^2\left(p_x^2-ip_x \right )} \\ p(x_t, t \mid \nu_0) &=& \int_{-\infty}^\infty \frac{dp_x}{2\pi}\exp\left( ip_x (x_t-x_0 -(r-q)t) -\nu_0 \frac{p_x^2-ip_x}{\Gamma + \Omega \coth\left(\Omega t/2 \right )} \right) \\ && \ \ \ \ \ \ \ \ \times \exp\left(-\frac{2\theta\kappa}{\sigma^2}\ln\left(\cosh\frac{\Omega t}{2} + \frac{\Gamma}{\Omega} \sinh \frac{\Omega t}{2}\right )+\frac{\kappa\Gamma\theta t}{\sigma^2} \right) \\ &=& \int_{-\infty}^\infty \frac{dp_x}{2\pi} \tilde{p}(p_x,t \mid \nu_0) \end{array} ](img/a0e49ce51c2300075a03113c80341f10.png)

This gives the opportunity to write a pricing engine for arbitrary European payoffs. The value of an European option with payoff function ![P(S_t) \in \mathbb{L}^2](img/a4643d1f6af02694544a55325dd333e3.png) at maturity ![t](img/2000b896307ab7e1efa5069769a4fc7f.png) is given by

![\begin{array}{rcl} \text{npv} &=& \int_{-\infty}^\infty dx_t\int_{0}^\infty d\nu_t P(S_0 e^{x_t+(r_t-q_t)t})e^{-r_t t} p(x_t,\nu_t,t) \\ &=& e^{-r_t t}\int_{-\infty}^\infty dx_t P(S_0 e^{x_t+(r_t-q_t)t})p(x_t,t \mid x_0,\nu_0) \end{array} ](img/c44eeb9679de198770c64b68be6cdb95.png)

The calculation needs two nested integrations which can be carried out efficiently using e. g. the Gauss-Lobatto algorithm. The solution of the equation

![| \tilde{p}(p_x, t \mid \nu_0)| = \text{QL\_EPSILON} ](img/9236fe43b037fa7d8e9158f6287451d8.png)

determines the upper boundary for the integration over ![p_x](img/c4c47f747af6babb42cd5beaf9714d28.png). The boundaries ![\left[ -x_{min}, x_{max}\right]](img/af88cd3b4874253b43d38bd4a82f60d4.png) for the integration over ![x_t](img/7a6c51eeafde57877526801e4a5da1e1.png) are chosen such that the interval covers ten times the expected variance

![-x_{min} = x_{max}=10\sqrt{\int_0^{t}E\left[ \nu_t \right ] dt} = 10\sqrt{\theta t + \frac{1}{\kappa}\left(\nu_0-\theta\right)\left(1-e^{-\kappa t}\right)} ](img/15e9152f288eefbbe042d319860f3014.png)

Obviously the nested integration makes this algorithm more tricky than the standard ways to price plain vanilla European options but it is not limited to vanilla payoffs. The implementation of this algorithm can be found [here](https://github.com/lballabio/quantlib/blob/master/QuantLib/ql/experimental/exoticoptions/analyticpdfhestonengine.cpp) within the [QuantLib trunk on Github.](https://github.com/lballabio/quantlib)

Broadie and Kaya [1] have outlined an algorithm to sample from the full probability density function ![p(x_t, \nu_t, t \mid x_0, \nu_0)](img/795feb8d1730fcdebca8e5685996535a.png) instead of the reduced density function ![p(x_t, t \mid x_0, \nu_0)](img/2601d3bb2ca9f248bd2328bbdaf6cd88.png). Starting point for this algorithm is the exact solution of the Heston stochastic differential equation

![\begin{array}{rcl} x_t &=& x_o + (r_t-q_t)t - \frac{1}{2}\int_0^t \nu_s ds + \rho\int_0^t \sqrt{\nu_s} dW_s^{(1)} + \sqrt{1-\rho^2}\int_0^t \sqrt{\nu_s} dW_s^{(2)} \nonumber \\ \nu_t &=& \nu_0 + \kappa\theta t - \kappa \int_0^t \nu_s ds + \sigma \int_0^t\sqrt{\nu_s}dW_s^{(1)} \nonumber \end{array} ](img/2d25b3feec7844e7e2801c13266bb545.png)

The probability density function of the variance process ![\nu_t](img/c56c88dfcf2d52e0221304d7c3dd90f9.png) is given by a noncentral chi-squared distribution

![\nu_t = \frac{\sigma^2\left( 1-e^{-\kappa t}\right)}{4\kappa}\chi_d^{'2}\left(\frac{4\kappa e^{-\kappa t}}{\sigma^2\left(1-e^{-\kappa t}\right)}\nu_0\right), d=\frac{4\theta\kappa}{\sigma^2} ](img/1497d56b7ebf62bc762b5c90fea44c2f.png)

The distribution ![\Psi(0,t)](img/a0b973bcc2db185a64bf978280bd893d.png) of the integral ![\int_0^t \nu_s ds](img/787aff30b276853cbb00259a1e526614.png) conditional on ![\nu_t](img/c56c88dfcf2d52e0221304d7c3dd90f9.png) and ![\nu_0](img/c15610bd2db7c127cda5ec48aff90fe0.png) can be calculated via the characteristic function

![\begin{array}{rcl} \text{Pr}(\Psi(t) \le x)&=& \frac{2}{\pi}\int_0^\infty \frac{\sin ux}{u}\text{Re}(\Phi(u)) du \\ \\ \Phi(a)&=& \frac{\gamma(a)e^{-\frac{1}{2}(\gamma(a)-\kappa)t} \left(1-e^{-\kappa t}\right)} {\kappa\left(1-e^{\gamma(a)t}\right)} \exp\left( \frac{\nu_t+\nu_0}{\sigma^2} \left[ \frac{\kappa\left(1+e^{-\kappa t}\right)}{1-e^{-\kappa t}} - \frac{\gamma(a)\left(1+e^{-\gamma(a)t}\right)}{1-e^{-\gamma(a)t}} \right] \right) \\ && \times \frac{I_{0.5d-1} \left( \sqrt{\nu_0\nu_t} \frac{4\gamma (a) e^{-0.5\gamma(a)t}}{\sigma^2\left(1-e^{-\gamma(a)t}\right)}\right)}{ I_{0.5d-1} \left( \sqrt{\nu_0\nu_t} \frac{4\kappa e^{-0.5\kappa t}}{\sigma^2\left(1-e^{-\kappa t}\right)}\right)} \\ && \times \frac{\exp\left((0.5d-1) \left[-\frac{1}{2}\gamma(a)t + \ln \frac{\gamma(a)}{1-e^{-\gamma(a)t}} \right]\right)}{\left(\frac{\gamma(a) e^{-0.5\gamma(a)t} }{ 1-e^{-\gamma(a)t}}\right)^{0.5d-1}} \\ \\ \gamma(a)&=&\sqrt{\kappa^2-2 i \sigma^2 a} \end{array} ](img/e6f33792cf83abd053d4dab3d5e29c73.png)

The modified Bessel function of first kind ![I_{0.5d-1}(z)](img/a0bcb8c3ace69aabee7680c3752123d7.png) can be evaluated using series expansion for small and medium ![|z|](img/a4465645dc8651912632fff921e5438e.png) or asymptotic approximation for large ![|z|](img/a4465645dc8651912632fff921e5438e.png) [5]. Unfortunately Boost provides only real versions of the Bessel functions and the copyright status of older complex valued Fortran77 routine is vague. Therefore QuantLib comes with its own [implementation](https://github.com/lballabio/quantlib/blob/master/QuantLib/ql/math/modifiedbessel.cpp).

Please notice that ![\Phi(a)](img/61ee75f762045b293ef1497ab4bbf4b3.png) is already a continuous version of the characteristic function and therefore the integration does not need to track the branches of ![arg(z)](img/bae1589c039eef2a61ad369f26fa4ed6.png) when calculating the complex valued Bessel function [4].

The integration over the characteristic function is best done using either Gauss-Laguerre, Gauss-Lobatto or trapezoidal rule. The two later algorithms need to truncate the integration at some upper bound. First guess for a truncation limit can be taken from the [Cornish-Fisher expansion](http://en.wikipedia.org/wiki/Cornish%E2%80%93Fisher_expansion)  for some very small ![\epsilon](img/361dcef49d79b59b4e3688e587851f00.png). The moment-generating function ![\Phi(a)](img/61ee75f762045b293ef1497ab4bbf4b3.png) can be used to get the first, second and third moment of the distribution via finite difference quotient.

![m_n = E(X^n) = \frac{d^n}{dy^n}\Phi(x+iy)\Big|_{x=y=0} ](img/002ab31ec2e1050dbd06e69994cccb3b.png)

The next term is now fairly easy to calculate

![\int_0^t \sqrt{\nu_s} dW_s^{(1)} = \frac{1}{\sigma}\left( \nu_t - \nu_0 - \kappa\theta t+\kappa \int_0^t \nu_s ds \right)](img/7267877f4d99017b43f88c0d8f899aa2.png)

The log spot process can now be sampled using a standard normal random variable ![Z](img/051625cbd82ebd99476330b3cd2e1917.png) and

![\begin{array}{rcl} x_t &=& x_0 + m(t) + \sigma(t)Z \nonumber \\ \sigma^2(t) &=& (1-\rho^2)\int_0^t \nu_s ds \nonumber \\ m(t) &=& (r_t-q_t)t - \frac{1}{2}\int_0^t \nu_s ds + \rho\int_0^t \sqrt{\nu_s}dW_s^{(1)} \nonumber \end{array} ](img/6db99810e6b4d284694229a18ee87066.png)

This sampling algorithm is exact even for very large time steps and therefore gives some advantages for quasi random Monte-Carlo methods but the inversion of the integration of the characteristic function is also very slow. The algorithm is implemented within the [HestonProcess](https://github.com/lballabio/quantlib/blob/master/QuantLib/ql/processes/hestonprocess.cpp) class.

[1] I. Clark, [Foreign Exchange Option Pricing: A Practitioners Guide](http://books.google.de/books?id=7vua-0-2sgMC&pg=PT130&lpg=PT130&dq=heston+model+fokker+planck+equation&source=bl&ots=nHutgX1qSu&sig=2FFDK3WVot5LSxBldfE5VoYCZKc&hl=de&sa=X&ei=R_3kUvDpBoWEtAb0xIHYAQ&ved=0CEwQ6AEwAg#v=onepage&q=heston%20model%20fokker%20planck%20equation&f=false), p. 113

[2] A. Dragulescu, V. Yakovenko, [Probability distribution of returns in the Heston model with stochastic volatility](http://arxiv.org/pdf/cond-mat/0203046.pdf)

[3] M. Broadie, Ö. Kaya, [Exact Simulation of Stochastic Volatility and other Affine Jump Diffusion Processes](http://finmath.stanford.edu/seminars/documents/Broadie.pdf)

[4] R. Lord, [Efficient pricing algorithms for exotic derivatives](http://www.google.de/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&ved=0CDwQFjAC&url=http%3A%2F%2Frepub.eur.nl%2Fpub%2F13917%2FLordR-Thesis.pdf&ei=49nwUsreLYjnswbZ2IHIDQ&usg=AFQjCNFWjTcnOft7cgo_0q-VDDhUaS1YUA&bvm=bv.60444564,d.Yms), p. 40

[5] J.R. Culham, [Bessel Functions of the First and Second Kind](http://www.mhtlab.uwaterloo.ca/courses/me755/web_chap4.pdf)