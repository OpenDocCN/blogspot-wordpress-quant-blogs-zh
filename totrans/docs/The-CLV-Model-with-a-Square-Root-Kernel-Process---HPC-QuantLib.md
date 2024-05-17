<!--yml
category: 未分类
date: 2024-05-17 23:26:53
-->

# The CLV Model with a Square Root Kernel Process – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2016/11/02/the-clv-model-with-a-square-root-kernel-process/#0001-01-01](https://hpcquantlib.wordpress.com/2016/11/02/the-clv-model-with-a-square-root-kernel-process/#0001-01-01)

The kernel process of the Collocating Local Volatility (CLV) model [1] defines the forward skew dynamics of the model. Although the Ornstein-Uhlenbeck process has some nice analytical features it offers sometimes too little control over the forward skew dynamics. The square root process

![d\nu_t=\kappa(\theta-\nu_t) dt + \sigma \sqrt{\nu_t}dW_t ](img/f5bcf96d62120c9cf7fc549d3c0b5f71.png)

is a promising kernel to get more control over the forward skew. First, exact sampling is pretty easy for the square root process. The probability density function of ![\nu_t](img/c56c88dfcf2d52e0221304d7c3dd90f9.png) given ![\nu_0](img/c15610bd2db7c127cda5ec48aff90fe0.png) is

![\nu_t = \frac{\sigma^2 (1- e^{-\kappa t})}{4\kappa} \chi_d^{'2}\left(\frac{4\kappa e ^{-\kappa t}}{\sigma^2(1-e^{-\kappa t})}\nu_0\right)](img/6d453b703272cfde72c815758cd7aea4.png)

where ![\chi_d^{'2}](img/d001df63428660a5acdceef1a172fd1e.png) denotes the noncentral chi-squared distribution with

![d=\frac{4\theta\kappa}{\sigma^2}](img/bb8ea86ea02539e4e1f82d43172284c6.png)

degrees of freedom and the noncentrality parameter

![\lambda = \frac{4\kappa e^{-\kappa t}}{\sigma^2(1-e^{-\kappa t})}\nu_0](img/0f91941ec7244e8e2f4f349363631bd1.png)

The boost library provides an efficient and accurate implementation of the inverse of the cumulative noncentral chi-squared distribution function, which can be used for an exact Monte-Carlo sampling scheme.

The optimal collocation points are given by the Gaussian quadrature points, which are defined by the zeros of the corresponding orthogonal polynomials. The orthogonal polynomials are defined by a recurrence relation and the collocation points are given by the eigenvalues of a symmetric, tri-diagonal matrix with the diagonal ![\{\alpha_i\}](img/42689b0d62841508524b832adddc8bd9.png) and the minor diagonal ![\{\sqrt{\beta_i}\}](img/37ac220896fb9d4b4443fd4244e759b9.png). Again these vectors are defined by a recurrence relation [2]

![\begin{array}{rcl} z_{k, i} &=& z_{k-1, i+1} + \alpha_k z_{k-1,i} - \beta_k z_{k-2,i} \\ \nonumber \alpha_{k+1} &=& \frac{z_{k-1,k}}{k-1,k-1}-\frac{z_{k,k+1}}{z_{k,k}} \\ \nonumber \beta_{k+1} &=& \frac{z_{k,k}}{z_{k-1,k-1}}\\ \nonumber z_{-1,i} &=& 0 \\ \nonumber z_{0,i} &=& \mu_i = \int_0^\infty x^i\chi_{d,\lambda}^{'2}(x) dx \\ \nonumber \alpha_1 &=& -\frac{\mu_1}{\mu_0} \\ \nonumber \beta_1 &=& \mu_0 = 1\end{array} ](img/5ff276f77e9371ffc817d70da94af577.png)

The first n moments ![\mu_i(d, \lambda), i=0,..,n](img/30af049efdcd30a39895904a3e63e19e.png) of the noncentral chi-squared distribution can be calculated using Mathematica and exported as plain C code in order to be integrated into QuantLib.

```
m[n_] := CForm[ Expectation[X^n, X \[Distributed]
NoncentralChiSquareDistribution[d, lambda]] // Simplify]

```

Solving the recurrence relation is often ill-conditioned when using double precision. Therefore the resulting equations will be solved using the Boost.Multiprecision package with the cpp_dec_float back-end (header only and dependency free). The results have been tested accordingly to the proposal in [3]. For any reasonable number of collocation points a precision of up to 100 digits seems to be sufficient. On the other side the computation even with 100 digits is really fast. The eigenvalue calculation is carried out using standard double precision.

The implementation of the calibration routine follows the same way as for the Ornstein-Uhlenbeck kernel process. Again the calibration is pretty fast and accurate compared with other structured models even though it involves multiple precision arithmetic.

**Example: Forward volatility skew**

*   Market prices are given by a Heston model with

![S_0=100, r=0.1, q=0.05, \nu_0=0.09, \kappa=1.0, \theta=0.06, \sigma=0.4, \rho=-0.75](img/5b939a0cb5329020a11b678c9cdd5460.png).

*   SquareRoot-CLV kernel process parameters are given by

![\kappa=0.2, \theta=0.09, \sigma=0.1, x_0=0.09](img/ca696a25fdb6b8f07a1aa226b0b6a7e8.png)

The diagram below shows the implied volatility of an forward starting European option with moneyness varying from 0.5 to 2 and maturity date six month after the reset date.

![circlvforwardskew1](img/7dbf509dfb1f32a4a785efdd995ff863.png)

Same plot but with the following parameters of the square root kernel process

![\kappa=0.1, \theta=0.09, \sigma=0.1, x_0=0.25](img/64c895d94dc2a288e9822239cb513de1.png)

![circlvforwardskew2](img/03960a1c1378af347046250d7823009f.png)

Source code is available [here](http://hpc-quantlib.de/src/squarerootclvmodel.zip). The code is in an early state and needs some more testing/clean-up before a pull request can be made out of it. Next step will be to calibrate such a CIR-CLV model to the forward skew dynamics of an Heston Stochastic Local Volatility model.

[1] A. Grzelak, 2016, [The CLV Framework – A Fresh Look at Efficient Pricing with Smile](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2747541)

[2] M. Morandi Cecchi and M. Redivo Zaglia, [Computing the coefficients](http://ac.els-cdn.com/0377042793901522/1-s2.0-0377042793901522-main.pdf?_tid=643d5dca-a05d-11e6-9a56-00000aab0f27&acdnat=1478023545_cf7c87cba4cc9e37a136e68a2564d411) [of a recurrence formula for numerical integration by moments and](http://ac.els-cdn.com/0377042793901522/1-s2.0-0377042793901522-main.pdf?_tid=643d5dca-a05d-11e6-9a56-00000aab0f27&acdnat=1478023545_cf7c87cba4cc9e37a136e68a2564d411) [modified moments.](http://ac.els-cdn.com/0377042793901522/1-s2.0-0377042793901522-main.pdf?_tid=643d5dca-a05d-11e6-9a56-00000aab0f27&acdnat=1478023545_cf7c87cba4cc9e37a136e68a2564d411)

[3] Walter Gautschi, [How and How not to check Gaussian Quadrature Formulae.](https://www.cs.purdue.edu/homes/wxg/selected_works/section_08/084.pdf)