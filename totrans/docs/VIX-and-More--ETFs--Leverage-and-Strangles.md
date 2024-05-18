<!--yml
category: 未分类
date: 2024-05-18 17:44:35
-->

# VIX and More: ETFs, Leverage and Strangles

> 来源：[http://vixandmore.blogspot.com/2009/06/etfs-leverage-and-strangles.html#0001-01-01](http://vixandmore.blogspot.com/2009/06/etfs-leverage-and-strangles.html#0001-01-01)

I was surprised by the volume of the feedback I received from last week’s [Using Options to Control Risk in Leveraged ETFs](http://vixandmore.blogspot.com/2009/05/using-options-to-control-risks-in.html). Clearly there is a great deal of interest in options and leveraged ETFs.

Among the emails I received were several questions about strategies associated with ETFs. For the record, my intent here is not to advocate a particular strategy, but merely to illuminate various strategic building blocks that I believe should be part of the trading arsenal of any options trader.

With that out of the way, let me spend a minute talking about [strangles](http://vixandmore.blogspot.com/search/label/strangle). I realize I have not talked about strangles as much as [straddles](http://vixandmore.blogspot.com/search/label/straddle) here, but I actually prefer to trade strangles instead of straddles when I am selling options. Whereas, the point of maximum profit for a straddle is a point that often resembles a [Sisyphean](http://en.wikipedia.org/wiki/Sisyphus) lottery, strangles have a maximum profit zone that is much wider and easier to manage.

In the chart immediately below, I have taken a snapshot of a short strangle on [IWM](http://vixandmore.blogspot.com/search/label/IWM), which is an ETF for the Russell 2000 small cap index. The short strangle is created by selling 10 June 50 puts and selling 10 June 55 calls. In this example, the puts have an [implied volatility](http://vixandmore.blogspot.com/search/label/implied%20volatility) of 37 and the calls have an implied volatility of 31\. Note that the maximum profit on this short strangle is $1210 and occurs if IWM closes anywhere from 50 to 55 at expiration. The full profit zone spans 7.92 points from 48.79 to 56.71.

![](img/2bccf38622cfe3f5dc5959338840baa3.png)

[TNA](http://vixandmore.blogspot.com/search/label/TNA) is a 3x ETF for the same Russell 2000 small cap index. Whereas IWM closed at 52.43, TNA closed at 30.66, a little more than 41% below its 1x sibling. Even at a significantly lower price, however, the firepower of the 3x ETF is immediately obvious when you look at the options. The chart below shows the result that is created by selling 10 June 28 puts and selling 10 June 33 calls. As in the IWM example, the strikes have a five point interval. The differences in the profit and loss graphic below are largely a result of the extreme differences in volatility. In this example, the puts have an implied volatility of 92 and the calls have an implied volatility of 87 – almost, but not quite, three times that of IWM. As result of the higher volatility, the maximum profit is $2800 (between 28 and 33), while the full profit zone is 10.60 points, from 25.20 to 35.80.

In brief, for an implied volatility that is about 2.6 times higher, TNA offers a maximum profit that is 2.3 times greater and profit zone that is 1.3 times larger.

These comparisons are admittedly less than perfect, given that the IWM and TNA trade at much different prices, but they certainly convey the essence of the idea that in a range-bound market, an options seller who is short options on 3x leveraged ETFs can rack up large gains (or losses) in a hurry. Of course, this same trade can be made much less risky by "buying the wings" and turning the strangle into an iron [condor](http://vixandmore.blogspot.com/search/label/condor).

For a related post, check out [The Options Opportunity Matrix](http://vixandmore.blogspot.com/2009/04/options-opportunity-matrix.html).

![](img/6e53d1c3bb6d75dfa2b677eb08fd020d.png)

*[graphics: optionsXpress]*