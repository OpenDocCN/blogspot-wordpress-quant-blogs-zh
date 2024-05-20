<!--yml
category: 未分类
date: 2024-05-12 18:16:09
-->

# Another Short-Term Trend Indicator- DSR (Distribution Skew versus Range) | CSSA

> 来源：[https://cssanalytics.wordpress.com/2010/11/01/another-short-term-trend-indicator-dsr-distribution-skew-versus-range/#0001-01-01](https://cssanalytics.wordpress.com/2010/11/01/another-short-term-trend-indicator-dsr-distribution-skew-versus-range/#0001-01-01)

Note: I will be in Chicago this week presenting at the **NAAIM** conference on trading system evaluation along with two of my colleagues. [http://naaim.org/](http://naaim.org/) I have scheduled meetings booked throughout the week, but if you would like to meet up to discuss our institutional services one of my colleagues should be available. You can send me an email at: [david@cssanalytics.com](mailto:david@cssanalytics.com) In light of my current trip posting will be light. Some of the interesting research done in preparation for NAAIM will be provided on our site when I return.

*-also* be sure to check out **Quanting Dutchman** who has recently done some good work/research on trading systems and has also been providing Amibroker code for this specific type of H,L,C array: [http://quantingdutchman.wordpress.com/](http://quantingdutchman.wordpress.com/)

**DSR**—-CAGR on SPY over 2400 bars: **14%**

This is a trend distribution indicator that considers the skew of prices at higher moments versus the skew of prices at lower moments in relation to the price range. Effectively, a relatively high differential between the two in relation to the range  suggests that prices have more upside than downside. So far this indicator shows a great deal of promise for a short-term trend indicator and there are many possible ways to apply it. I will leave that part to many of my saavy readers and fellow bloggers. The indicator calculation is a bit tricky:

DSR *differentia*l=  average(  65th percentile (H,L,C, 20-days), 80th percentile  (H,L,C, 20-days)) –  average(  35th percentile (H,L,C, 20-days), 20th percentile  (H,L,C, 20-days))

DSR *raw*=  DSR *differential*/(max(H,L,C, 20-days)-min(H,L,C, 20-days))

**DSR**= 252-day percentrank of ( 10-day sma of DSR *raw)*