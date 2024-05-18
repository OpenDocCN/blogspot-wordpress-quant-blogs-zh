<!--yml
category: 未分类
date: 2024-05-18 15:11:56
-->

# Timely Portfolio: Reporting Good Enough to Share

> 来源：[http://timelyportfolio.blogspot.com/2011/09/reporting-good-enough-to-share.html#0001-01-01](http://timelyportfolio.blogspot.com/2011/09/reporting-good-enough-to-share.html#0001-01-01)

```
#this report uses the PerformanceAnalytics charts.PerformanceSummary
#as the base for a new one-pager
#99% of the code is from the PerformanceAnalytics package
#all credit should be given to the PerformanceAnalytics team
#all errors should be assigned to me

#this is almost entirely from the PerformanceAnalytics
#chart.CumReturns function
#I only change to label the endpoints
na.skip <- function (x, FUN=NULL, ...) # maybe add a trim capability?
{ # @author Brian Peterson

    # DESCRIPTION:

    # Time series data often contains NA's, either due to missing days, 
    # noncontiguous series, or merging multiple series,
    # 
    # Some Calulcations, such as return calculations, require data that 
    # looks like a vector, and needs the output of na.omit
    # 
    # It is often convenient to apply these vector-like functions, but 
    # you still need to keep track of the structure of the oridginal data.

    # Inputs
    # x		the time series to apply FUN too
    # FUN	function to apply
    # ...	any additonal parameters to FUN

    # Outputs:
    # An xts time series that has the same index and NA's as the data 
    # passed in, after applying FUN

    nx <- na.omit(x)
    fx <- FUN(nx, ... = ...)
    if (is.vector(fx)) {
        result <- .xts(fx, .index(x), .indexCLASS = indexClass(x))
    }
    else {
        result <- merge(fx, .xts(, .index(x)))
    }
    return(result)
}

chart.CumReturnsX <-
function (R, wealth.index = FALSE, geometric = TRUE, legend.loc = NULL, colorset = (1:12), begin = c("first","axis"), ...)
{ # @author Peter Carl

    # DESCRIPTION:
    # Cumulates the returns given and draws a line graph of the results as
    # a cumulative return or a "wealth index".

    # Inputs:
    # R: a matrix, data frame, or timeSeries of returns
    # wealth.index:  if true, shows the "value of $1", starting the cumulation
    #    of returns at 1 rather than zero
    # legend.loc: use this to locate the legend, e.g., "topright"
    # colorset: use the name of any of the palattes above
    # method: "none"

    # Outputs:
    # A timeseries line chart of the cumulative return series

    # FUNCTION:

    # Transform input data to a matrix
    begin = begin[1]
    x = checkData(R)

    # Get dimensions and labels
    columns = ncol(x)
    columnnames = colnames(x)

    # Calculate the cumulative return
    one = 0
    if(!wealth.index)
        one = 1

    ##find the longest column, calc cum returns and use it for starting values

    if(begin == "first") {
        length.column.one = length(x[,1])
        # find the row number of the last NA in the first column
        start.row = 1
        start.index = 0
        while(is.na(x[start.row,1])){
            start.row = start.row + 1
        }
        x = x[start.row:length.column.one,]
        if(geometric)
            reference.index = na.skip(x[,1],FUN=function(x) {cumprod(1+x)})
        else
            reference.index = na.skip(x[,1],FUN=function(x) {cumsum(x)})
    }
    for(column in 1:columns) {
        if(begin == "axis") {
            start.index = FALSE
		} else {
    		# find the row number of the last NA in the target column
            start.row = 1
            while(is.na(x[start.row,column])){
                start.row = start.row + 1
            }
            start.index=ifelse(start.row > 1,TRUE,FALSE)
        }
        if(start.index){
	        # we need to "pin" the beginning of the shorter series to the (start date - 1 period) 
	        # value of the reference index while preserving NA's in the shorter series
            if(geometric)
                z = na.skip(x[,column],FUN = function(x,index=reference.index[(start.row - 1)]) {rbind(index,1+x)})
            else
                z = na.skip(x[,column],FUN = function(x,index=reference.index[(start.row - 1)]) {rbind(1+index,1+x)})
        } else {
            z = 1+x[,column] 
        }
        column.Return.cumulative = na.skip(z,FUN = function(x, one, geometric) {if(geometric) cumprod(x)-one else (1-one) + cumsum(x-1)},one=one, geometric=geometric)
        if(column == 1)
            Return.cumulative = column.Return.cumulative
        else
            Return.cumulative = merge(Return.cumulative,column.Return.cumulative)
    }
    if(columns == 1)
        Return.cumulative = as.xts(Return.cumulative)
    colnames(Return.cumulative) = columnnames

    # Chart the cumulative returns series
    chart.TimeSeries(Return.cumulative, col = colorset, legend.loc = legend.loc, ...)
	for (i in 1:NCOL(Return.cumulative)) {
		text(x=NROW(Return.cumulative),
		y=coredata(Return.cumulative)[NROW(Return.cumulative),i],
		sprintf("%1.0f%%",round(coredata(Return.cumulative)[NROW(Return.cumulative),i],2)*100),
		adj = c(0, 0.5),lwd=0.5,col=colorset[i])
	}
}

#this function shows bar plot side-by-side comparisons for rolling annualized
#returns
#please proceed with caution as function is not robust
#and does not perform adequate error checking
chart.SideBar <- function (w,  auto.grid = TRUE, xaxis = TRUE, yaxis = TRUE, yaxis.right = FALSE, 
    type = "l", lty = 1, lwd = 2, main = NULL, ylab = "Annualized Returns", xlab = NULL, 
    xlim = NULL, ylim = NULL, element.color = "darkgray", event.lines = NULL, 
    event.labels = NULL, period.areas = NULL, event.color = "darkgray", 
    period.color = "aliceblue", colorset = (1:12), pch = (1:12), 
    legend.loc = NULL, cex.axis = 0.8, cex.legend = 0.8, 
    cex.lab = 1, cex.labels = 0.8, cex.main = 1, major.ticks = "auto", 
    minor.ticks = TRUE, grid.color = "lightgray", grid.lty = "dotted", 
    xaxis.labels = NULL, ...) 
{
        barplot(w, beside=TRUE, col = colorset[1:NROW(w)], 
            xlab = xlab, ylab = ylab, axes = FALSE,
            ylim = c(min(0,min(w)),max(w)+0.05),...)

    if (auto.grid) {
        abline(v=0, col = element.color, lty = grid.lty)
        grid(NA, NULL, col = grid.color)
    }
    abline(h = 0, col = grid.color)

	axis(2, cex.axis = cex.axis, col = element.color)
	title(ylab = ylab, cex = cex.lab)

    if (!is.null(legend.loc)) {
        legend(legend.loc, inset = 0.02, text.col = colorset, 
            col = colorset, cex = cex.legend, border.col = grid.color, 
            lty = lty, lwd = 2, bg = "white", legend = rownames(w))
    }

	box(col = element.color)
}

charts.PerformanceSummaryX <-
function (R, Rf = 0, main = NULL, submain=NULL, geometric=TRUE, methods = "none", width = 0, event.labels = NULL, ylog = FALSE, wealth.index = FALSE, gap = 12, begin=c("first","axis"), legend.loc="bottomright", p=0.95, maxdraw = TRUE,...)
{ # @author Peter Carl

    # DESCRIPTION:
    # A wrapper to create a wealth index chart, bars for monthly peRformance,
    # and underwater chart for drawdown.

    # Inputs:
    # R: a matrix, data frame, or timeSeries, usually a set of monthly returns.
    #   The first column is assumed to be the returns of interest, the next
    #   columns are assumed to be relevant benchmarks for comparison.
    # Rf: this is the risk free rate.  Remember to set this to the same
    #   periodicity as the data being passed in.
    # method: Used to select the risk parameter to use in the chart.BarVaR.  May
    #   be any of:
    #     modVaR - uses CF modified VaR
    #     VaR - uses traditional Value at Risk
    #     StdDev - monthly standard deviation of trailing 12 month returns
    #

    # Outputs:
    # A stack of three related timeseries line charts

    # FUNCTION:
    begin = begin[1]
    x = checkData(R)
    colnames = colnames(x)
    ncols = ncol(x)

# This repeats a bit of code from chart.CumReturns, but it's intended
# to align the start dates of all three charts.  Basically, it assumes
# that the first column in the list is the column of interest, and 
# starts everything from that start date

    length.column.one = length(x[,1])
# find the row number of the last NA in the first column
    start.row = 1
    start.index = 0
    while(is.na(x[start.row,1])){
        start.row = start.row + 1
    }
    x = x[start.row:length.column.one,]

    if(ncols > 1)
        legend.loc = legend.loc
    else
        legend.loc = NULL

    if(is.null(main))
        main = paste(colnames[1],"Performance", sep=" ")

    if(ylog)
        wealth.index = TRUE

    op <- par(no.readonly=TRUE)

    # First, we lay out the graphic as a three row, one column format
#    plot.new()
    layout(matrix(c(1,2,3)),height=c(2,1,1.3),width=1)
    # to see the resulting layout, use layout.show(3)

    # mar: a numerical vector of the form c(bottom, left, top, right) which
    # gives the number of lines of margin to be specified on the four sides
    # of the plot. The default is c(5, 4, 4, 2) + 0.1

    # The first row is the cumulative returns line plot
	par(oma=c(2,2,4,2))	
    par(mar=c(1,6,8,4))
    chart.CumReturnsX(x, main = "", xaxis = FALSE, legend.loc = legend.loc, cex.legend = 1, event.labels = event.labels, ylog = ylog, wealth.index = wealth.index, begin = begin, geometric = geometric, ylab="Cumulative Return",...)

#	title(main=main, sub=submain, cex.main=2, cex.sub=1.5, adj=0, outer =FALSE)
mtext(text=main, line = -2, outer = TRUE, adj = 0.1, cex=2)
mtext(text=submain, line = -4, outer = TRUE, adj = 0.075, cex=1.5)

    # The second row is the monthly returns bar plot
#    par(mar=c(1,4,0,2))

    freq = periodicity(x)

    switch(freq$scale,
	seconds = { date.label = "Second"},
	minute = { date.label = "Minute"},
	hourly = {date.label = "Hourly"},
	daily = {date.label = "Daily"},
	weekly = {date.label = "Weekly"},
	monthly = {date.label = "Monthly"},
	quarterly = {date.label = "Quarterly"},
	yearly = {date.label = "Annual"}
    )

#    chart.BarVaR(x, main = "", xaxis = FALSE, width = width, ylab = paste(date.label,"Return"), methods = methods, event.labels = NULL, ylog=FALSE, gap = gap, p=p, ...)

    # The third row is the underwater plot
    par(mar=c(3,6,0,4))
    chart.Drawdown(x, geometric = geometric, main = "", xlab=NA, ylab = "Drawdown", event.labels = NULL, ylog=FALSE, ...)
	if (maxdraw) {
		abline(h=-0.1,col="tomato3",lwd=3,lty="dashed")
		text(x=2,y=-0.1,"maximum acceptable drawdown",adj = c(0, 0.5))
	}

#     If we wanted to add a fourth row with the table of monthly returns
#    par(mar=c(0,0,0,0))
#    textplot(table.Returns(as.matrix(R)),cex=.7,cmar=1.5,rmar=0.5,halign="center", valign="center")

par(mar=c(6,6,0,4))

returnTable <- returnTable <- table.TrailingPeriods(x,
	periods=c(12,24,36,NROW(x)),
	FUNCS="Return.annualized")
rownames(returnTable) <- c(paste(c(1:3)," Year",sep=""),"Since Inception")[1:NROW(returnTable)]

chart.SideBar(t(as.matrix(returnTable)),...)

par(op)

}

#now let's use the amended report to look at performance
require(quantmod)
require(PerformanceAnalytics)

clientPerf <- read.csv("clientperf.csv",stringsAsFactors=FALSE)
clientPerf[,2:NCOL(clientPerf)] <- lapply(clientPerf[,2:NCOL(clientPerf)],as.numeric)
clientPerf <- as.xts(clientPerf[,2:NCOL(clientPerf)]/100,
	order.by = as.Date(clientPerf[,1],format="%m-%d-%y"))
colnames(clientPerf) <- c("Client","BarclaysAgg","SP500")

jpeg(filename="performance summary.jpg",quality=100,width=6, height = 7,  units="in",res=96)
charts.PerformanceSummary(clientPerf)
dev.off()

jpeg(filename="performance one-pager.jpg",quality=100,width=6, height = 7,  units="in",res=96)
charts.PerformanceSummaryX(clientPerf,main="Client Performance",
	submain=paste("Since Inception - ",format(seq(index(clientPerf)[1], length=2, by="-1 months")[2],"%B %Y"),sep=""),legend.loc="bottomright",maxdraw=FALSE,
	colorset=c("cadetblue4","darkgray","bisque3"),lwd=c(3,2,2))
dev.off()
```