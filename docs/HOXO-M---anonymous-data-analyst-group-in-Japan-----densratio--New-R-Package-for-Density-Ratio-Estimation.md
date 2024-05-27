<!--yml

分类：未分类

日期：2024-05-18 06:47:49

-->

# HOXO-M - 日本匿名数据分析小组 - ：densratio：密度比估计的新 R 包

> 来源：[`mockquant.blogspot.com/2016/04/densratio-new-r-package-for-density.html#0001-01-01`](http://mockquant.blogspot.com/2016/04/densratio-new-r-package-for-density.html#0001-01-01)

## 1\. 概述

**密度比估计**描述如下：对于给定的来自未知分布$p(x)$和$q(y)$的两个数据样本$x$和$y$，估计 $$ w(x) = \frac{p(x)}{q(x)} $$ 其中$x$和$y$是$d$-维实数。

估计的密度比函数$w(x)$可以用于许多应用，例如基于内点的异常检测[1]和协变量转移适应[2]。关于密度比估计的其他有用应用是由 Sugiyama et al. (2012) [3]总结的。

包**densratio**提供了一个名为`densratio()`的函数，它返回一个具有估计密度比`compute_density_ratio()`的结果。

例如，

```
set.seed(3)
x <- rnorm(200, mean = 1, sd = 1/8)
y <- rnorm(200, mean = 1, sd = 1/2)

library(densratio)
result <- densratio(x, y)
result
```

```
## 
## Call:
## densratio(x = x, y = y, method = "uLSIF")
## 
## Kernel Information:
##   Kernel type:  Gaussian RBF 
##   Number of kernels:  100 
##   Bandwidth(sigma):  0.1 
##   Centers:  num [1:100, 1] 1.007 0.752 0.917 0.824 0.7 ...
## 
## Kernel Weights(alpha):
##   num [1:100] 0.4044 0.0479 0.1736 0.125 0.0597 ...
## 
## The Function to Estimate Density Ratio:
##   compute_density_ratio()
```

在这种情况下，真实密度比$w(x)$是已知的，所以我们可以将$w(x)$与估计的密度比$\hat{w}(x)$进行比较。

```
true_density_ratio <- function(x) dnorm(x, 1, 1/8) / dnorm(x, 1, 1/2)
estimated_density_ratio <- result$compute_density_ratio

plot(true_density_ratio, xlim=c(-1, 3), lwd=2, col="red", xlab = "x", ylab = "Density Ratio")
plot(estimated_density_ratio, xlim=c(-1, 3), lwd=2, col="green", add=TRUE)
legend("topright", legend=c(expression(w(x)), expression(hat(w)(x))), col=2:3, lty=1, lwd=2, pch=NA)
```

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhQdqp_r8q8fbiM4iVE7wNKdMaOKh65ZLg8hd-hsEOOA6IDjHgZvKxp-6mORmqPKN6FlzXQnAr78f6wyfuhnt8JE2EIlk0HBPi66E8jU8R56JBN70lFj3iat_P3N_U7jwrEna_IrZea9Sg/s1600/unnamed-chunk-1-1.png)

## 2\. 安装方法

