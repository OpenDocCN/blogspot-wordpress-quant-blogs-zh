<!--yml
category: 未分类
date: 2024-05-17 23:29:36
-->

# LSMC: Need for fast and accurate Generalized Least Squares – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2016/02/13/lsmc-need-for-fast-and-accurate-generalized-least-squares/#0001-01-01](https://hpcquantlib.wordpress.com/2016/02/13/lsmc-need-for-fast-and-accurate-generalized-least-squares/#0001-01-01)

Update 21.02.2016: Added values for QR decomposition with pivoting and QuantLib performance improvements.

Least Squares Monte Carlo simulations spend a significant amount of the total computation time on the generalized least squares especially if the problem itself has a high dimensional state.  Preferred techniques to solve the normal equations are the QR decomposition

![A = Q\cdot R](img/97c2f8703e9053349ddbf5de6e2a9f09.png)

where ![Q](img/cce0ee434ca4714e77d346c4f6ebf573.png) is orthogonal and ![R](img/e44744d666c5e2e22c0d42b61e9631f9.png) is upper triangular or the singular value decomposition (SVD)

![A = U\cdot w \cdot V^T](img/329d3f5695e52894845c07096ea0544f.png)

where ![U](img/11464e262320dc0222962f3337ef8705.png) is column-orthogonal, ![V](img/77bb324491ef895001cc13da1d0208f6.png)  is an orthogonal matrix and ![w](img/91e16cf334dc7440d37f9b5fa24cabb2.png) is a positive semi-definite diagonal matrix. The Cholesky Factorization

![A = L \cdot L^T](img/d1eac0f4a43b0f06fd99754089769fb9.png)

where ![L](img/c48829d076e0b243fc2be1c334f78ee6.png) is a lower triangular is the fasted method but often numerically unstable. The author in [1] summaries all methods and also outlines the computational efforts involved for ![m](img/29a5c6972bfb9cdcfcd544dd4275dd4e.png) observations and ![n](img/17deaa124310c647ec1dd85566e7b1e5.png) parameters as

*   Chlolesky Factorization: costs ![\sim mn^2 + n^3/3](img/74dcbbe9f5f17ef045f6d903f6d714f0.png) flops
*   QR decomposition: costs ![\sim 2mn^2 - 2n^3/3](img/8486852953b5f615cfc5251d42bfe62f.png) flops
*   Singular value decomposition: costs ![2mn^2 + 11n^3](img/32e1547543a25a084394074a6c63756e.png) flops

For LSMC simulations we have ![m\gg n](img/1fff5960e40f94102b3cbb63eb790640.png) and therefore the QR decomposition has no computational advantages over the SVD.  Since a QR decomposition without column pivoting has numerical problems if ![A](img/f6c194c9a4ae3b06df69cda19cb6b1e8.png) is rank-deficient, the singular value decomposition is often the method of choice for LSMC simulations.

All three decomposition methods are available in [QuantLib](http://quantlib.org/index.shtml), in [LAPACK](http://www.netlib.org/lapack/) (with or without optimized [OpenBLAS](http://www.openblas.net/) library) and in Intel’s [MKL](https://software.intel.com/en-us/intel-mkl) library. A standard Swing option valuation via LSMC should serve as a test bed to measure the performance of the QR decomposition with and without column pivoting and of the SVD algorithm. For LAPACK and MKL the methods dgels and dgesvd have been used to implement the SVD and the QR decomposition without pivoting whereas QR with pivoting is based on dgeqp3, dormqr and dtrsm.  In order to keep results comparable the single thread performance was measured in all cases. The reference prices are calculated via finite difference methods and all LSMC implementations have led to the same price in line with the reference price. The current QR implementation in QuantLib 1.7 has a performance issue if the number of rows is much larger than the number of columns. For these tests an [improved](https://github.com/lballabio/QuantLib/pull/54/files) version of QuantLib’s QR decomposition has been used.

![swing_perf](img/adb59e4324681b7bcff59dd501bb9cd8.png)

As expected MKL is often the fasted library but the difference between MKL and  LAPACK plus OpenBLAS is small.

[1] Do Q Lee, 2012, [Numerically Efficient Methods for Solving Least Squares Problems](http://math.uchicago.edu/~may/REU2012/REUPapers/Lee.pdf)