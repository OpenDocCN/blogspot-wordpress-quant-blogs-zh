<!--yml
category: 未分类
date: 2024-05-18 08:09:33
-->

# Generation of correlated random numbers: recommended article | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2012/02/29/generation-of-correlated-random-numbers-recommended-article/#0001-01-01](https://quantcorner.wordpress.com/2012/02/29/generation-of-correlated-random-numbers-recommended-article/#0001-01-01)

This quick blog entry to share an excellent article of **Thijs van den Berg** entitled [Generating Correlated Random Numbers](http://www.sitmo.com/article/generating-correlated-random-numbers/#comment-325 "Generating correlated random numbers").

This author describes in a nicely way how to generate sequences of correlated random numbers using the **Cholesky** **decomposition**, and a **Eigenvector decomposition** as well. (I worked out matrices with QuantLib [some time ago](https://quantcorner.wordpress.com/2011/02/20/matrix-decomposition-with-quantlib/ "some time ago").)  A piece of **Matlab** code follows.

This short article is a good opportunity for the reader to get back to some essential statisticals tools/concepts, such as **Eigenvectors** and **Eigenvalues**. One can have a look at **[MathWorld](http://mathworld.wolfram.com "MathWorld"),** for example.

The reader like myself that doesn’t have a **Matlab** license might be tempted to write equivalent code in **R** language. I recommend the [Matrix Algebra in R](http://personality-project.org/r/sem.appendix.1.pdf "Matrix algebra in R") documentation if you need a  refresh on matrices using **R**.

**Example R code using a Cholesky decomposition**: *In-a-shot*, the code corresponding to the **Matlab** snippet of the original article might be as follows :

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