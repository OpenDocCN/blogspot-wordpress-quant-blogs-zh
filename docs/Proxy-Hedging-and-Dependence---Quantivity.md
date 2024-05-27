<!--yml

类别：未分类

日期：2024-05-18 13:47:29

-->

# 代理对冲和相依性 | Quantivity

> 来源：[`quantivity.wordpress.com/2011/10/26/proxy-cross-hedge-correlation-dependence/#0001-01-01`](https://quantivity.wordpress.com/2011/10/26/proxy-cross-hedge-correlation-dependence/#0001-01-01)

当被问及他们对[代理/交叉对冲](https://quantivity.wordpress.com/2011/10/02/proxy-cross-hedging)方法进行总结时，许多大银行的资深人士将其简化为一个相关性：使用一个相关系数接近-1 的乐器进行对冲。这个观点与流行的实践文献相符，例如最近出版的书籍[Hedging Market Exposures](http://books.google.com/books?id=CpSv76NCmJcC)（Bychuk 和 Haughey, 2011）。此外，这个观点也是大量研究文献的核心，追溯到最优对冲比率的原始定义![\hat{\beta}](img/bf55cafee1613728641a3fb0910e4efd.png)（例如[Hull](http://books.google.com/books?id=sEmQZoHoJCcC)，第 57 页）：

![\hat{\beta} = \rho ( \frac{\sigma_u}{\sigma_h} )](img/30b7f48f8ea271361d9846df5d20f083.png)

然而，虽然确实如此，但在实践中对于对冲众所周知的中等股并不非常有帮助，如前所述——因为没有其他相关性的乐器存在。这促使我们重新审视对冲中的相依性角色，揭示可能是一个有趣的结果：*多周期渐近完美对冲存在![\rho \ll -1](img/e14f50fc2c19ba1275fcec675d240476.png)*。

为了推导这个结果，首先问一个简单的问题：在基础和避险之间的相关性范围内，一个完美对冲可能被构建在哪里？当评估为*一个周期*时，答案显然是一个值：![\rho = -1](img/eacdc8ab71faed0d58e774b80ade78d2.png)，因为![\epsilon > 0](img/1fa69ea1fea10840411735cfa4278f5a.png)对于其他任何相关性，给定：

![\rho \ne -1 \iff u \ne h](img/c4e359f890c687398fa435430f81ab67.png)。

然而，这个问题在泛化为*多个周期*时变得更加有趣。特别是，考虑多个连续周期内代理误差的时序系列：

![\{ \epsilon_{t_1}, \epsilon_{t_2}, \dots, \epsilon_{t_n} \} = \boldsymbol{\epsilon}](img/757ee6fcc0a3975439dd60401f794132.png)

能否通过直接建模![\boldsymbol{\epsilon}](img/0853a698c25ab23f3bfd567f6ec6431b.png)的时间演变，而不是描述![u](img/3e3dc85b695f49b6073b5656627101bb.png)和![h](img/proxy-correlation-sin1.png)

这个模型很有趣，因为它捕捉到了最优代理对冲的两个理想属性：

+   **零交叉**：误差在其路径上正数次穿过零点（由下面的 `zerocross` 参数确定），提供频繁的零损失对冲退出机会（*即* ![ \boldsymbol{\epsilon} = 0](img/60da9003031e0d7455c0ab3c9571fdb4.png)）

+   **绝对界限**：误差被限制在上下两个边界内，不超过某个最大阈值。

这两个属性对于交易相对价值策略的读者来说应该是熟悉的。

鉴于上述时间演变的![\boldsymbol{\epsilon}](img/0853a698c25ab23f3bfd567f6ec6431b.png)，下一个问题是询问给定![h](img/1aeb683dd8e8cbb4ed875f43ce92850d.png) 和 ![u](img/3e3dc85b695f49b6073b5656627101bb.png) 的任意路径，可能出现的![\rho](img/3e72a82f16831a4135a859a809b7fe10.png) 范围。正如常言道，一图胜过千言万语。

定义 ![u](img/3e3dc85b695f49b6073b5656627101bb.png) 遵循长度为 ![n](img/4f0c9881324df3a61e8d3cc580ec06e6.png) 的随机过程，其值从高斯分布中绘制（给定 ![ \mu](img/9c754889c3ac09f75741e7f39896143d.png) 和 ![ \sigma](img/527f0b49e7d8291d393b5c36137fd2d0.png) 参数）：

```

u <- rnorm(n, mu, sd);

```

换句话说，基础遵循一个随机过程，这似乎是合理的。鉴于此，![h](img/1aeb683dd8e8cbb4ed875f43ce92850d.png) 被确定为算术差异，给定正弦曲线的离散微分 ![ \epsilon](img/fa45401b4ac499b260e1f16cdc22b992.png) 和期望的零交叉数：

```

e <- (sin(seq(-zerocross*pi, zerocross*pi, len = n)) + 0.01) / 10
de <- diff(e)
h <- de - u

```

以下图表说明了一条样本路径 ![u](img/3e3dc85b695f49b6073b5656627101bb.png)，及其相应的 ![h](img/1aeb683dd8e8cbb4ed875f43ce92850d.png)，跨越多个周期（参数 `n=200; zerocross=1; mu=0; sd=0.05`）：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/10/proxy-correlation-1-returns.png)

这些收益看起来相当正常，尽管明显是从一个既没有长尾也没有记忆的分布中抽样得到的。

给定基础和对冲，相关密度可以通过对 ![u](img/3e3dc85b695f49b6073b5656627101bb.png) 进行抽样生成：

```

cor(h, u, method="kendall")

```

以下图表说明了模拟散点图和经验密度，对于给定 1000 次迭代（参数 `n=200; zerocross=1; mu=0; sd=0.05`）：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/10/proxy-correlation-1-mc.png)

