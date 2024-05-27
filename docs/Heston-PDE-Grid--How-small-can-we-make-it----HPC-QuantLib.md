<!--yml

category: 未分类

日期：2024-05-13 00:12:10

-->

# Heston PDE Grid: How small can we make it? – HPC-QuantLib

> 源自：[`hpcquantlib.wordpress.com/2021/05/25/heston-pde-grid-how-small-can-we-make-it/#0001-01-01`](https://hpcquantlib.wordpress.com/2021/05/25/heston-pde-grid-how-small-can-we-make-it/#0001-01-01)

目标是将用在[任意数目的差分点](https://hpcquantlib.wordpress.com/2018/06/05/arbitrary-number-of-stencil-points/)的技巧应用到具有![x_t = \\ln S_t](img/16f746d6b95837f7e9cfec20abd14a6d.png)的 Heston 模型的偏微分方程（PDE）中。

![\\displaystyle  0 = \\frac{\\partial u}{\\partial t} +\\frac{1}{2}\\nu\\frac{\\partial² u}{\\partial x²}  + \\left(r_t-q_t -\\frac{\\nu}{2}\\right)\\frac{\\partial u}{\\partial x} + \\rho\\sigma\\nu \\frac{\\partial² u}{\\partial \\nu \\partial x} +\\frac{1}{2}\\sigma²\\nu\\frac{\\partial² u}{\\partial \\nu²} + \\kappa(\\theta - \\nu) \\frac{\\partial u}{\\partial \\nu}-r_tu](img/f384ae2a09f7838f35121cd7463a761b.png)

为了在给定的精度下得到最小可能的网格。手头上的 Heston 模型参数是

![\\displaystyle S_0 = 100, v_0 = 0.04, \\kappa = 1, \\theta = v_0, \\sigma=0.2, \\rho=-0.75, r=5\\%, q=0\\%](img/4e5ac95d235d554373299178312a9555.png),

基准期权的行权价为

![\\displaystyle k\\in \\{50, 75, 90, 100, 110, 125, 150, 200\\}](img/f566faea1dfbb25956061e577152528b.png)

而期权的到期日应该为一年。首先让我们在![x](img/a02ca3461b38d94f9ca87463267dd179.png)方向上使用五点差分。如预期的那样，收敛阶在从二阶到四阶递增。

接下来是同样的实验，但现在在![\\nu](img/cafd388c0e801cfe79db6142b0511d49.png)方向也使用五点差分。由于收敛速度较快，即使是在相对较小的格点上，也已经出现了有限格效应。

时间方向上可以使用 Richardson 外推将收敛阶从二阶外推到三阶。

所以最终，对于这组参数，如果目标是使平均定价误差低于![\\displaystyle 10^{-3}](img/b2b9278c24f8abb4e84a51e1c228657d.png)，那么网格大小为

![\\displaystyle x\\times\\nu\\times T = 50\\times 10 \\times 20](img/4b95ce8ce708afea17a46786bafa25e6.png)

似乎使用![x](img/a02ca3461b38d94f9ca87463267dd179.png)和![\\nu](img/cafd388c0e801cfe79db6142b0511d49.png)方向的五点差分算子和时间方向的 Richardson 外推就足够了。不幸的是，对于给定的精度，这一技术比通常的技术要慢，如算子分裂，因为 Crank-Nicolson 格式的矩阵求逆必须由一个迭代求解器完成，也就是 BiCGstab。数值实验的代码可以在测试用例

[`NthOrderDerivativeOpTest::testHigerOrderHestonOptionPricing()`](https://github.com/lballabio/QuantLib/blob/master/test-suite/nthorderderivativeop.cpp)中找到。
