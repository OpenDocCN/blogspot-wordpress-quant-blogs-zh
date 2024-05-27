<!--yml

类别：未分类

日期：2024 年 05 月 18 日 14:30:39

-->

# 捕获日内数据 | 系统投资者

> 来源：[`systematicinvestor.wordpress.com/2014/03/11/capturing-intraday-data/#0001-01-01`](https://systematicinvestor.wordpress.com/2014/03/11/capturing-intraday-data/#0001-01-01)

我想在[日内数据](https://systematicinvestor.wordpress.com/2014/03/10/intraday-data/)一文后跟进，示例说明如何通过记录市场的 1 分钟快照来捕获日内数据，而不需要太多的努力。

我将使用以下函数从 Yahoo Finance 获取市场快照，该函数下载带有日期和时间戳的延迟市场报价：

```
###############################################################################
# getSymbols interface to Yahoo today's delayed qoutes
# based on getQuote.yahoo from quantmod package
###############################################################################            
getQuote.yahoo.today <- function(Symbols) {
    require('data.table')
    what = yahooQF(names = spl('Symbol,Last Trade Time,Last Trade Date,Open,Days High,Days Low,Last Trade (Price Only),Volume'))
    names = spl('Symbol,Time,Date,Open,High,Low,Close,Volume')

    all.symbols = lapply(seq(1, len(Symbols), 100), function(x) na.omit(Symbols[x:(x + 99)]))
    out = c()

    for(i in 1:len(all.symbols)) {
        # download
        url = paste('http://download.finance.yahoo.com/d/quotes.csv?s=',
            join( trim(all.symbols[[i]]), ','),
            '&f=', what[[1]], sep = '')

        txt = join(readLines(url),'\n') 
        data = fread(paste0(txt,'\n'), stringsAsFactors=F, sep=',')
            setnames(data,names)
            setkey(data,'Symbol')      	
      	out = rbind(out, data)
    }
    out
} 

```

接下来，我们可以每分钟从 9:30 到 16:00 运行 getQuote.yahoo.today 函数，并记录市场快照。请注意，在处理高点和低点时，您需要做出一些判断。

```
Symbols = spl('IBM,AAPL')

prev = c()
while(T) {
    out = getQuote.yahoo.today(Symbols)

    if (is.null(prev)) 
        for(i in 1:nrow(out)) {
	    cat(names(out), '\n', sep=',', file=paste0(out$Symbol[i],'.csv'), append=F)
	    cat(unlist(out[i]), '\n', sep=',', file=paste0(out$Symbol[i],'.csv'), append=T)					
	}
    else
        for(i in 1:nrow(out)) {
	    s0 = prev[Symbol==out$Symbol[i]]
	    s1 = out[i]
	    s1$Volume = s1$Volume - s0$Volume
	    s1$Open = s0$Close
	    s1$High = iif(s1$High > s0$High, s1$High, max(s1$Close, s1$Open))
	    s1$Low  = iif(s1$Low  < s0$Low , s1$Low , min(s1$Close, s1$Open))
	    cat(unlist(s1), '\n', sep=',', file=paste0(out$Symbol[i],'.csv'), append=T)					
        }

    # copy
    prev = out

    # sleep 1 minute   
    Sys.sleep(60)	
} 

```

例如，我能够为 AAPL 保存以下报价：

```
Symbol   Time      Date    Open    High      Low   Close  Volume
  AAPL 2:57pm 3/10/2014 528.360 533.330 528.3391 531.340 5048146
  AAPL 2:58pm 3/10/2014 531.340 531.570 531.3400 531.570    7650
  AAPL 2:59pm 3/10/2014 531.570 531.570 531.5170 531.517    2223
  AAPL 3:00pm 3/10/2014 531.517 531.517 531.4500 531.450    5283
  AAPL 3:01pm 3/10/2014 531.450 531.450 531.2900 531.290    4413
  AAPL 3:02pm 3/10/2014 531.290 531.490 531.2900 531.490    2440

```

不幸的是，除非购买历史日内数据，否则无法回溯历史。但如果你想开始记录市场变动，下面的代码应该可以帮助你入门。
