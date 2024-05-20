<!--yml
category: 未分类
date: 2024-05-17 23:38:39
-->

# Fokker-Planck Equation, Feller Constraint and Boundary Conditions – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2013/05/04/fokker-planck-equation-feller-constraint-and-boundary-conditions/#0001-01-01](https://hpcquantlib.wordpress.com/2013/05/04/fokker-planck-equation-feller-constraint-and-boundary-conditions/#0001-01-01)

The Fokker-Planck forward equation is an important tool to calibrate local volatility extensions of stochastic volatility models, e.g. the local vol extension of the Heston model. But the treatment of the boundary conditions – especially at zero instantaneous variance – is notoriously difficult if the Feller constraint

![\sigma^2 \le 2\kappa\theta](img/93659630c1c3500de6d47b5e11f2bd05.png)

of the square root process for the variance ![\nu ](img/055272eff19b00f433d1c4d5cb2f1743.png)

![d\nu_t = \kappa(\theta-\nu_t)dt + \sigma\sqrt{\nu_t}dW ](img/4af261bfcf0d5287fd2ea27975a5833a.png)

is violated. The corresponding Fokker-Planck forward equation

 *![\frac{\partial p}{\partial t} = \frac{\sigma^2}{2}\frac{\partial^2}{\partial \nu^2}(\nu p) - \frac{\partial}{\partial \nu}\left(\kappa\left(\theta-\nu \right ) p\right) ](img/b58a476db8bdff063eb53607c0e1c9f0.png)

describes the time evolution of the probability density function *p* and the boundary at the origin ![\nu=0 ](img/d4ad13d9f0f911ea45f9f15351ce64ff.png) is instantaneously attainable if the Feller constraint is violated. In this case the stationary solution [1] of the Fokker-Planck equation

![p_\nu = \frac{\eta^\eta}{\Gamma(\eta)}\frac{\nu^{\eta-1}}{\theta^\eta}e^{-\eta\nu/\theta},\ \eta=\frac{2\kappa\theta}{\sigma^2}](img/d887394694b61252aaa8ff46de38b6e4.png)

diverges with

![\lim_{\nu\to 0} p_\nu^{s} \sim \nu^{\eta-1} = \nu^{-\alpha},\ \alpha=1-\frac{2\kappa\theta}{\sigma^2} ](img/cf9a00ebd5b6559f676b0a2cbb10a988.png)

and the zero flow boundary condition at the origin

![\left.\left[ \frac{\sigma^2}{2}\frac{\partial}{\partial \nu} (\nu p) + \kappa(\nu-\theta)p\right]\right|_{\nu=0} = 0 ](img/0a363d806048f3f15d07d14e9f90bfd1.png)

becomes hard to track numerically. Rewriting the partial differential equation in terms of ![q_\nu = v^\alpha p_\nu](img/4ab282ce2879403aab30aae349f96e54.png) helps to mitigate the problem [2].

![\frac{\partial q}{\partial t} = \nu\frac{\sigma^2}{2}\frac{\partial^2}{\partial \nu^2} q + \kappa(\nu+\theta)\frac{\partial}{\partial \nu}q + \frac{2\kappa^2\theta}{\sigma^2}q ](img/2d758c4bd2f314a097974730bb6d8b6a.png)

The corresponding zero flow boundary condition in *q* reads as follows

![\left.\left[ \nu\frac{\sigma^2}{2}\frac{\partial}{\partial \nu} q + \kappa\nu q\right]\right|_{\nu=0} = 0 ](img/1d9af5d4fcf08f5782f5c8f3da45a731.png)

The first step in order to apply the boundary condition is to discretize the transformed Fokker-Planck equation in space direction on a non-uniform grid ![\nu_i](img/c12f6546d6c0d88be936cfac37126542.png)

![\frac{\partial q_i}{\partial t} = \alpha_iq_{i-1}+\beta_iq_i+\gamma_iq_{i+1]} ](img/052394286b32b6291c58862678e83ba2.png)

with

![\begin{array}{rcl} h_i &=& \nu_{i+1}-\nu_i \\ \zeta_i &=& h_{i-1}h_i \\ \zeta^p_i &=& h_i(h_{i-1}+h_i) \\ \zeta^m_i &=& h_{i-1}(h_{i-1}+h_i) \\ \alpha_i &=& \frac{1}{\zeta^m_i}\left(\sigma^2\nu_i-\kappa(\theta+\nu_i)h_i)\right) \\ \beta_i &=& \frac{1}{\zeta_i}\left( -\sigma^2\nu_i+\kappa(\theta+\nu_i)(h_i-h_{i-1}) \right ) +\frac{2\kappa^2\theta}{\sigma^2} \\ \gamma_i &=& \frac{1}{\zeta^p_i}\left( \sigma^2\nu_i + \kappa(\theta+\nu_i)h_{i-1} \right ) \end{array} ](img/0135cfe1b2b8691f89e19f28a0c4d414.png)

Next step is to discretize the zero flow boundary condition using a second order forward discretization [3] for the derivative ![\frac{\partial q}{\partial \nu}](img/11bebc0e82b87839f6f36d1430b5729b.png).

![\left.\left[ \nu\frac{\sigma^2}{2}\frac{\partial}{\partial \nu} q + \kappa\nu q\right]\right|_{\nu=\nu_{i-1}} \approx a_iq_{i-1} + b_iq_{i} + c_iq_{i+1} = 0 ](img/01399fbc2ae0d6d714bf008fc437b389.png)

