<!--yml
category: 未分类
date: 2024-05-12 18:54:36
-->

# Quantitative Trading: Why does our Tail Reaper program work in times of market turmoil?

> 来源：[http://epchan.blogspot.com/2020/03/why-does-our-tail-reaper-program-work.html#0001-01-01](http://epchan.blogspot.com/2020/03/why-does-our-tail-reaper-program-work.html#0001-01-01)

I generally don't like to write about our

[investment programs](http://www.qtscm.com/accounts)

here, since the good folks at the National Futures Association would then have to review my blog posts during their regular audits/examinations of our CPO/CTA. But given the extraordinary market condition we are experiencing, our kind cap intro broker urged me to do so. Hopefully there is enough financial insights here to benefit those who do not wish to invest with us.

As the name of our Tail Reaper program implies, it is designed to benefit from tail events. It did so (+20.07%) during August-December, 2015’s Chinese stock market crash (even though it trades only the E-mini S&P 500 index futures), it did so (+18.38%) during February-March, 2018’s “volmageddon”, and now it did it again (+12.98%) during February, 2020’s Covid-19 crisis. (As of this writing, March is up over 21% gross.) There are many names to this strategy: some call it “crisis alpha”, others call it “convex”, “long gamma” or “long vega” (even though no options are involved), “long volatility”, “tail hedge”, or just plain old “trend-following”. Whatever the name or description, it usually enjoys outsize return when there is real panic. (But of course, PAST PERFORMANCE IS NOT NECESSARILY INDICATIVE OF FUTURE RESULTS.) Furthermore, our strategy did so without holding any overnight positions.

Why is a trend-following strategy profitable in a crisis? A simple example will suffice. If a short trade is triggered when the return (from some chosen benchmark) exceeds -1%, then the trade will be very profitable if the market ends up dropping -4%. Vice versa for a long trade. (As recent market actions have demonstrated, prices exhibit both left and right tail movements in a crisis.) The trick, of course, is to find the right benchmark for the entry, and to find the right exit condition.

Naturally, insurance against market crash isn’t completely free. Our goal is to prevent the insurance cost, which is essentially the loss that the strategy suffers during a stretch of bull market, from being too high. After all, if insurance were all we want, we could have just bought put options on the market index, and watched it lost premium every month in “good” times. To prevent the loss of insurance premium requires a dose of market timing, assisted by our machine learning program that utilizes many, many factors to predict whether the market will suffer extreme movements in the next day. In most years, the cost (loss) is negligible despite the long bull market, except in 2019 when we lost 8.13%. That year, which seems a long time ago, the SPY was up 30.9%. (It was in the August of that year that we added the machine learning risk management layer.) But most investors have a substantial long exposure. A proper asset allocation to both Tail Reaper and to a long-only portfolio will smooth out the annual returns and hopefully eliminate any losing year. (Again, PAST PERFORMANCE IS NOT NECESSARILY INDICATIVE OF FUTURE RESULTS.)

But why should we worry about a losing year? Isnt’ total return all investors should care about? Recently, Mark Spitznagel (who co-founded Empirica Capital with Nassim Nicholas Taleb) wrote a series of interesting

[articles](https://www.universa.net/riskmitigation.html)

. It argued that even if a tail hedge strategy like ours returns an arithmetic average return of 0%, as long as it provides outsize positive returns during a market crisis, it will be able to significantly improves the compound growth rate of a portfolio that includes both an index fund and the tail hedge strategy. I have previously written a somewhat technical

[blog post](http://epchan.blogspot.com/2017/05/paradox-resolved-why-risk-decreases.html)

on this mathematical curiosity. The gist of the argument is that the compound growth rate of a portfolio is m-s^2/2, where m is the arithmetic mean return and s is the standard deviation of returns. Hedging tail risk is not just for the psychological comfort of having no losing years - it is mathematically proven to improve long-term compound growth rate overall.

PAST PERFORMANCE IS NOT NECESSARILY INDICATIVE OF FUTURE RESULTS.

For further reading on convex strategies, please see the papers by Paul Jusselin et al “Understanding the Momentum Risk Premium: An In-Depth Journey Through Trend-Following Strategies” and Dao et al “Tail protection for long investors: Trend convexity at work” (Hat tip to Corey Hoffstein for leading me to them!)