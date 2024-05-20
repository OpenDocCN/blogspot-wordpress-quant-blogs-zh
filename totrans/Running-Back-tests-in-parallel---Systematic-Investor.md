<!--yml
category: 未分类
date: 2024-05-18 14:31:33
-->

# Running Back-tests in parallel | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2013/11/11/running-back-tests-in-parallel/#0001-01-01](https://systematicinvestor.wordpress.com/2013/11/11/running-back-tests-in-parallel/#0001-01-01)

Once you start experimenting with many different asset allocation algorithms, the computation time of running the back-tests can be substantial. One simple way to solve the computation time problem is to run the back-tests in parallel. I.e. if the asset allocation algorithm does not use the prior period holdings to make decision about current allocation, we can run many periods in parallel.

In the [Update for Backtesting Asset Allocation Portfolios](https://systematicinvestor.wordpress.com/2013/10/24/update-for-backtesting-asset-allocation-portfolios-post/) post, I show cased the [portfolio.allocation.helper() function in strategy.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/strategy.r). The [portfolio.allocation.helper() function](https://github.com/systematicinvestor/SIT/blob/master/R/strategy.r) is a user-friendly interface to evaluate multiple asset allocation algorithms over given asset universe in a sequential fashion.

Following is a sample code from the [Update for Backtesting Asset Allocation Portfolios](https://systematicinvestor.wordpress.com/2013/10/24/update-for-backtesting-asset-allocation-portfolios-post/) post:

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

To run the same strategies in parallel, I created the [portfolio.allocation.helper.parallel() function in strategy.r at github](https://github.com/systematicinvestor/SIT/blob/master/R/strategy.r). There is one extra input that you need to specify: cores – number of CPU processors used for computations.

For example, the code below will use 2 CPU processors to run back-test computations. It will run faster than the [portfolio.allocation.helper() function](https://github.com/systematicinvestor/SIT/blob/master/R/strategy.r).

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

Hopefully, I did not ruin your prolong lunch plans 🙂