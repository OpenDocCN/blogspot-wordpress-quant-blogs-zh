<!--yml

类别：未分类

日期：2024-05-18 08:09:33

-->

# 相关文章：Generation of correlated random numbers: recommended article | Quant Corner

> 来源：[`quantcorner.wordpress.com/2012/02/29/generation-of-correlated-random-numbers-recommended-article/#0001-01-01`](https://quantcorner.wordpress.com/2012/02/29/generation-of-correlated-random-numbers-recommended-article/#0001-01-01)

这篇简短的博文分享了一篇来自 **Thijs van den Berg** 的优秀文章，名为[生成相关随机数](http://www.sitmo.com/article/generating-correlated-random-numbers/#comment-325 "Generating correlated random numbers")。

本文作者非常巧妙地描述了如何使用 **Cholesky** **decomposition** 和 **Eigenvector decomposition** 生成相关随机数序列（我以前使用 QuantLib[做过矩阵的处理](https://quantcorner.wordpress.com/2011/02/20/matrix-decomposition-with-quantlib/ "some time ago")。）下面是一段 **Matlab** 代码。

这篇简短的文章是读者重新回顾一些基本统计工具/概念的好机会，比如 **Eigenvectors** 和 **Eigenvalues**。例如，您可以去看看**[MathWorld](http://mathworld.wolfram.com "MathWorld")** 的内容。

像我这样没有 **Matlab** 许可证的读者可能会想要使用 **R** 语言编写等效的代码。如果您需要刷新一下使用 **R** 处理矩阵的知识，我推荐看看[使用 R 进行矩阵代数](http://personality-project.org/r/sem.appendix.1.pdf "Matrix algebra in R")文档。

**Cholesky 分解的示例 R 代码**: *In-a-shot*，原文中的 **Matlab** 代码对应的 **R** 代码可能如下：

```
Mat <- matrix(c(1,0.6,0.3,0.6,1,0.5,0.3,0.5,1.0),nrow=3) # matrix creation
Chol <- chol(Mat) # cholesky decomposition
set.seed(123) # sets seed for random number generator
V1 <- rnorm(10, 0, 1)
V2 <- rnorm(10, 0, 1)
V3 <- rnorm(10, 0, 1)
VFin <- cbind(V1, V2, V3) # 3 vectors of 10 rand. norm. numbers
ans <- VFin %*% Chol
```
