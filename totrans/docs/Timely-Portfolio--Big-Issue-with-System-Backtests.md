<!--yml
category: 未分类
date: 2024-05-18 15:03:25
-->

# Timely Portfolio: Big Issue with System Backtests

> 来源：[http://timelyportfolio.blogspot.com/2012/09/big-issue-with-system-backtests.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/09/big-issue-with-system-backtests.html#0001-01-01)

Almost always, when I see a system backtested, the backtest assumes a static portfolio with no contributions or withdrawals.  This assumption only covers an extremely limited subset of my clients.  Cash flows in and out of a portfolio or system can have a much larger impact on ending net worth than the geometrically linked performance of a system or money manager.  Most of the systems I have shown for demonstration purposes on this blog have suffered from this unrealistic assumption.  I thought I should show how contributions similar to those in a 401k can affect a simple moving average system.

In a roaring bull market, any momentum system will underperform so significantly that potential abandonment of the system due to lack of confidence is highly likely.  As shown below, there was very little discussion of moving average strategies 1990-2000 due to the simple fact that buy/hold absolutely clobbered them.  While normal adjustments like return/risk and a log scale can soften the impact on the screen, the psychological impact to a client can be very damaging as the focus moves entirely to $ value of the portfolio.  Below is a comparison of buy and hold versus a 200 day moving average system with no additions or withdrawals.  As discussed, 1990-2000 was not kind to the moving average.

However, if we add a simple framework similar to a 401k investor starting with $100,000 and adding $10,000 per year ($2,500 per quarter), the results differ significantly.

I intentionally played a little trick by changing the y axis to a log scale.  Clients don’t think in log scale when evaluating performance.  They simply look at $ value of the portfolio.  If we look at the results without a log scale, underperformance by 2000 is visible, but it is nowhere near as great as shown in the first chart of the post, and outperformance after the 2008-2009 collapse is very healthy.  I actually think a client could accept this profile much more readily than that shown with a static portfolio.

Of course, this test was not perfect, and all sorts of assumptions and simulations can be added, but we can start to see how inflows and outflows can impact a portfolio whether it is buy/hold, discretionary, or systematic.

[R code from GIST ( do raw for copy/paste ):](https://gist.github.com/3669823)