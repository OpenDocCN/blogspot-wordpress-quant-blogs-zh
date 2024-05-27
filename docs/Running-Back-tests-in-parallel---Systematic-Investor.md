<!--yml

分类：未分类

日期：2024-05-18 14:31:33

-->

# 并行运行回测 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2013/11/11/running-back-tests-in-parallel/#0001-01-01`](https://systematicinvestor.wordpress.com/2013/11/11/running-back-tests-in-parallel/#0001-01-01)

一旦你开始尝试多种不同的资产配置算法，运行回测的计算时间可能会相当长。解决计算时间问题的一个简单方法就是并行运行回测。也就是说，如果资产配置算法不使用前期持仓来决定当前分配，我们可以同时并行运行多个期间。

在[回测资产配置组合的更新](https://systematicinvestor.wordpress.com/2013/10/24/update-for-backtesting-asset-allocation-portfolios-post/)文章中，我展示了 GitHub 上[strategy.r 文件中的 portfolio.allocation.helper()函数](https://github.com/systematicinvestor/SIT/blob/master/R/strategy.r)。[portfolio.allocation.helper()函数](https://github.com/systematicinvestor/SIT/blob/master/R/strategy.r)是一个用户友好的界面，可以评估在给定的资产宇宙中，以顺序方式评估多种资产配置算法。

以下是来自[回测资产配置组合的更新](https://systematicinvestor.wordpress.com/2013/10/24/update-for-backtesting-asset-allocation-portfolios-post/)文章的示例代码：

```
    #*****************************************************************
    # Code Strategies
    #******************************************************************                    
    obj = portfolio.allocation.helper(data$prices,
        periodicity = 'months', lookback.len = 60,
        min.risk.fns = list(
            EW=equal.weight.portfolio,
            RP=risk.parity.portfolio,
            MD=max.div.portfolio,                      

            MV=min.var.portfolio,
            MVE=min.var.excel.portfolio,
            MV2=min.var2.portfolio,

            MC=min.corr.portfolio,
            MCE=min.corr.excel.portfolio,
            MC2=min.corr2.portfolio,

            MS=max.sharpe.portfolio(),
            ERC = equal.risk.contribution.portfolio,

            # target retunr / risk
            TRET.12 = target.return.portfolio(12/100),                             
            TRISK.10 = target.risk.portfolio(10/100),

            # rso
            RSO.RP.5 = rso.portfolio(risk.parity.portfolio, 5, 500),

            # others
            MMaxLoss = min.maxloss.portfolio,
            MMad = min.mad.portfolio,
            MCVaR = min.cvar.portfolio,
            MCDaR = min.cdar.portfolio,
            MMadDown = min.mad.downside.portfolio,
            MRiskDown = min.risk.downside.portfolio,
            MCorCov = min.cor.insteadof.cov.portfolio
        )
    )

```

为了并行运行相同的策略，我在 GitHub 上的[strategy.r 文件中创建了 portfolio.allocation.helper.parallel()函数](https://github.com/systematicinvestor/SIT/blob/master/R/strategy.r)。你需要指定一个额外的输入：核心数——用于计算的 CPU 处理器数量。

例如，下面的代码将使用 2 个 CPU 处理器来运行回测计算。它比[portfolio.allocation.helper()函数](https://github.com/systematicinvestor/SIT/blob/master/R/strategy.r)运行得更快。

```
    #*****************************************************************
    # Code Strategies
    #******************************************************************                    
    obj = portfolio.allocation.helper.parallel(cores = 2, data$prices,
        periodicity = 'months', lookback.len = 60,
        min.risk.fns = list(
            EW=equal.weight.portfolio,
            RP=risk.parity.portfolio,
            MD=max.div.portfolio,                      

            MV=min.var.portfolio,
            MVE=min.var.excel.portfolio,
            MV2=min.var2.portfolio,

            MC=min.corr.portfolio,
            MCE=min.corr.excel.portfolio,
            MC2=min.corr2.portfolio,

            MS=max.sharpe.portfolio(),
            ERC = equal.risk.contribution.portfolio,

            # target retunr / risk
            TRET.12 = target.return.portfolio(12/100),                             
            TRISK.10 = target.risk.portfolio(10/100),

            # rso
            RSO.RP.5 = rso.portfolio(risk.parity.portfolio, 5, 500),

            # others
            MMaxLoss = min.maxloss.portfolio,
            MMad = min.mad.portfolio,
            MCVaR = min.cvar.portfolio,
            MCDaR = min.cdar.portfolio,
            MMadDown = min.mad.downside.portfolio,
            MRiskDown = min.risk.downside.portfolio,
            MCorCov = min.cor.insteadof.cov.portfolio
        )
    )

```

希望我没有破坏你那悠长的午餐计划:)