你可以从[CRAN](https://cran.r-project.org/web/packages/densratio/)安装**densratio**包。

```
install.packages("densratio")
```

你也可以从 GitHub 安装这个包。

```
install.packages("devtools") # if you have not installed "devtools" package
devtools::install_github("hoxo-m/densratio")
```

**densratio**包的源代码可在 GitHub 上获得

## 3\. 详细信息

### 3.1\. 基础知识

该包提供了`densratio()`，该结果具有估计密度比的功能。

对于数据样本`x`和`y`，

```
library(densratio)

x <- rnorm(200, mean = 1, sd = 1/8)
y <- rnorm(200, mean = 1, sd = 1/2)

result <- densratio(x, y)
```

在这种情况下，`result$compute_density_ratio()`可以计算估计的密度比。

```
w_hat <- result$compute_density_ratio(y)
plot(y, w_hat)
```

### 3.2\. 方法

`densratio()`有一个`method`参数，你可以传递`"uLSIF"`或`"KLIEP"`。

+   **uLSIF**（无约束最小二乘重要度拟合）是默认方法。此算法通过最小化平方损失来估计密度比。你可以在 Hido et al. (2011) [1]中找到更多信息。

+   **KLIEP**（Kullback-Leibler Importance Estimation Procedure）是另一种方法。此算法通过最小化 Kullback-Leibler 散度来估计密度比。你可以在 Sugiyama et al. (2007) [2]中找到更多信息。

两种方法都假设密度比由线性模型表示：$$ w(x) = \alpha_1 K(x, c_1) + \alpha_2 K(x, c_2) + ... + \alpha_b K(x, c_b) $$ 其中 $$ K(x, c) = \exp\left(\frac{-\|x - c\|²}{2 \sigma ^ 2}\right) $$ 是高斯 RBF。

`densratio()`执行着两个主要任务：

+   首先，决定核权重$\alpha$，

+   其次，通过交叉验证确定核参数$\sigma$，

结果是，你可以获得`compute_density_ratio()`。

### 3.3\. 结果和参数设置

`densratio()`的输出结果如下所示：

```
## 
## Call:
## densratio(x = x, y = y, method = "uLSIF")
## 
## Kernel Information:
##   Kernel type:  Gaussian RBF 
##   Number of kernels:  100 
##   Bandwidth(sigma):  0.1 
##   Centers:  num [1:100, 1] 1.007 0.752 0.917 0.824 0.7 ...
## 
## Kernel Weights(alpha):
##   num [1:100] 0.4044 0.0479 0.1736 0.125 0.0597 ...
## 
## Regularization Parameter(lambda):  
## 
## The Function to Estimate Density Ratio:
##   compute_density_ratio()
```

+   **核类型**固定为高斯 RBF。

+   **核的数量**是线性模型中核的数量。你可以通过设置`kernel_num`参数进行更改。默认情况下，`kernel_num = 100`。

+   **带宽（sigma）**是高斯核的带宽。默认情况下，`sigma = "auto"`，算法会通过交叉验证自动选择最佳值。如果你设置`sigma`为一个数字，那么它将被使用。如果你设置一个数值向量，算法将通过交叉验证在其中选择最佳值。

+   **中心**是线性模型中高斯核的中心。这些是从分子分布`p_nu(x)`下潜在数据样本`x`中随机选择的。你可以在`result$kernel_info$centers`中找到所有值。

+   **核权重**是线性模型中的 alpha 参数。它是由算法进行优化的。你可以在`result$alpha`中找到所有值。

+   **估计密度比的函数**被命名为`compute_density_ratio()`。

## 4\. 多维数据样本

在上文中，输入数据样本`x`和`y`是一维的。`densratio()`允许输入作为`矩阵`的多维数据样本。

例如，

```
library(densratio)
library(mvtnorm)

set.seed(71)
x <- rmvnorm(300, mean = c(1, 1), sigma = diag(1/8, 2))
y <- rmvnorm(300, mean = c(1, 1), sigma = diag(1/2, 2))

result <- densratio(x, y)
result
```

```
## 
## Call:
## densratio(x = x, y = y, method = "uLSIF")
## 
## Kernel Information:
##   Kernel type:  Gaussian RBF 
##   Number of kernels:  100 
##   Bandwidth(sigma):  0.316 
##   Centers:  num [1:100, 1:2] 1.178 0.863 1.453 0.961 0.831 ...
## 
## Kernel Weights(alpha):
##   num [1:100] 0.145 0.128 0.138 0.187 0.303 ...
## 
## Regularization Parameter(lambda):  0.1 
## 
## The Function to Estimate Density Ratio:
##   compute_density_ratio()
```

同样，在这种情况下，我们可以比较真实密度比和估计密度比。

```
true_density_ratio <- function(x) {
  dmvnorm(x, mean = c(1, 1), sigma = diag(1/8, 2)) /
    dmvnorm(x, mean = c(1, 1), sigma = diag(1/2, 2))
}
estimated_density_ratio <- result$compute_density_ratio

N <- 20
range <- seq(0, 2, length.out = N)
input <- expand.grid(range, range)
z_true <- matrix(true_density_ratio(input), nrow = N)
z_hat <- matrix(estimated_density_ratio(input), nrow = N)

par(mfrow = c(1, 2))
contour(range, range, z_true, main = "True Density Ratio")
contour(range, range, z_hat, main = "Estimated Density Ratio")
```

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjkW1oxCEr4i3Z-Uk5ALQ70m1_sgd5_4oOwS5HQ0Jc2zg_qDHNs6HrzQbEsXmkIQo23lF7N89q-6VEWEx-1KK0-ohX6uRT9amNXqdc7CoMKhkMPzd9CUdwlQ9Ykl0RcqTjB_Wq6-7FA-nA/s1600/unnamed-chunk-6-1.png)

`x`和`y`的维度必须相同。

## 5\. 参考资料

[1] Hido, S., Tsuboi, Y., Kashima, H., Sugiyama, M., & Kanamori, T. **使用直接密度比估计的统计离群点检测**。知识与信息系统，2011 年。

[2] Sugiyama, M., Nakajima, S., Kashima, H., von Bünau, P. & Kawanabe, M. **具有模型选择的直接重要性估计及其在协变量转移适应中的应用**。NIPS 2007 年。

[3] Sugiyama, M., Suzuki, T. & Kanamori, T. **机器学习中的密度比估计**。剑桥大学出版社，2012 年。
