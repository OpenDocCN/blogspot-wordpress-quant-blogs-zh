<!--yml
category: 未分类
date: 2024-05-12 19:03:18
-->

# Quantitative Trading: Shorting the VIX calendar spread

> 来源：[http://epchan.blogspot.com/2011/01/shorting-vix-calendar-spread.html#0001-01-01](http://epchan.blogspot.com/2011/01/shorting-vix-calendar-spread.html#0001-01-01)

Lately there were a few interesting discussions in the 

blogosphere 

on the profitability of shorting the VXX-VXZ spread. (See

[Quantum Blog](http://matlab-trading.blogspot.com/2010/12/vix-buy-hold-strategy.html)

and

[The Speculator's Ball](http://speculators-ball.blogspot.com/2010/12/is-vxx-due-for-bounce.html)

.) For background, VXX is an ETN that tracks the first and second month of the VIX future, which in turn tracks the VIX volatility index, which in turn tracks the volatility of SPX. VXZ is the ETN that tracks the 4th - 7th months of the VIX future. During the period 2009-2010, there were 2 different reasons why shorting this "calendar spread" was profitable:

1) The VIX futures were/are in contango: i.e. the back months' futures are more expensive than the front months'.

2) The volatility of SPX was decreasing with time.

However, some traders seem to think that either one of these conditions is enough to ensure the profitability of shorting a calendar spread.  It is not. (Otherwise, life as a futures trader would be too easy!)

To see this, let's resort to a simplistic linear approximation to a model of futures prices. From

[John Hull](http://www.amazon.com/gp/product/0132164949?ie=UTF8&tag=quantitativet-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0132164949)

's book on derivatives, section 3.12, the price of  a future which matures at time T is

F(t, T)=E(S

T

)exp(c(T-t)),

where E(S

T

) is the expected value of the spot price at maturity, c is a constant, and t is the current time. If the futures are in contango, then c > 0.

If we assume that abs(c) is small, and T-t is also small (i.e. not too far from maturity), and that the expected value of the spot price changes slowly, we can linearize this formula as

F=(a+b(T-t))*(1+c(T-t))

If the market expects the future spot price to increase, then b > 0.

After a few simple algebraic steps, you can verify that the calendar spread's price is proportional to

F(t, T

1

)-F(t, T

2

) ~ bct

where T

1

< T

2

(i.e. F(t, T

1

) is the front month's price, and F(t, T

2

) the back month's).

This is a satisfyingly illustrative result. It says that shorting this calendar spread will be profitable if

A) futures are in contango

*and*

the expected spot price in the future is decreasing; or else

B) futures are in backwardation

*and*

the expected spot price in the future is increasing.

So what is the situation today? Will it still be profitable to short this spread? As our fellow bloggers have pointed out, VIX futures are still in contango, but the market is expecting volatility to increase in the future over the last month or so. So this may no longer be a profitable trade anymore.