<!--yml
category: 未分类
date: 2024-05-18 04:45:04
-->

# Intelligent Trading: Conditioning Systems on Regime Variables

> 来源：[http://intelligenttradingtech.blogspot.com/2010/08/conditioning-systems-on-regime.html#0001-01-01](http://intelligenttradingtech.blogspot.com/2010/08/conditioning-systems-on-regime.html#0001-01-01)

Here is a brief and simple example of switching systems based upon regime type (sometimes called gating).

I've brought up the idea of conditioning systems based upon regimes many times in past posts. Some texts call this filtering, although I prefer to use the term conditional gating. The simple idea is to turn on a certain system during certain conditions and either: switching systems, or simply tracking the underlying series during alternate conditions. In this case the gating condition is regime, which in turn is, is High or Low Volatility as measured by the VIX.  Although I'm not divulging the details of the underlying system itself, I've seen enough discussions in public domain to feel that other traders have picked up on the ideas demonstrated here.

 Fig 1\. Terminal Wealth vs. VIX threshold

The animation below shows the system results during each step of the conditioning variable, the VIX. Notice the dramatic improvement at the value of 23\. Also, notice as mentioned in earlier posts how the optimal switching point of 23 is the most robust value, since even if the OOS results are to the left or right of the optimal switching point, they will be the best local values over a wide range of dependency. The astute observer might have noticed that this system is simply tracking buy&hold during low vix regimes, while switching on system V, during the high regimes. It is evident that the terminal wealth simply tracks buy & hold after a certain value of VIX, since it is always locked on to tracking mode under a certain threshold.

The system is only shown in sample, however, I've found it to be pretty successful OOS as well.

<param name="movie" value="http://www.youtube.com/v/ZcSyV0mMcA0&amp;hl=en&amp;fs=1"><param name="allowFullScreen" value="true"><param name="allowscriptaccess" value="always"><embed src="http://www.youtube.com/v/ZcSyV0mMcA0&amp;hl=en&amp;fs=1" type="application/x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true">

Video 1\. Stepping the Equity Curve system through linear VIX range.