<!--yml
category: 未分类
date: 2024-05-17 23:32:32
-->

# Probability Distribution of the Heston Model, Part II – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2014/02/22/probability-distribution-of-the-heston-model-part-ii/#0001-01-01](https://hpcquantlib.wordpress.com/2014/02/22/probability-distribution-of-the-heston-model-part-ii/#0001-01-01)

Starting point for a semi-analytical solution of the Fokker-Planck forward equation for the Heston model is the exact sampling algorithm of Broadie and Kaya [1] (for the notation please see [2])

![\begin{array}{rcl} x_t &=& x_0 + m(t) + \sigma(t)Z \nonumber \\ \sigma^2(t) &=& (1-\rho^2)\int_0^t \nu_s ds \nonumber \\ m(t) &=& (r_t-q_t)t - \frac{1}{2}\int_0^t \nu_s ds + \rho\int_0^t \sqrt{\nu_s}dW_s^{(1)} \nonumber \end{array}](img/928b825394cb30fa0d6e679752c8f983.png)

The probability distribution function can be described as

![p(x_t, \nu_t, t) = p(\nu_t, t) p(x_t,t\mid \nu = \nu_t) ](img/bdea86416e661daeb5822f56f8e4bfc7.png)

and ![p(\nu_t, t)](img/430842f34bf863fe6bb7c17e3c6a3a8f.png) is  given by a noncentral chi squared distribution. The distribution ![p(x_t, t \mid \nu = \nu_t)](img/e3bed4b562bcc0bd779656cbc56327a1.png) can be calculated using the exact simulation algorithm. In this algorithm the variable ![x_t](img/7a6c51eeafde57877526801e4a5da1e1.png) is given as a function of two random variables ![\int_0^t \nu_s ds](img/787aff30b276853cbb00259a1e526614.png) and ![Z](img/051625cbd82ebd99476330b3cd2e1917.png).

The distribution of ![x_t](img/7a6c51eeafde57877526801e4a5da1e1.png) can now be derived using the general transformation theorem for random variables: Let *X *be a random variable with probability density function *f.* The transformed random variable ![Y=h(X)](img/8bddc80b8b9e990d7a203826ae694707.png) has the probability density function

![p(y) = f(h^{-1}(y)) \left| \det \left( \frac{\partial h^{-1}_i(y)}{\partial y_j} \right)\right|](img/b42c2ccbbce570d49a91ce7efaafa8ce.png)

First step is now to rewrite the exact simulation method in terms of the two random variables

![X_1 = \int_0^t \nu_s ds \ , X_2=Z](img/78c8b1e2144b8f71f4f5d88a3621625e.png) .

The simulation scheme then becomes

![\begin{array}{rcl} x_t &=& x_0+a(t) -\frac{1}{2}X_1 + \frac{\rho\kappa}{\sigma}X_1+\sigma(t) X_2 \nonumber \\\sigma^2(t)&=&(1-\rho^2)X_1 \nonumber \\a(t)&=&(r_t-q_t)t+\frac{\rho}{\sigma}\left( \nu_t-\nu_0-\kappa\theta t \right)\end{array}](img/9abcbc08578a7594631e2893d55544e2.png)

or in terms of the transformed random variable

![\begin{array}{rcl} Y_1 =h_1(X_1,X_2) &=& x_0+a(t)-\frac{1}{2}X_1 + \frac{\rho\kappa}{\sigma}X_1+\sqrt{\left(1-\rho^2\right)X_1}X_2 \nonumber \\ Y_2=h_2(X_1,X_2)&=& X_1 \nonumber\end{array}. ](img/c230689e5a6bace646eaa6ab0e27981a.png)

Let ![\phi(x_1)](img/607cb35ad5e19ff578fdbbd4e617bdd7.png) be the density function of ![X_1](img/1db0a764a9aadca3989c631bd0a5fef2.png)

![\phi(x_1)=\frac{2}{\pi}\int_0^\infty \cos ux_1 \mathrm{Re}(\Phi(u))\mathrm{d}u](img/fca80341c360f103a604586749044e10.png)

