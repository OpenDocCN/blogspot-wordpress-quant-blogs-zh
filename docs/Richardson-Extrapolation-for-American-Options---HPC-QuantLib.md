<!--yml

类别：未分类

日期：2024-05-17 23:30:53

-->

# Richardson Extrapolation for American Options – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2012/06/10/richardson-extrapolation-for-american-options/#0001-01-01`](https://hpcquantlib.wordpress.com/2012/06/10/richardson-extrapolation-for-american-options/#0001-01-01)

像一维的 Crank-Nicholson 方案或多维的操作分解方法如 Hundsdorfer-Verwer 方案这样的流行有限差分方案，通常在金融工程中的典型偏微分方程中以![\Delta t](img/35bff8105c8314c62070030cd46f8a1c.png)实现二阶收敛。不幸的是，如果这些方案与动态规划结合使用来定价美式期权，动态规划步骤的一阶收敛会破坏二阶收敛。

理查森外推法是一种简单的数值宝石，用以提高数值方法的收敛阶。比如说，一个数值方法的收敛行为如下

![f(\Delta t) = f_0 + \alpha \cdot (\Delta t)^n + O((\Delta t)^{n+1}) ](img/9494255d5ef2da3a60d4f8ecc90f202e.png) .

请注意，这比假设数值方法的阶数为*n*的要求更为严格，因为![\alpha](img/86ceb19e0d1d39c689d6601fd46650ae.png)不依赖于![\Delta t](img/35bff8105c8314c62070030cd46f8a1c.png)。现在公式

![R(x, \Delta t) = \frac{x^n f\left(\frac{\Delta t}{x}\right)-f(\Delta t)}{x^n-1} = f_0 + O((\Delta t)^{n+1}) ](img/61a914424f58647e72dd50ef590106bd.png)

也有

![\lim_{\Delta t\rightarrow 0} R(x,\Delta t) = f_0 ](img/e122534998d71446282043df314626fe.png)

但理查森外推法的收敛阶![R(x, \Delta t)](img/df54f5183a31ab276e6f5e360d3f01c6.png)是 *n+1*。阶数不依赖于*x*的具体值，但通常*x*选择为 2。这个简单的技巧可以扩展到*n*未知的情况，或者可以使用理查森外推法*m*次以提高收敛阶到*n+m* [2]。

让我们将理查森外推法应用于海森随机微分方程下美式看跌期权的价格。相应的偏微分方程

![0 = \frac{\partial u}{\partial t} + \frac{1}{2}S²v\frac{\partial² u}{\partial S²}+\rho\sigma S\nu \frac{\partial² u}{\partial S\partial \nu} + \frac{1}{2}\sigma²\nu \frac{\partial² u}{\partial \nu²} + rS\frac{\partial u}{\partial S} + \kappa(\theta - \nu)\frac{\partial u}{\partial \nu} -r u ](img/95a5ff3857be332a7e1487df4894904e.png)

使用 Hundsdorfer-Verwer 方案[1]求解。在每一步之后，使用动态规划实现提前行权条件。实验的参数是

![\small{T=1, K=10, S_0=11, r=0.1, \

如图所示，即使理查德森外推法是一个简单的公式，但它将收敛阶从*1.0*提升到了约*2.1*。如果事先不知道阶数，则得到的阶数仍为*1.4*。

![plot](https://hpcquantlib.wordpress.com/wp-content/uploads/2012/06/plot.png)

源代码可在[此处](http://hpc-quantlib.de/src/richardson.zip)找到。它依赖于从[SVN 主干](http://sourceforge.net/p/quantlib/code/HEAD/tree/)获取的最新 QuantLib 版本。

[1] Karel in ’t Hout, [ADI 有限差分法用于具有相关性的 Heston 模型](http://win.ua.ac.be/~kihout/ADI_Heston_lecture.pdf)。

[2] Eric Hung-Lin Liu, [数值外推法的基本方法及其应用](http://ocw.mit.edu/courses/mathematics/18-304-undergraduate-seminar-in-discrete-mathematics-spring-2006/projects/xtrpltn_liu_xpnd.pdf)。
