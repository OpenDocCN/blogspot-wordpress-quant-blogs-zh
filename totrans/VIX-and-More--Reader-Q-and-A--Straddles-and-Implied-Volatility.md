<!--yml
category: 未分类
date: 2024-05-18 16:50:37
-->

# VIX and More: Reader Q and A: Straddles and Implied Volatility

> 来源：[http://vixandmore.blogspot.com/2011/04/reader-q-and-straddles-and-implied.html#0001-01-01](http://vixandmore.blogspot.com/2011/04/reader-q-and-straddles-and-implied.html#0001-01-01)

> *Right before the close last Wednesday I placed an ATM straddle that proved to be profitable and I closed it after the IV spike on Thursday. I shouldn't have come back for more, but I placed another ATM straddle Monday before the close and even with the huge drop in price on Tuesday the IV collapse only allowed me to break even. These were my first two super short term volatility trades and now I now that the free IV data on the CBOE's website is an end of day service... definitely wouldn't have placed that trade on Monday afternoon. Seeing now that I possibly should have been doing the opposite, shorting volatility, do you suggest any strategies that aren't outright short and don't require a big amount of margin to be put up? *
>  *Also, what service do you use to view real-time IV for ETFs and such?*

> *Adam C.*

Hi Adam,

As a newbie, you should make an important distinction between options trades that have unlimited risk and those that you should characterize as limited risk or defined risk. Shorting 10

[SLV](http://vixandmore.blogspot.com/search/label/SLV)

July 47 calls theoretically opens you up to unlimited risk because SLV can continue to go up and up. Should this happen, depending upon your cash cushion, eventually your broker will hit you with a margin call and you will be forced to cover at a significant loss.

Take the same basic trade and add a second leg as a hedge and your unlimited risk is now limited. Instead of a naked short, a bear call spread involving 10 short SLV July 47 calls plus 10 long SLV July 50 calls caps your loss at the distance between the two strikes. Here that is 50-47 or three points. Three points times 10 options (with a 100 multiplier) puts your maximum loss at $3000.

Make that trade right now and for 10 contracts you should receive a credit of about $1.20 for that spread, so that means your maximum profit is $1200 and maximum loss is $3000 - $1200 or $1800.

This is a directional bet. For a non-directional bet – meaning that you expect SLV to be at about 47.00 at the time of the July expiration, you should probably focus on

[condors](http://vixandmore.blogspot.com/search/label/condor)

and

[butterflies](http://vixandmore.blogspot.com/search/label/butterfly)

, which are essentially the limited risk version of

[strangles](http://vixandmore.blogspot.com/search/label/strangle)

and

[straddles](http://vixandmore.blogspot.com/search/label/straddle)

. Sometimes you will hear a trader refer to “buying the wings.” What that means is they are converting an unlimited risk strangle or straddle into a limited risk condor or butterfly by buying out-of-the-money legs to hedge their risk, just as was the case with the call spread example above. As a matter of fact, one way to think about an iron condor is that it is just a

[bear call spread](http://vixandmore.blogspot.com/search/label/bear%20call%20spread)

plus a

[bull put spread](http://vixandmore.blogspot.com/search/label/bull%20put%20spread)

. Early on I used a more generic label of

[vertical credit spread](http://vixandmore.blogspot.com/search/label/vertical%20credit%20spread)

on the blog for these strategies. You should be able to follow any of these links to get more information.

An even better way to get up to speed on these strategies is with some online resources. A good place to start is with the Options Industry Council (OIC), where they have an

[Options Strategy Index](http://www.optionseducation.org/strategy/strategy_index.jsp)

. Click on any strategy diagram for more information. Among the many great resources out there, I can highly recommend the

[CBOE’s Options Institute](http://www.cboe.com/LearnCenter/default.aspx)

, where you might want to start with their

[tutorials](http://www.cboe.com/LearnCenter/Tutorials.aspx)

. Keep in mind that the options brokers also do an excellent job of educating their customers on options strategies. Two that put a great deal of effort into education are optionsXpress (

[Education Center](http://www.optionsxpress.com/free_education/education_center.aspx)

) and thinkorswim (

[Swim Lessons](https://www.thinkorswim.com/tos/displayPage.tos?webpage=trainingProducts)

).

Also, the links below should provide some specific posts that will give you some food for thought regarding your recent SLV (?) trade and some alternative approaches.

In terms of real-time IV, I use

[Livevol Pro](http://www.livevol.com/livevol_pro.html)

, which provides the graphs that I use on the blog for

[implied volatility](http://vixandmore.blogspot.com/search/label/implied%20volatility)

and

[historical volatility](http://vixandmore.blogspot.com/search/label/historical%20volatility)

. Your favorite options brokers (thinkorswim, optionsXpress, TradeMONSTER, Options House, Trade King, etc.) should also have good real-time or nearly real-time IV data. If you don't have an account at a broker that specializes in options, I highly recommend you open up one with at least one of the brokers mentioned above so you can get your data and place your trades on the same platform.

Related posts:

***Disclosure(s):** Short SLV at time of writing; Livevol, CBOE, optionsXpress, TradeMONSTER, Options House and Trade King are advertisers on VIX and More*