<!--yml
category: 未分类
date: 2024-05-17 23:31:11
-->

# The Hybrid Heston-Hull-White Model in the H1HW Approximation – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2012/08/17/the-hybrid-heston-hull-white-model-in-the-h1hw-approximation/#0001-01-01](https://hpcquantlib.wordpress.com/2012/08/17/the-hybrid-heston-hull-white-model-in-the-h1hw-approximation/#0001-01-01)

In his PhD thesis [1] Lech Grzelak studies several hybrid equity interest rate models. Among others the thesis presents the H1HW approximation of the hybrid Heston-Hull-White model:

![\begin{array}{rcl} dS_t &=& (r_t-q_t) S_t dt + \sqrt{v_t} S_t dW_t^S \\ dv_t &=& \kappa_v (\theta_v - v_t) dt + \sigma_v \sqrt{v_t} dW_t^v \\ dr_t & = & \kappa_r(\theta_{r,t}-r_t) dt + \sigma_r dW_t^r \\ \rho_{Sv} dt &=& dW_t^S dW_t^v\\ \rho_{Sr} dt &=& dW_t^S dW_t^r \\ \rho_{vr} dt &=& dW_t^v dW_t^r \end{array} ](img/d22f9b2f071c87cf69db05c3a2ad288e.png)

This model is tailor-made to analyse the impact of stochastic interest rates on structured equity notes like e.g. auto-callables. The corresponding partial differential equation

![\begin{array}{rcl} 0 &=& \frac{\partial u}{\partial t} + \frac{1}{2}S^2\nu \frac{\partial^2 u}{\partial S^2}+ \frac{1}{2}\sigma_\nu^2\nu\frac{\partial^2u}{\partial \nu^2}+ \frac{1}{2}\sigma_r^2\frac{\partial^2 u}{\partial r^2} + \rho_{S\nu}\sigma_\nu S\nu\frac{\partial^2u}{\partial S\partial\nu} + \rho_{Sr}\sigma_r S\sqrt\nu \frac{\partial^2 u}{\partial S\partial r} \nonumber\\ &+& (r-q)S\frac{\partial u}{\partial S}+ \kappa_v(\theta_v-\nu)\frac{\partial u}{\partial \nu}+ \kappa_r(\theta_{r,t}-r)\frac{\partial u}{\partial r} -ru \nonumber \end{array} ](img/65b5f976ac97a5585117017854522f0b.png)

does not fit into into the affine diffusion process framework and therefore has no closed form solution based on the characteristic function like the Heston model.

The H1HW approximation replaces the term ![\sqrt \nu](img/dbdc75526aa267f4dcb07536b8de3bf2.png) in the correlation interaction by its expectation value ![E(\sqrt\nu)](img/e2a619d190fff9e31510e33a2a7d533c.png). Semi closed form solutions for ![E(\sqrt\nu)](img/e2a619d190fff9e31510e33a2a7d533c.png) exist, if ![\nu_t](img/c56c88dfcf2d52e0221304d7c3dd90f9.png) is a CIR type process. The corresponding hybrid model is affine and a pricing engine for plain vanilla options can easily be implemented in QL based on the characteristic function framework.

The diagram below shows the root-mean-square error for vanilla european options with strikes equal to 40%, 80%, 100%, 120% and 180%. The parameters of the process are given by

![\kappa_v=0.3, \theta_v=0.05, \rho_{S\nu}=0.3, \rho_{Sr}=-0.6, \kappa_r=0.01, \sigma_r=0.01](img/f4474d7071754907801dd8d43b55d803.png)

The vol-of-vol ![\sigma_{\nu}](img/ce905c110a635d6ba6fd20f2fc5b9f81.png) is set so that the Feller parameter ![\sigma_\nu^2/(\kappa_v \theta_v)](img/f6039600c502feb6512481b53a9ff498.png) varies between 0.25 and 128\. The reference prices are calculated using the finite difference Heston-Hull-White engine.

[![](img/c51e1878fa71680364f086a75c309373.png "plot")](https://hpcquantlib.wordpress.com/wp-content/uploads/2012/08/plot1.png)

The results of the H1HW approximation look very well if the Feller constraint ![\sigma_\nu^2/(\kappa_\nu \theta_\nu) < 2](img/8a789aed8b9f33a0d99393c4b6d49fb8.png) is fulfilled but has problems in high ![\sigma_\nu](img/81d93c05287608ce1d2bc01b770fec62.png) scenarios. The integration of the characteristic function of the H1HW approximation becomes unstable if ![\rho_{Sr} < 0](img/faf51378befbc30a70ae5d660c0cfce0.png). The example code is available [here](http://hpc-quantlib.de/src/h1hw.zip) and depends on the latest QL version based from the [SVN trunk.](http://sourceforge.net/p/quantlib/code/HEAD/tree/)

[1] Lech A. Grzelak: [Equity and Foreign Exchange Hybrid Models for Pricing Long-Maturity Financial Derivatives](a8e1a007-bd89-481a-aee3-0e22f15ade6b/PhDThesis_main.pdf)