```yml

类别：未分类

date: 2024-05-18 15:12:56

```

# 及时投资组合：做空 Mebane Faber

> 来源：[`timelyportfolio.blogspot.com/2011/07/shorting-mebane-faber.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/07/shorting-mebane-faber.html#0001-01-01)

```
require(quantmod)
require(PerformanceAnalytics)   #completely from the PerformanceAnalytics package chart.RiskReturn
#cannot claim any of the credit for the fine work in this package   chart.DrawdownReturn <- function (R, Rf = 0, main = "Annualized Return and Worst Drawdown", add.names = TRUE, 
    xlab = "WorstDrawdown", ylab = "Annualized Return", method = "calc", 
    geometric = TRUE, scale = NA, add.sharpe = c(1, 2, 3), add.boxplots = FALSE, 
    colorset = 1, symbolset = 1, element.color = "darkgray", 
    legend.loc = NULL, xlim = NULL, ylim = NULL, cex.legend = 1, 
    cex.axis = 0.8, cex.main = 1, cex.lab = 1, ...) 
{
    if (method == "calc") 
        x = checkData(R, method = "zoo")
    else x = t(R)
    if (!is.null(dim(Rf))) 
        Rf = checkData(Rf, method = "zoo")
    columns = ncol(x)
    rows = nrow(x)
    columnnames = colnames(x)
    rownames = rownames(x)
    if (length(colorset) < columns) 
        colorset = rep(colorset, length.out = columns)
    if (length(symbolset) < columns) 
        symbolset = rep(symbolset, length.out = columns)
    if (method == "calc") {
        comparison = cbind(t(Return.annualized(x[, columns:1])),
		t(maxDrawdown(x[, columns:1])))
        returns = comparison[, 1]
        risk = comparison[, 2]
        rnames = row.names(comparison)
    }
    else {
        x = t(x[, ncol(x):1])
        returns = x[, 1]
        risk = x[, 2]
        rnames = names(returns)
    }
    if (is.null(xlim[1])) 
        xlim = c(0, max(risk) + 0.02)
    if (is.null(ylim[1])) 
        ylim = c(min(c(0, returns)), max(returns) + 0.02)
    if (add.boxplots) {
        original.layout <- par()
        layout(matrix(c(2, 1, 0, 3), 2, 2, byrow = TRUE), c(1, 
            6), c(4, 1), )
        par(mar = c(1, 1, 5, 2))
    }
    plot(returns ~ risk, xlab = "", ylab = "", las = 1, xlim = xlim, 
        ylim = ylim, col = colorset[columns:1], pch = symbolset[columns:1], 
        axes = FALSE, ...)
    if (ylim[1] != 0) {
        abline(h = 0, col = element.color)
    }
    axis(1, cex.axis = cex.axis, col = element.color)
    axis(2, cex.axis = cex.axis, col = element.color)
    if (!add.boxplots) {
        title(ylab = ylab, cex.lab = cex.lab)
        title(xlab = xlab, cex.lab = cex.lab)
    }
    if (!is.na(add.sharpe[1])) {
        for (line in add.sharpe) {
            abline(a = (Rf * 12), b = add.sharpe[line], col = "gray", 
                lty = 2)
        }
    }
    if (add.names) 
        text(x = risk, y = returns, labels = rnames, pos = 4, 
            cex = 0.8, col = colorset[columns:1])
    rug(side = 1, risk, col = element.color)
    rug(side = 2, returns, col = element.color)
    title(main = main, cex.main = cex.main)
    if (!is.null(legend.loc)) {
        legend(legend.loc, inset = 0.02, text.col = colorset, 
            col = colorset, cex = cex.legend, border.col = element.color, 
            pch = symbolset, bg = "white", legend = columnnames)
    }
    box(col = element.color)
    if (add.boxplots) {
        par(mar = c(1, 2, 5, 1))
        boxplot(returns, axes = FALSE, ylim = ylim)
        title(ylab = ylab, line = 0, cex.lab = cex.lab)
        par(mar = c(5, 1, 1, 2))
        boxplot(risk, horizontal = TRUE, axes = FALSE, ylim = xlim)
        title(xlab = xlab, line = 1, cex.lab = cex.lab)
        par(original.layout)
    }
}     getSymbols("DJIA",src="FRED")
#if you prefer Yahoo! Finance
#getSymbols("^DJI",from="1919-01-01",to=Sys.Date())   DJIA <- to.monthly(DJIA)[,4]
index(DJIA) <- as.Date(index(DJIA))   signalUp <- ifelse(DJIA > runMean(DJIA,n=10), 1, 0)
signalDown <- ifelse(DJIA < runMean(DJIA,n=10), -1, 0)   retUp <- lag(signalUp,k=1)* ROC(DJIA,type="discrete",n=1)
retDown <- lag(signalDown, k=1) * ROC(DJIA,type="discrete",n=1)
ret <- merge(retUp + retDown,retUp,retDown,-retDown,ROC(DJIA,type="discrete",n=1))
colnames(ret) <- c("Combined","LongAbove","ShortBelow","LongBelow","DJIA")   #jpeg(filename="performance summary all.jpg",quality=100,
#	width=6.25, height = 6.25,  units="in",res=96)
charts.PerformanceSummary(ret,ylog=TRUE,
	colorset=c("cadetblue","darkolivegreen3","goldenrod","purple","gray70"),
	main="DJIA 10 Month Moving Average Strategy Comparisons
	May 1896-Jun 2011")
#dev.off()
#jpeg(filename="performance summary before 1932.jpg",quality=100,
#	width=6.25, height = 6.25,  units="in",res=96)
charts.PerformanceSummary(ret["::1932-06",3],ylog=TRUE,
	main="DJIA Short Below 10 Month Moving Average Works
	May 1896-Jun 1932")
#dev.off()
#jpeg(filename="performance summary after 1932.jpg",quality=100,
#	width=6.25, height = 6.25,  units="in",res=96)
charts.PerformanceSummary(ret["1932-07::",3],ylog=TRUE,
	main="DJIA Short Below 10 Month Moving Average Fails
	Jul 1932-Jun 2011")
#dev.off()   #jpeg(filename="drawdown annualized return scatter.jpg",quality=100,
#	width=6.25, height = 6.25,  units="in",res=96)
chart.DrawdownReturn(ret[,1:5])
#dev.off()   #look at risk measures
require(ggplot2)
#jpeg(filename="risk.jpg",quality=100,width=6.25, height = 5, 
#	units="in",res=96) 
downsideTable<-table.DownsideRisk(ret)
downsideTable<-melt(cbind(rownames(downsideTable),
	downsideTable))
colnames(downsideTable)<-c("Statistic","Portfolio","Value")
ggplot(downsideTable, stat="identity",
	aes(x=Statistic,y=Value,fill=Portfolio)) +
	geom_bar(position="dodge") + coord_flip()
#dev.off()
```
