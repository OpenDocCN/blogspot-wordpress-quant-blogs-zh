<!--yml

分类：未分类

日期：2024-05-18 08:08:30

-->

# R 语言中最小二乘法和最大似然估计校准 | 量角器角落

> 来源：[`quantcorner.wordpress.com/2013/11/17/least-squares-and-maximum-likelihood-estimation-calibration-with-r/#0001-01-01`](https://quantcorner.wordpress.com/2013/11/17/least-squares-and-maximum-likelihood-estimation-calibration-with-r/#0001-01-01)

在这篇简短的文章中，我们提供了**最小二乘法**（**LS**）和**最大似然估计**（**MLE**）的代码片段。它们基于 www.sitmo.com 上的[校准奥恩斯坦-乌伦贝克（瓦西克）模型](http://www.sitmo.com/article/calibrating-the-ornstein-uhlenbeck-model/ "Calibrating the Ornstein-Uhlenbeck (Vasicek) model")。人们还可以阅读由威廉·史密斯撰写的文章[关于均值回归奥恩斯坦-乌伦贝克过程的模拟和估计](http://commoditymodels.files.wordpress.com/2010/02/estimating-the-parameters-of-a-mean-reverting-ornstein-uhlenbeck-process1.pdf "On the Simulation and Estimation of the Mean-Reverting Ornstein-Uhlenbeck Process")。这篇文章很直接。

```
###################################################
# Édouard Tallent @ TaGoMa.Tech, November 2013    #
# QuantCorner @ https://quantcorner.wordpress.com  #
###################################################

# Least Squares Calibration
# Please see http://www.sitmo.com/article/calibrating-the-ornstein-uhlenbeck-model/

S <- c(3, 1.76, 1.2693, 1.196, 0.9468,
        0.9532, 0.6252, 0.8604, 1.0984,
        1.431, 1.3019, 1.4005, 1.2686,
        0.7147, 0.9237, 0.7297, 0.7105,
        0.8683, 0.7406, 0.7314, 0.6232)
n <- 20
delta <- 0.25

Sx <- sum(S[1:length(S)-1])
Sy <- sum(S[2:length(S)])
Sxx <- crossprod(S[1:length(S)-1], S[1:length(S)-1])
Sxy <- crossprod(S[1:length(S)-1], S[2:length(S)])
Syy <- crossprod(S[2:length(S)], S[2:length(S)])

a  <- (n*Sxy - Sx * Sy ) / ( n * Sxx - Sx² )
b  <- (Sy - a * Sx ) / n
sd <- sqrt((n * Syy - Sy² - a * (n * Sxy - Sx * Sy)) / (n * (n-2)))

lambda <- -log(a)/delta
mu <- b/(1-a)
sigma <- sd * sqrt( -2*log(a)/delta/(1-a²))
```

```
###################################################
# Édouard Tallent @ TaGoMa.Tech, November 2013    #
# QuantCorner @ https://quantcorner.wordpress.com  #
###################################################

# Maximum Likelihood Calibration
# PLease, see http://www.sitmo.com/article/calibrating-the-ornstein-uhlenbeck-model/

S <- c(3, 1.76, 1.2693, 1.196, 0.9468,
        0.9532, 0.6252, 0.8604, 1.0984,
        1.431, 1.3019, 1.4005, 1.2686,
        0.7147, 0.9237, 0.7297, 0.7105,
        0.8683, 0.7406, 0.7314, 0.6232)
n <- 20
delta <- 0.25

Sx <- sum(S[1:length(S)-1])
Sy <- sum(S[2:length(S)])
Sxx <- crossprod(S[1:length(S)-1], S[1:length(S)-1])
Sxy <- crossprod(S[1:length(S)-1], S[2:length(S)])
Syy <- crossprod(S[2:length(S)], S[2:length(S)])

mu  <- (Sy * Sxx - Sx * Sxy) / (n* (Sxx - Sxy) - (Sx² - Sx*Sy) )
lambda <- -log((Sxy - mu * Sx - mu * Sy + n * mu²) /   (Sxx - 2 * mu * Sx + n * mu²)) / delta
a <- exp(-lambda*delta)
sigmah2 <- (Syy - 2 * a * Sxy + a² * Sxx - 2 * mu * (1-a) * (Sy - a * Sx) + n * mu² * (1 - a)²)/n
sigma <- sqrt(sigmah2 * 2 * lambda / (1 - a²))
```
