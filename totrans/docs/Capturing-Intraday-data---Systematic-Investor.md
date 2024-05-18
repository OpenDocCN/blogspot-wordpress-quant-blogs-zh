<!--yml
category: 未分类
date: 2024-05-18 14:30:39
-->

# Capturing Intraday data | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2014/03/11/capturing-intraday-data/#0001-01-01](https://systematicinvestor.wordpress.com/2014/03/11/capturing-intraday-data/#0001-01-01)

I want to follow up the [Intraday data](https://systematicinvestor.wordpress.com/2014/03/10/intraday-data/) post with an example of how you can capture Intraday data without too much effort by recording 1 minute snapshots of the market.

I will take market snapshots from Yahoo Finance using following function that downloads delayed market quotes with date and time stamps:

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

Next we can run the getQuote.yahoo.today function from 9:30 to 16:00 every minute and record market snap shoots. Please note that you will have to make some judgement calls in terms of how you want to deal with highs and lows.

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

For example I was able to saved following quotes for AAPL:

```
Symbol   Time      Date    Open    High      Low   Close  Volume
  AAPL 2:57pm 3/10/2014 528.360 533.330 528.3391 531.340 5048146
  AAPL 2:58pm 3/10/2014 531.340 531.570 531.3400 531.570    7650
  AAPL 2:59pm 3/10/2014 531.570 531.570 531.5170 531.517    2223
  AAPL 3:00pm 3/10/2014 531.517 531.517 531.4500 531.450    5283
  AAPL 3:01pm 3/10/2014 531.450 531.450 531.2900 531.290    4413
  AAPL 3:02pm 3/10/2014 531.290 531.490 531.2900 531.490    2440

```

Unfortunately, there is no way to go back in history, unless you buy historical intraday data. But if you want to start recording market moves yourself, following code should get you started.