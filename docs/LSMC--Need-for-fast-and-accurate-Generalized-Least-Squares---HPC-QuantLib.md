<!--yml

category: 未分类

date: 2024-05-17 23:29:36

-->

# LSMC：快速准确广义最小二乘的需求 - HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2016/02/13/lsmc-need-for-fast-and-accurate-generalized-least-squares/#0001-01-01`](https://hpcquantlib.wordpress.com/2016/02/13/lsmc-need-for-fast-and-accurate-generalized-least-squares/#0001-01-01)

更新日期：2026 年 2 月 21 日：添加了 QR 分解与枢轴和 QuantLib 性能改进的值。

最小二乘蒙特卡罗模拟将大部分总计算时间花费在广义最小二乘上，尤其是如果问题本身具有高维状态。解正规方程的首选技术是 QR 分解

![A = Q\cdot R](img/97c2f8703e9053349ddbf5de6e2a9f09.png)

其中![Q](img/cce0ee434ca4714e77d346c4f6ebf573.png)是正交矩阵，![R](img/e44744d666c5e2e22c0d42b61e9631f9.png)是上三角矩阵，或者奇异值分解（SVD）

![A = U\cdot w \cdot V^T](img/329d3f5695e52894845c07096ea0544f.png)

其中![U](img/11464e262320dc0222962f3337ef8705.png)是列正交矩阵，![V](img/77bb324491ef895001cc13da1d0208f6.png)是一个正交矩阵，![w](img/91e16cf334dc7440d37f9b5fa24cabb2.png)是一个正半定对角矩阵。Cholesky 分解

![A = L \cdot L^T](img/d1eac0f4a43b0f06fd99754089769fb9.png)

其中![L](img/c48829d076e0b243fc2be1c334f78ee6.png)是一个下三角矩阵，是最快的方法，但通常数值不稳定。作者在[1]中总结了所有方法，并概述了对![m](img/29a5c6972bfb9cdcfcd544dd4275dd4e.png)个观测和![n](img/17deaa124310c647ec1dd85566e7b1e5.png)个参数的计算工作量如下：

+   Cholesky 分解：成本为![\sim mn² + n³/3](img/74dcbbe9f5f17ef045f6d903f6d714f0.png) flops

+   QR 分解：成本为![\sim 2mn² - 2n³/3](img/8486852953b5f615cfc5251d42bfe62f.png) flops

+   奇异值分解：成本为![2mn² + 11n³](img/32e1547543a25a084394074a6c63756e.png) flops

对于 LSMC 模拟，我们有![m\gg n](img/1fff5960e40f94102b3cbb63eb790640.png)，因此 QR 分解在计算上没有比 SVD 更大的优势。由于 QR 分解在![A](img/f6c194c9a4ae3b06df69cda19cb6b1e8.png)是秩亏时存在数值问题，奇异值分解通常是 LSMC 模拟的选择方法。

三种分解方法在[QuantLib](http://quantlib.org/index.shtml)中都可以使用，在[LAPACK](http://www.netlib.org/lapack/)（带或不带优化的[OpenBLAS](http://www.openblas.net/)库）和英特尔的[MKL](https://software.intel.com/en-us/intel-mkl)库中也可使用。通过 LSMC 的标准摆动期权估值应作为一个测试平台，以测量带和不带列交换的 QR 分解的性能以及 SVD 算法。对于 LAPACK 和 MKL，已使用 dgels 和 dgesvd 方法来实现 SVD 和无交换的 QR 分解，而带交换的 QR 则基于 dgeqp3、dormqr 和 dtrsm。为了保持结果可比较，所有情况下都测量了单线程性能。参考价格是通过有限差分方法计算得到的，所有 LSMC 实现都导致了与参考价格相同的价格。QuantLib 1.7 中当前的 QR 实现如果在行数远大于列数时，存在性能问题。对这些测试使用了 QuantLib QR 分解的[改进](https://github.com/lballabio/QuantLib/pull/54/files)版本。

![swing_perf](img/adb59e4324681b7bcff59dd501bb9cd8.png)：swing_perf 的图片。

正如预期，MKL 通常是速度最快的库，但 MKL 与 LAPACK 加上 OpenBLAS 之间的差异很小。

参考文献[1]：杜克·李（Do Q Lee），2012 年，《解决最小二乘问题的数值高效方法》（[Numerically Efficient Methods for Solving Least Squares Problems](http://math.uchicago.edu/~may/REU2012/REUPapers/Lee.pdf)）。
