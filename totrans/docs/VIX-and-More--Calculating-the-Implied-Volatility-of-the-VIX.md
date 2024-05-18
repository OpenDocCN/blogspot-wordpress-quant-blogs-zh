<!--yml
category: 未分类
date: 2024-05-18 17:53:09
-->

# VIX and More: Calculating the Implied Volatility of the VIX

> 来源：[http://vixandmore.blogspot.com/2009/04/calculating-implied-volatility-of-vix.html#0001-01-01](http://vixandmore.blogspot.com/2009/04/calculating-implied-volatility-of-vix.html#0001-01-01)

Earlier today, a reader had an excellent observation and question regarding the [implied volatility](http://vixandmore.blogspot.com/search/label/implied%20volatility) of the VIX:

> *“I noticed that the IV for ATM July options is 50 while the VIX itself is 42 right now. That seems crazy to me since the IV for the VIX is a second derivative and should be much more than the VIX itself…”*

The problem with most data sources is that they assume the cash/spot VIX is the underlying for [VIX options](http://vixandmore.blogspot.com/search/label/VIX%20options), instead of using [VIX futures](http://vixandmore.blogspot.com/search/label/VIX%20futures), which more accurately approximate the underlying for VIX options (which is technically a [variance swap](http://en.wikipedia.org/wiki/Variance_swap).)

I cannot vouch for every data provider, but I believe most of the highly regarded options sites on the web use the cash/spot VIX to calculate VIX implied volatility, so the resulting calculations are distorted by the difference between the cash/spot VIX and the VIX futures.

Several options data sources have a proprietary mean implied volatility calculations that they publish for optionable securities. Perhaps the best known of these is the “IV Index mean” from iVolatility.com. After today’s close, the [iVolatility VIX IV index mean](http://www.ivolatility.com/options.j?ticker=vix&R=0&x=0&y=0) was 61.38\. The International Securities Exchange has a similar calculation that uses the same name. Today the [ISE’s VIX IV index mean](http://www.ise.com/WebForm/md_livevol.aspx?categoryId=124&header2=true&menu1=true) closed at 64.98.

Thinkorswim calculates an IV for each month. For April, they have the VIX IV at 85.71\. Doing a little interpolation on the optionsXpress site, I get a VIX IV for April ATM options of 77.12.

Without knowing the details behind the models that generate these VIX IV calculations, I cannot vouch for the integrity of any of the VIX IV outputs. I would love to find a source that calculates the implied volatility of the VIX using VIX futures as the underlying. My guess is that none of above four numbers takes this approach. If anyone is aware of a source that publishes VIX IV calculations based on VIX futures, I would certainly be interested in hearing more about it. Until then, my working assumption would be that all the VIX IV data you get from your data provider is invalid and based on the cash/spot VIX.