对于单个零交叉，该模型恢复了经典的一期最优对冲结果：![\rho \approx -1](img/ca5c170ff097b68a7dae332f5869d3e2.png)。

当零交叉数增加到 1 以上时，这个模型变得有趣起来。这样做会使模型从经典的单周期中脱离出来，概念上延长时间跨越多个周期。以下图表说明了当零交叉为 10 时的收益：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/10/proxy-correlation-10-returns.png)

累积回报图的视觉检查清楚地表明有些不同寻常的事情正在发生。显然，底层和套期保值并不像完美反向，当零交叉更多时。更深层次的因素正在起作用。为了进一步说明，考虑相应的抽样相关性图表：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/10/proxy-correlation-10-mc.png)

说明相关性从-1 开始分歧，接近-0.73 峰值。记住这是底层和套期保值的相关性，在有限的时间点上提供了*渐进最优性*。这是偶然的，还是代表了一个更普遍原则在起作用？考虑以下带有 50 个零交叉的代理误差回报图：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/10/proxy-correlation-50-returns.png)

现在底层和套期保值看起来并不像彼此，除了它们的大方向一致性地相反。再次，考虑相应的相关性图表，它说明抽样相关性减少到接近-0.30 密度的峰值。

![](https://quantivity.wordpress.com/wp-content/uploads/2011/10/proxy-correlation-50-mc.png)

这或许展示了一个有趣的成果，即对于代理对冲的完美负相关性传统观念的的反例，尽管只是理论上。

* * *

生成上述抽样和图表的 R 代码：

```

proxyMultiPeriodCorrelation <- function(i=100, zerocross=20, n=200, mu=0, 
                                        sd=0.05, doPlot=FALSE)
{
  # Monte carlo sampling for visualizing multi-period correlation dynamics.
  #
  # Args:
  #     i: number of sampling iterations
  #     zerocross: number of zero crosses for error
  #     n: number of iterations for error sin curve
  #     mu: mean of Gaussian samples for u
  #     sd: standard deviation of Gaussian samples for u
  #     doPlot: flag to indicate whether to plot returns
  #
  # Returns: vector of sampled correlations

  e <- (sin(seq(-zerocross*pi, zerocross*pi, len = n)) + 0.01) / 10
  de <- diff(e)

  cors <- sapply(c(1:i), function(i){ 
    u <- rnorm(length(de),mu,sd); 
    h <- de - u;
    pair <- u + h
    c <- cor(h, u, method="kendall");

    if (doPlot)
    {
      oldpar <- par(mfrow=c(2,1))
      plot(u, type='l', xlab="Time", ylab="Returns", main="Optimal Proxy Returns");
      lines(h, col=colors[2])
      legend("topleft",legend=c("Underlying", "Hedge"), fill=colors, cex=0.5)

      cumH <- cumprod(1+h)-1
      cumU <- cumprod(1+u)-1

      plot(cumU,ylim=c(min(cumH,cumU,e),max(cumH,cumU,e)), type='l', ylab="Cumulative Return", xlab="Time", main="Optimal Proxy Cumulative Returns")
      lines(cumH, col=colors[2])
      lines(e, col=colors[3]);
      legend("topleft",legend=c("Underlying", "Hedge", "Error"), fill=colors, cex=0.5)
      par(oldpar)
    }

    return (c)
  })

  oldpar <- par(mfrow=c(2,1))
  plot(cors, ylab="Correlation", main="Optimal Proxy Hedge Correlation Scatter")
  plot(density(cors), xlab="Correlation", main="Optimal Proxy Hedge Correlation Density")
  par(oldpar)

  return (cors)
}

```
