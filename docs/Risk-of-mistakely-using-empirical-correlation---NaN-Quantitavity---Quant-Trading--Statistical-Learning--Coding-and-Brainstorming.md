<!--yml

分类：未分类

日期：2024-05-18 13:57:17

-->

# 错误使用经验相关性的风险 | NaN 量化 - 量化交易、统计学习、编程和头脑风暴

> 来源：[`quantlife.wordpress.com/2013/04/01/risk-of-mistakely-using-empirical-correlation/#0001-01-01`](https://quantlife.wordpress.com/2013/04/01/risk-of-mistakely-using-empirical-correlation/#0001-01-01)

```
#---------------------------------------------------------------------------------------------
#| Comparing different copula;
#| Showing why empirical correlation will be risky if your assumption
#| of the join distribution (ex: Multi normal vs. t) is not correct.
#|
#| Created by: Nan Zhou
#| Time: 2012-03-05
#---------------------------------------------------------------------------------------------
rm(list=ls())
#memory.size(max=4000)
require(copula)
n = 1000 # number of simulation of random sample
p =0.95 # quantile line for the plot
df = 1 # d.f. of marginal distribution of t
rho = 0.75 # empirical correlation
dist.margin = "norm" # Marginal distribution
#---------------------------------------------------------------------------------------------

#Normal Marginal

mvd.gaussian <- mvdc(copula = ellipCopula(family = "normal", param = rho),
                     margins = rep(dist.margin,2),
                     paramMargins = list(list(mean = 0,sd = 1), list(mean = 0, sd = 1)))

myMvd2 <- mvdc(copula = ellipCopula(family = "t", param = rho, df = df),
                margins = rep(dist.margin,2),
                paramMargins = list(list(mean = 0,sd = 1), list(mean = 0, sd = 1)))

#windows ( width = 150, height = 200)
#layout(matrix(c(1,2,3,3),ncol=2,byrow=TRUE),heights=c(1,2))

par(mfrow=c(3,2))
contour(mvd.gaussian, dmvdc, xlim = c(-3, 3), ylim = c(-3, 3))
title(paste("Gaussian Copula, Margin Dist =", dist.margin, ", rho =", rho, ", df =",df),
        cex.main=.8)
contour(myMvd2, dmvdc, xlim = c(-3, 3), ylim = c(-3, 3))
title(paste("t Copula, Margin Dist =", dist.margin, ", rho =", rho, ", df =",df),
        cex.main=.8)

for (rho in c(0.75,0.25))
for (df in c(1,5))
{
    seed = 1
    lim.plot = c(-3,3)
    u <- rcopula(normalCopula(param = rho, dim = 2), n)
    v <- rcopula(tCopula(param = rho, dim = 2, df = df), n)
    plot(qnorm(u),xlab='x1',ylab='x2',col='blue',cex=0.6,xlim=lim.plot,ylim=lim.plot)
    title(paste("rho=",rho,"df=",df))
    points(qnorm(v),xlab='x1',ylab='x2',col='red',cex=0.6)
    q = qnorm(p)
    abline(v = q)
    abline(h = q)
    text(-2,q,paste(p*100,"% quantile"))
}
```
