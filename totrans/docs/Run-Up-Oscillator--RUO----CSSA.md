<!--yml
category: 未分类
date: 2024-05-12 18:10:34
-->

# Run-Up Oscillator (RUO) | CSSA

> 来源：[https://cssanalytics.wordpress.com/2011/04/29/run-up-oscillator-ruo/#0001-01-01](https://cssanalytics.wordpress.com/2011/04/29/run-up-oscillator-ruo/#0001-01-01)

In the previous post we discussed the concept of a drawdown oscillator- which measures the normalized drawdown from a long or short trade as defined by the Donchian Channel. A related and highly complimentary oscillator would naturally measure the run-up between drawdowns. This would allow us to create a more dynamic/holistic strategy, as there is typically a relationship between the magnitude of a run-up and the subsequent drawdown. The run-up oscillator would be constructed for both long and short positions using the same trend metric– the Donchian Channel. The oscillator is a little tricky to calculate as it has several features:

1) **Trigger**: this uses the Drawdown Oscillator (DRO) to create a minimum definition for a drawdown. In this case, I would stipulate that the minimum level be greater than .25 or basically above the lowest quartile of drawdowns.

2) **Point of Measure:** this would be the first 50-day high (or low for shorts) using default parameters following the DRO hitting a level above the lowest quartile ie >.25.

3) **Run-up violation:** this would be the first drawdown of a minimum qualifying level using the DRO. In this case, a violation would be a DRO >.25 by default.

**RUO Calculation:**  this is the ATRs gained from the point of measure (using say a 10 or 20-day ATR by default) using the default trigger without a run-up violation. The current number of ATRs gained is ranked in percentile terms relative to  the 50 previous run-ups.

Applications:

One can use this measure to reduce exposure to trend trades, or even utilize as a means to time counter-trend trades. Another more complex application would be to compare the run-up oscillator levels to predicted drawdown levels as represented by the DRO. In other words, if the market goes up a certain amount in percentile terms from the last correction, what is the expected drawdown in percentile terms that follows. A lot of possibilities for the serious researcher.