```yaml

类别：未分类

date: 2024-05-18 14:36:41

→

# Permanent Portfolio – Transaction Cost and better Risk Parity | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/10/10/permanent-portfolio-transaction-cost-and-better-risk-parity/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/10/10/permanent-portfolio-transaction-cost-and-better-risk-parity/#0001-01-01)

I want to address comments that were asked in my last post, [Permanent Portfolio – Simple Tools](https://systematicinvestor.wordpress.com/2012/10/05/permanent-portfolio-simple-tools/), about [Permanent Portfolio](https://systematicinvestor.wordpress.com/2012/09/18/permanent-portfolio/) strategy. Specifically:

+   交易成本对表现的影响

+   Create a modified version of risk allocation portfolio that distributes weights across 3 asset classes: stocks(SPY), gold(GLD), and treasuries(TLT), and only invests into cash(SHY) to fill the residual portfolio exposure once we scale the SPY/GLD/TLT portfolio to the target volatility

第一个观点很简单，只需在 bt.run.share()函数调用中添加 commission=0.1 参数，就可以将交易成本纳入回测。例如，要查看假设每股 10 美分的佣金，美元分配策略的表现，请使用以下代码：

```

# original strategy
models$dollar = bt.run.share(data, clean.signal=F)

# assuming 10c a share commissions
models$dollar = bt.run.share(data, commission=0.1, clean.signal=F)

```

第二个观点需要做一些更复杂的工作。首先，让我们只在三个资产类别之间分配风险：股票（SPY）、黄金（GLD）和国债（TLT）。接下来，让我们将 SPY/GLD/TLT 投资组合调整到 7%的目标波动性。最后，让我们将剩余的投资组合风险分配给现金（SHY）。

```

	#*****************************************************************
	# Risk Weighted: allocate only to 3 asset classes: stocks(SPY), gold(GLD), and treasuries(TLT)
	#****************************************************************** 				
	ret.log = bt.apply.matrix(prices, ROC, type='continuous')
	hist.vol = sqrt(252) * bt.apply.matrix(ret.log, runSD, n = 21)	
	weight.risk = weight.dollar / hist.vol
		weight.risk$SHY = 0 
		weight.risk = weight.risk / rowSums(weight.risk)

	data$weight[] = NA
		data$weight[period.ends,] = weight.risk[period.ends,]
	models$risk = bt.run.share(data, commission=commission, clean.signal=F)

	#*****************************************************************
	# Risk Weighted + 7% target volatility
	#****************************************************************** 				
	data$weight[] = NA
		data$weight[period.ends,] = target.vol.strategy(models$risk,
						weight.risk, 7/100, 21, 100/100)[period.ends,]
	models$risk.target7 = bt.run.share(data, commission=commission, clean.signal=F)

	#*****************************************************************
	# Risk Weighted + 7% target volatility + SHY
	#****************************************************************** 				
	data$weight[] = NA
		data$weight[period.ends,] = target.vol.strategy(models$risk,
						weight.risk, 7/100, 21, 100/100)[period.ends,]

  		cash = 1-rowSums(data$weight)
	    data$weight$SHY[period.ends,] = cash[period.ends]
	models$risk.target7.shy = bt.run.share(data, commission=commission, clean.signal=F)

```

![plot1.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot1-small2.png)

![plot2.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot2-small2.png)

![plot3.png.small](https://systematicinvestor.wordpress.com/wp-content/uploads/2012/10/plot3-small1.png)

即使考虑每笔交易 10 美分的成本，修改后的风险分配投资组合的表现仍然优于其他投资组合。

要查看此示例的完整源代码，请查看 GitHub 上的[bt.permanent.portfolio3.test()函数](https://github.com/systematicinvestor/SIT/blob/master/R/bt.test.r)。
