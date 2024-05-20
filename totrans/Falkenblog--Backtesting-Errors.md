<!--yml
category: 未分类
date: 2024-05-12 22:29:15
-->

# Falkenblog: Backtesting Errors

> 来源：[http://falkenblog.blogspot.com/2009/01/backtesting-errors.html#0001-01-01](http://falkenblog.blogspot.com/2009/01/backtesting-errors.html#0001-01-01)

The most annoying part of backtesting is creating a database, which is problematic because most data is meant to show a one-off take of current information, as opposed to cross-sectional data as of January 14, 1998\. It's free and easy to see all about, say, IBM's market and financial statement data. But what good is that information if not put into context, and what is the context, other than a historical sense for the relative distributions and correlations, of the past?

Pulling together such data usually involves integrating data from different sources, splicing them together, and making sure you have 'dead' companies. Invariably a data provider insists they have 'all' the data, because for them, current companies are all they can conceive of. So you have to be specific, and ask instead if they have 'dead' companies, such as Enron, WorldCom-MCI, and Bear Stearns. Then there are issues about splits, dividends, that can, if not accounted for, generate illusory patterns.

Anyway, I discovered something I thought was really interesting, but then found it was merely an error. See if you can spot the error. I have a database with financial statement information available at the end of every month. With that record or observation, I have the month-ahead returns, and also information on the trading volume and market cap as of the end of the month.

I looked at earnings day returns, the returns from the day prior to the earnings release date, and the close of prices the day after the earnings release date. To do this, I had to take the earnings report date information, and then take those date-firmID pairs to a database of daily return data. I noted their daily (annualized) volatility is about 150% higher than average daily returns in this period, which makes total sense. Just for fun, I looked at all companies with a market cap greater than $1B, and saw that the

average

daily return on this date was about 0.2% or so, highly significant. On average the return was significantly positive, but no one noticed because for any one observation there is a lot of noise, and its not so large as to be totally obvious. I looked for companies with greater than $500MM market cap, same result, and was highly consistent over time.

What is the error?

Well, my size filter used market cap data from the

end of the month

, to look back at the earnings date returns

from that same month

. By looking only at companies with greater than $1B or $500MM in market cap at the end of the month, it would include enough of those who migrated upward, and exclude enough of those that migrated downward, to generate the 0.2% return, which was entirely due to this bias. That is, there are enough companies moving from $975MM to $1001MM on earnings that get in, and enough going from $1001MM to $975 that are censored, to generate an illusory sample statistic.

I didn't think a $1B cut-off was material, especially because

usually

this database is used to look for patterns in month-ahead returns where the bias does not exist, so it didn't occur to me. But in fact there was a material selection bias in the market cap cut-off. These things are subtle sometimes.