and ![X_2](img/143c44d06619ea584f5e40cf47d21c85.png) follows by definition a normal distribution. The joint probability density function of ![(X_1, X_2](img/0820147029a025c055ff21d510e92ea0.png)) is then

![f\left( \begin{matrix} x_1 \\ x_2 \end{matrix}\right)=\phi(x_1) \frac{1}{\sqrt{2\pi}}e^{-\frac{x_2^2}{2}}](img/0194f06c261d4782d12ee9553e1bf3ed.png)

with

![\begin{array}{rcl}f\left(h^{-1}(y)\right)&=&f\left(\begin{matrix}y_2 \\ \frac{1}{\sqrt{\left(1-\rho^2\right)y_2}}\left(y_1-x_0-a(t)+\frac{1}{2}y_2-\frac{\rho\kappa}{\sigma}y_2\right)\end{matrix}\right)  \nonumber \\  \left|\det \left( \frac{\partial h^{-1}_i(y)}{\partial y_j} \right)\right| &=& \frac{1}{\sqrt{\left(1-\rho^2\right)y_2}}  \end{array}.](img/e09ad5419d77b32ebfb9edffa87f1251.png)

This yields to the semi-analytical formula for the solution of the Fokker-Planck equation because by definition ![p(x_t,t \mid \nu = \nu_t)](img/101b0fc5df95d5209d689ffcfffb6db2.png) is the distribution density function of ![Y_1](img/7a7aaee8206ca6fdf1f140cc29a465ac.png), which is given by

![p(x_t,t \mid \nu = \nu_t) = \int_0^\infty \mathrm{d}y_2 p(y_1, y_2)\mid_{y_1=x_t} = \int_0^\infty \mathrm{d}y_2 \left[f\left(h^{-1}(y)\right)\left|\det \left( \frac{\partial h^{-1}_i(y)}{\partial y_j} \right)\right| \right]_{y_1=x_t}](img/30818ad101b0f674c0b63d908b613d37.png)

The integration over ![y_2](img/ec1ac6fd3be365487b52e785be175352.png) can be carried out using e.g. the Simpson integral rule together with the Cornish-Fisher expansion, which gives an upper bound for the truncation of the upper limit of the integration.

The contour plots below show the probability density function of the Heston model for some example parametrisations.

[![plot](img/34a24b8bc901f4e09c6288476cfc85cf.png)](https://hpcquantlib.wordpress.com/wp-content/uploads/2014/02/plot.png)
![\begin{array}{|c|c|c|c|c|c|c|c|c|} \hline {\rm Parameters} & x_0 & \nu_0 & r & q & \kappa & \theta & \sigma & \rho \\ \hline \hline  a & 4.6052 & 0.4 & 5\% & 2.5\% & 1.0 & 0.4 & 0.8 & -75\%  \\ \hline  b & 4.6052 & 0.4 & 5\% & 2.5\% & 1.0 & 0.4 & 0.8 & \ \ 75\%  \\ \hline  c & 4.6052 & 0.4 & 5\% & 2.5\% & 1.0 & 0.4 & 0.4 & -75\%  \\ \hline  d & 4.6052 & 0.4 & 5\% & 2.5\% & 1.0 & 0.4 & 0.4 & \ \ \ \ 0\%  \\ \hline  \end{array}](img/2d7094c664a4fb63528d7fe90e0d74c2.png)

The example code is available [here](http://hpc-quantlib.de/src/hestonpdf.zip) and depends on the upcoming QuantLib version 1.4.

[1] M. Broadie, Ö. Kaya, [Exact Simulation of Stochastic Volatility and other Affine Jump Diffusion Processes](http://finmath.stanford.edu/seminars/documents/Broadie.pdf)

[2] K. Spanderen, [Probability Distribution of the Heston Model, Part I](https://hpcquantlib.wordpress.com/2014/02/04/probability-distribution-of-the-heston-model-part-i/)

[3] R.U. Seydel, [Tools for Computational Finance, pp 86](http://www.springer.com/mathematics/quantitative+finance/book/978-1-4471-2992-9)