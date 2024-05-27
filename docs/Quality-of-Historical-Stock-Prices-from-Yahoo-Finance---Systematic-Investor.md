<!--yml

类别：未分类

日期：2024-05-18 14:30:18

-->

# 来自雅虎财经的历史股价质量 | 系统性投资者

> 来源：[`systematicinvestor.wordpress.com/2014/04/08/quality-of-historical-stock-prices-from-yahoo-finance/#0001-01-01`](https://systematicinvestor.wordpress.com/2014/04/08/quality-of-historical-stock-prices-from-yahoo-finance/#0001-01-01)

我最近研究了投资于[S&P/TSX 60](http://ca.spindices.com/indices/equity/sp-tsx-60-index)指数成分的策略，发现了一些历史数据中无法解释的异常跳动/下跌。为了帮助我发现这些点并删除它们，我创建了一个辅助函数[data.clean()函数在 github 上的 data.r](https://github.com/systematicinvestor/SIT/blob/master/R/data.r)。以下是如何使用[data.clean()函数](https://github.com/systematicinvestor/SIT/blob/master/R/data.r)的示例：

```

##############################################################################
# Load Systematic Investor Toolbox (SIT)
# https://systematicinvestor.wordpress.com/systematic-investor-toolbox/
###############################################################################
setInternet2(TRUE)
con = gzcon(url('http://www.systematicportfolio.com/sit.gz', 'rb'))
    source(con)
close(con)

	###############################################################################
	# S&P/TSX 60 Index as of Mar 31 2014
	# http://ca.spindices.com/indices/equity/sp-tsx-60-index
	###############################################################################	
	load.packages('quantmod')

	tickers = spl('AEM,AGU,ARX,BMO,BNS,ABX,BCE,BB,BBD.B,BAM.A,CCO,CM,CNR,CNQ,COS,CP,CTC.A,CCT,CVE,GIB.A,CPG,ELD,ENB,ECA,ERF,FM,FTS,WN,GIL,G,HSE,IMO,K,L,MG,MFC,MRU,NA,PWT,POT,POW,RCI.B,RY,SAP,SJR.B,SC,SLW,SNC,SLF,SU,TLM,TCK.B,T,TRI,THI,TD,TA,TRP,VRX,YRI')
		tickers = gsub('\\.', '-', tickers)
	tickers.suffix = '.TO'

	data <- new.env()
	for(ticker in tickers)
		data[[ticker]] = getSymbols(paste0(ticker, tickers.suffix), src = 'yahoo', from = '1980-01-01', auto.assign = F)

	###############################################################################
	# Plot Abnormal Series
	###############################################################################
	layout(matrix(1:4,2))	
	plota(data$ARX$Adjusted['2000'], type='p', pch='|', main='ARX Adjusted Price in 2000')	
	plota(data$COS$Adjusted['2000'], type='p', pch='|', main='COS Adjusted Price in 2000')	
	plota(data$ERF$Adjusted['2000'], type='p', pch='|', main='ERF Adjusted Price in 2000')	
	plota(data$YRI$Adjusted['1999'], type='p', pch='|', main='YRI Adjusted Price in 1999')	

	###############################################################################
	# Clean data
	###############################################################################
	data.clean(data, min.ratio = 2)	

```

![plot1](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/04/plot1.png)

```

> data.clean(data, min.ratio = 2)	
Removing BNS TRP have less than 756 observations
Abnormal price found for ARX 23-Jun-2000 Ratio : 124.7
Abnormal price found for ARX 26-Sep-2000 Inverse Ratio : 99.4
Abnormal price found for COS 23-Jun-2000 Ratio : 124.1
Abnormal price found for COS 26-Sep-2000 Inverse Ratio : 101.1
Abnormal price found for ERF 14-Jun-2000 Ratio : 7.9
Abnormal price found for YRI 18-Feb-1998 Ratio : 2.1
Abnormal price found for YRI 25-May-1999 Ratio : 3

```

令人惊讶的是，[加拿大新斯科舍银行（BNS.TO）](http://ca.finance.yahoo.com/q/hp?s=BNS.TO)只有一年的历史数据。我也没有找到关于 2000 年 ARX、COS、ERF 跳动的解释。

接下来，我对[S&P 100](http://ca.spindices.com/indices/equity/sp-100)指数中的股票进行了同样的分析：

```

	###############################################################################
	# S&P 100 as of Mar 31 2014
	# http://ca.spindices.com/indices/equity/sp-100
	###############################################################################	
	tickers = spl('MMM,ABT,ABBV,ACN,ALL,MO,AMZN,AXP,AIG,AMGN,APC,APA,AAPL,T,BAC,BAX,BRK.B,BIIB,BA,BMY,COF,CAT,CVX,CSCO,C,KO,CL,CMCSA,COP,COST,CVS,DVN,DOW,DD,EBAY,EMC,EMR,EXC,XOM,FB,FDX,F,FCX,GD,GE,GM,GILD,GS,GOOG,HAL,HPQ,HD,HON,INTC,IBM,JNJ,JPM,LLY,LMT,LOW,MA,MCD,MDT,MRK,MET,MSFT,MDLZ,MON,MS,NOV,NKE,NSC,OXY,ORCL,PEP,PFE,PM,PG,QCOM,RTN,SLB,SPG,SO,SBUX,TGT,TXN,BK,TWX,FOXA,UNP,UPS,UTX,UNH,USB,VZ,V,WMT,WAG,DIS,WFC')
	tickers.suffix = ''

	data <- new.env()
	for(ticker in tickers)
		data[[ticker]] = getSymbols(paste0(ticker, tickers.suffix), src = 'yahoo', from = '1980-01-01', auto.assign = F)

	###############################################################################
	# Plot Abnormal Series
	###############################################################################    
	layout(matrix(1:4,2))	
	plota(data$AAPL$Adjusted['2000'], type='p', pch='|', main='AAPL Adjusted Price in 2000')	
	plota(data$AIG$Adjusted['2008'], type='p', pch='|', main='AIG Adjusted Price in 2008')	
	plota(data$FDX$Adjusted['1982'], type='p', pch='|', main='1982 Adjusted Price in 1982')	

	###############################################################################
	# Clean data
	###############################################################################
	data.clean(data, min.ratio = 2)	

```

![plot2](https://systematicinvestor.wordpress.com/wp-content/uploads/2014/04/plot2.png)

```

> data.clean(data, min.ratio = 2)	
Removing ABBV FB have less than 756 observations
Abnormal price found for AAPL 29-Sep-2000 Inverse Ratio : 2.1
Abnormal price found for AIG 15-Sep-2008 Inverse Ratio : 2.6
Abnormal price found for FDX 13-May-1982 Ratio : 8
Abnormal price found for FDX 06-Aug-1982 Ratio : 7.8
Abnormal price found for FDX 14-May-1982 Inverse Ratio : 8
Abnormal price found for FDX 09-Aug-1982 Inverse Ratio : 8

```

我最初以为 2000 年 9 月 29 日苹果公司（AAPL）的下跌是数据错误；然而，我找到了以下新闻：[苹果打击科技行业，2000 年 9 月 29 日：下午 4:33](http://cnnfn.cnn.com/2000/09/29/markets/techwrap/)电脑制造商的警告对硬件、芯片股造成了压力；纳斯达克大幅下跌。

因此，处理数据需要一些数据操作和一些侦探工作。请在运行任何回测或得出任何结论之前，务必查看数据。
