<!--yml
category: 未分类
date: 2024-05-12 19:04:34
-->

# Quantitative Trading: A method for optimizing parameters

> 来源：[http://epchan.blogspot.com/2010/01/method-for-optimizing-parameters.html#0001-01-01](http://epchan.blogspot.com/2010/01/method-for-optimizing-parameters.html#0001-01-01)

Most trading systems have a number of parameters embedded, parameters such as the lookback period, the entry and exit thresholds, and so on. Readers of my blog (for e.g.,

[here](http://epchan.blogspot.com/2008/05/parameterless-trading-models.html)

and

[here](http://epchan.blogspot.com/2008/08/more-on-parameterless-trading-model.html)

) and my

[book](http://www.amazon.com/dp/0470284889?tag=quantitativet-20&camp=14573&creative=327641&linkCode=as1&creativeASIN=0470284889&adid=1ZQ6268JYSSZDWNC9976&)

would know my opinion on parameter optimization: I am no big fan of it. This is because I believe financial time series is too non-stationary to allow one to say what was optimal in the backtest is necessarily optimal in the future. Most traders I know would rather trade a strategy that is insensitive to small changes in parameters, or alternatively, a "parameterless" strategy that is effectively an average of models with different parameters.

That being said, if you can only trade one model with one specific set of parameters, it is rational to ask how one can pick the best (optimal) set of parameters. Many trading models have a good number of parameters, and it is quite onerous to find the optimal values of all these parameters simultaneously. Recently, Ron Schoenberg published an

[article](http://www.futuresmag.com/Issues/2010/February-2010/Pages/Using-DOE-method-in-trading.aspx)

in the Futures Magazine that details a way to accomplish this with just a tiny amount of computer power.

The key technique that Ron uses is cubic polynomial fit of the P&L surface as a function of the parameters. Ron uses the VIX RSI strategy in Larry Connors' book "

[Short Term Trading Strategies That Work](http://www.amazon.com/dp/0981923909?tag=quantitativet-20&camp=14573&creative=327641&linkCode=as1&creativeASIN=0981923909&adid=1BPFA03ZZFNQ82NW23QT&)

" as an example. This strategy has 5 parameters to be optimized, but Ron only needs to compute the P&L for 62 different sets of parameters, and the whole procedure only takes 58 seconds.

Although Ron has confirmed that most of the parameters that Connors picked are close to optimal, he did find a few surprises: namely, that RSI of period 3 or 4 is significantly more profitable than the 2 that Connors used, at least in the backtest period.

Now, for a true test of this optimization, it would be helpful if Ron performed this optimization withholding some out-of-sample data, and see if these parameters are still optimal in that withheld data set. Since he didn't do that, we need to wait for another year to find out ourselves!