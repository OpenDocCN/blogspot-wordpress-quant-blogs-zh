<!--yml
category: 未分类
date: 2024-05-17 23:42:27
-->

# Scrambled Sobol Sequences – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2011/05/11/pricing-asian-options-using-scrambled-sobol-sequence/#0001-01-01](https://hpcquantlib.wordpress.com/2011/05/11/pricing-asian-options-using-scrambled-sobol-sequence/#0001-01-01)

The authors of [1][2] presented an efficient way to create scrambled Sobol numbers and have shown that their scrambling algorithm can lead to a significantly higher convergence speed. The upcoming CUDA 4.0 Release provides an implementation of the scrambling algorithm outlined in [2].

The aim is now to compare the order of convergence of a PRNG (Merssenne-Twister),  a QRNG (Sobol) and this scrambled-QRNG for the pricing of a portfolio of geometric Asian options. To number of observation dates of the Asian options in the benchmark portfolio varies between 45 and 120 observation dates. The dimensionality of the pricing problem is considerably large. We’ll use a Brownian bridge to construct the paths. This ensures that the first coordinates of a Sobol sequence are used to sample the most important modes.

The error analysis is not an easy task.  Simply applying another randomized shift is not sufficient as this transformation changes the discrepancy of a point-set (A shifted (t,m,d)-net does not need to be a (t,m,d)-net.). In [3] this problem was overcome by looking on the RMS relative error

![\sqrt{\frac{1}{m}\sum_{i=1}^m\left(\frac{\hat{C}_i -C_i}{C_i}\right)^2}](img/dcb9bf78c212158e44a1c35f912c6dad.png)

of a set of benchmark options with true prices given by ![C_1,...,C_m](img/831a4009518336968517250147f8fe36.png) and the Monte-Carlo approximations ![\hat{C}_1,...,\hat{C}_m](img/ed43dabcc2b93498206b9a85e90138f4.png).

We are in particular interest in ratios between the PRNG, QRNG and scrambled QRNG errors and in the order ![\alpha](img/86ceb19e0d1d39c689d6601fd46650ae.png) of the convergence.  For PRNG we are expecting a convergence of order ![err \simeq N^{\alpha}](img/b4665ed6b0dbc8ad2dfae8709b2947fd.png) with  ![\alpha=-0.5](img/589629ef8e0566261e8844268d68958c.png) and ![N](img/f6ed931dee56eceee76562d962e13d4a.png) being the number of paths.

As can be seen in the diagram the scrambled Sobol sequence provides the smallest overall error bounds but the convergence order between scrambled and non-scrambled Sobol does not differ significantly. As the implementation comes more or less for free it’s definitely worth to check scrambled Sobol sequences out.

C++ and CUDA code is available [here](http://hpc-quantlib.de/src/scrambled.zip).  It depends on [QuantLib 1.1](http://quantlib.org) and [CUDA 4.0](http://www.nvidia.com/object/cuda_home_new.html). If you want to generate the plot directly out of the C++ program you also need [R](http://www.r-project.org/), [RCPP](http://cran.r-project.org/web/packages/Rcpp/index.html) and [RInside](http://cran.r-project.org/web/packages/RInside/index.html).

[![](img/7ae8c9af651ce65be71fb670f0994e75.png "plot")](https://hpcquantlib.wordpress.com/wp-content/uploads/2011/05/plot2.png)

[1] J. Dick, [Higher order scrambled digital nets achieve the optimal rate of the root mean square error for smooth integrands](http://arxiv.org/abs/1007.0842). ArXiv, 8 July 2010.

[2] A.B. Owen, [Local antithetic sampling with scrambled nets](http://arxiv.org/pdf/0811.0528). ArXiv, 28 May 2008

[3] P. Glasserman, Monte Carlo Methods in Financial Engineering.  ISBN-0387004513