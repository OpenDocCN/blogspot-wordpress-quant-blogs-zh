<!--yml
category: 未分类
date: 2024-05-17 23:42:14
-->

# Solving Sparse Linear Systems using CUSP and CUDA – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2011/11/13/solving-sparse-linear-systems-using-cusp-and-cuda/#0001-01-01](https://hpcquantlib.wordpress.com/2011/11/13/solving-sparse-linear-systems-using-cusp-and-cuda/#0001-01-01)

A finite difference equation can be represented and solved based on a sparse linear system. When using schemes with implicit parts to solve the equation one needs to calculate the inverse of this sparse matrix. Iterative solvers like the BiCGStab algorithm (plus preconditioner) are tailor-made for these kind of problems. In addition these solvers can easily be adapted to parallel computing architectures like modern GPUs. The cusp library [1] implements a set of common iterative solvers for sparse matrices based on CUDA and thrust [2].

Alternatively operator splitting techniques can be used to solve the problem. In this case only tridiagonal linear systems have to be inverted. The Thomas algorithm (named after Liewellyn Thomas) can solve such systems in ![O(n)](img/96728d95b82ba397b34d5747dcae71df.png) operations instead of ![O(n^3)](img/fbc716f86b4dc2e159077e5ea61995e1.png) operations required by the Gaussian elimination. But it is not easy to parallelize the Thomas algorithm.

On a CPU operator splitting usually outperforms iterative solvers like BiCGStab for the implicit part. The VPP pricing problem from the previous blog entries will now serve as a benchmark to compare the solver performance on the CPU against a GPU. As can be seen in the diagram below on a CPU operator splitting is faster than the BiCGStab solver plus preconditioner. But the BiCGStab on the GPU clearly gains the lead even though the corresponding preconditioner for the GPU has not been implemented yet. Please find the interface class between QuantLib/boost::ublas and cusp [here](http://www.hpc-quantlib.de/src/gpubicgstab.zip). [](https://hpcquantlib.wordpress.com/wp-content/uploads/2011/11/plot2.png) [![](img/fd2dec968687852b5795f80d4a27c8db.png "plot")](https://hpcquantlib.wordpress.com/wp-content/uploads/2011/11/plot4.png) [](https://hpcquantlib.wordpress.com/wp-content/uploads/2011/11/plot1.png) 

[1] cusp, [Generic Parallel Algorithms for Sparse Matrix and Graph Computations](http://code.google.com/p/cusp-library/)

[2] thrust, [Code at the speed of light](http://code.google.com/p/thrust/)