with

![\begin{array}{rcl} \eta_i &=& \frac{1}{h_{i-1}h_i(h_{i-1}+h_i)} \\ a_i &=& - \eta\frac{\sigma^2}{2}\nu_{i-1}\left((h_{i-1}+h_i)^2-h_{i-1}^2 \right ) + \kappa\nu_{i-1} \\ b_i &=& \eta\frac{\sigma^2}{2}v_{i-1}\left(h_{i-1}+h_i \right )^2 \\ c_i &=& -\eta\frac{\sigma^2}{2}v_{i-1} h_{n-1}^2 \end{array} ](img/c540f2408bef666ed132179df9cf15b6.png)

Now the value ![q_{0}](img/a52fdb7a3f8e9d957152a2263d914281.png) at the boundary ![\nu_0](img/c15610bd2db7c127cda5ec48aff90fe0.png) can be expressed in terms of ![q_1](img/ca4cb4f59bf32dddd72682afec2b6653.png) and ![q_2](img/dab963ffb5426e3685a6abd100531c72.png).

![q_{0} = \frac{-b_1q_{1} - c_1q_{2}}{a_1}](img/236b4898ffa5bf9978c4d9a99653a73a.png)

This equation can be used to remove the boundary value ![q_0](img/b23f0e755ad8fabd34fc6590bb55461e.png) from the discretization of the transformed Fokker-Planck equation. In the same manner the zero flow boundary condition can be implemented for the upper boundary ![\nu_{max}](img/31fc6a7a428dbb82341675dddc6aa113.png) and for the original Fokker-Planck equation.

The following parameters of the square-root process will be used to test the different boundary conditions.

![\kappa=2.5,\ \theta=0.2,\ \sigma\in\{0.2, 2.0\} ](img/c13a22f00113af9cb5659055da00b5f2.png)

The uniform grid ![\nu_{min} \le \nu_i \le \nu_{max}](img/dbbcf66c05263beade9d15da56fe4da0.png) has 100 or 1000 grid points and the stationary solution ![p^s_{\nu_i}](img/7b2ca8c3be6d531b92bc8b4aa6afc130.png) of the Fokker-Planck equation is chosen as the start configuration on the grid points. The boundaries ![v_{min}, v_{max}](img/2b5cf020ff4da7df9b5445c59263e4dc.png) are defined via the inverse cumulated distribution function such that

![\int_0^{v_{min}}p^s_\nu d\nu = \int_{v_{max}}^\infty p_\nu^s d\nu = 1\% ](img/8e2e38444493ee965ddeddccaacf9612.png).

The grid covers 98% of the distribution and this value would not change over time if the boundary conditions are satisfied without discretiszation errors. To test the magnitude of the discretization errors we let the initial solution evolve over one year using 100 time steps with the Crank-Nicolson scheme. The resulting solution ![q_{i,t=1} = v_i^\alpha p_{i,t=1}](img/c2ac86d37a48c930f4f4c0d2328aac36.png) is interpolated using cubic splines to get the function ![q_\nu](img/0e1e31233d7ed40e4830e4dbe82eaf65.png). The value

![\int_{vmin}^{v_{max}}q_\nu\nu^{-\alpha} d\nu - 98\% ](img/8df08b98ef82e823bf3f170ecbbf7544.png)

servers as a quality indicator for the discretization errors of the boundary condition.

As can be seen in the diagram below if ![\sigma](img/d2e0f91b4f9ab5cb8554a898295d118c.png) is small then the original Fokker-Planck equation shows smaller discretization errors than the transformed Fokker-Planck equation in ![q=v^\alpha p](img/1aa7c27506ffb3d46a4d2b7f5592b626.png). But if ![\sigma](img/d2e0f91b4f9ab5cb8554a898295d118c.png) becomes larger and especially if the Feller constraint is violated then the solution of the transformed Fokker-Planck equation clearly outperforms the original solution. As a rule of thumb based on this example one should use the original Fokker-Planck equation if ![\frac{2\kappa\theta}{\sigma^2} \ge 2.5](img/3debfe345dc692bb14237168597e3397.png)  and the transformed equation otherwise.

[![plot](img/e503283550a03fba3cb92ca921f4e67e.png)](https://hpcquantlib.wordpress.com/wp-content/uploads/2013/05/plot.png)

The same techniques can be used to solve the Fokker-Planck equation for the Heston model. The code for the numerical tests is available in the latest [QuantLib](http://www.quantlib.org) version from the SVN [trunk](http://sourceforge.net/p/quantlib/code/HEAD/tree/). The diagram is based on the test FDHestonTest::testSquareRootEvolveWithStationaryDensity.

[1] A. Dragulescu, V. Yakovenko, [Probability distribution of returns in the Heston model with stochastic volatility](http://arxiv.org/pdf/cond-mat/0203046)

[2] V. Lucic, [Boundary Conditions for Computing Densities in Hybrid Models via PDE Methods](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1191962)

[3] P. Lermusiaux, [Numerical Fluid Mechanics](http://ocw.mit.edu/courses/mechanical-engineering/2-29-numerical-fluid-mechanics-fall-2011/index.htm), Lecture Note 14, Page 5*