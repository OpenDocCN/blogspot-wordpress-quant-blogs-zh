<!--yml
category: 未分类
date: 2024-05-12 18:51:47
-->

# Normalizing Bollinger Bands Using DV Bands (part 1) | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/08/05/normalizing-bollinger-bands-using-dv-bands-part-1/#0001-01-01](https://cssanalytics.wordpress.com/2009/08/05/normalizing-bollinger-bands-using-dv-bands-part-1/#0001-01-01)

*The link to Part 2 was missed by most people, you can find it here:* [https://cssanalytics.wordpress.com/2009/08/06/](https://cssanalytics.wordpress.com/2009/08/06/)part-2-improvi…-intraday-data/

The key impetus behind designing bollinger bands was to find a method that could accurately contain most price movements for a given security. The standard setting of 20 days as the average, and 2 standard deviations above and below, should theorectically contain 95% of prices if prices are normally distributed. In his book–“Bolliinger on Bollinger Bands,” John Bollinger states that in testing prices are actually contained within the bands 89% of the time using this default setting.

One of the key insights that goes into my work, is the normalization of indicators and even stock rankings using the empirical distribution. I decided to take a look at how this applies to bollinger bands–which is a very popular indicator for traders. I chose to test the SPY going back to 1995\. I compared bollinger bands to DV bands to determine whether the procedure added statistical value. DV Bands are simply bollinger bands that have been normalized by ranking the current z-score using the PERCENTRANK function with a lookback of 252 days. DV bands like bollinger bands are set at 20 and 2, with 20 being the 20-day average of prices and +/- 2 standard deviations representing the upper and lower bands.

First i ran a test of how many prices actually fell within the two bands using both methods:

|   | actual % of prices falling | historical |
|   |  between upper and lower bands | error |
| Bollinger Bands (20,2) | **91%** | **-4%** |
| DV Bands (20,2) | **95%** | **0%** |

As you can see, Bollinger Bands contain only 91% of historical prices, which is 4% less than would be expected if the values were normally distributed. In contrast DV Bands contain 95% of historical prices—exactly what we would expect, because these bands do not assume a normal distribution, and adapt to the empirical distribution of the stock as it evolves over time. But what about out of sample? What percentage of prices are contained within the bands, if today they were contained within the bands?  Here are the results:

|   | *next day  % of prices falling | forecast |
|   |  between upper and lower bands | error |
| Bollinger Bands (20,2) | **89%** | **-6%** |
| DV Bands (20,2) | **91%** | **-4%** |
|   |   |   |
| *if today the price is between the upper and lower band Out of sample, we also see an improvement in forecast error. Note that if you use even longer lookbacks periods (percentrank), such as 4 or 5 years, performance improves even more. There are ways to further improve this such as training the bands with different historical values of ADX, as well as historical bandwidth over the last 20-days. Presumably, band violations will be more frequent when the bands are tight and ADX is low but rising.Using ATR bands simultaneously would likely also add  additional information because they are not perfectly correlated with bollinger bands, as they contain intraday data. Now lets take at the raw impact of trading with these improvements: 

&#124;   &#124; *next day avg  return if **BELOW** the mean &#124;
&#124;   &#124; AND  between upper and lower bands &#124;
&#124; Bollinger Bands (20,2) &#124; **0.016%** &#124;
&#124; DV Bands (20,2) &#124; **0.0250%** &#124;
&#124;   &#124;   &#124;
&#124;   &#124; *next day  return if **ABOVE** the mean &#124;
&#124;   &#124; AND  between upper and lower bands &#124;
&#124; Bollinger Bands (20,2) &#124; **-0.004%** &#124;
&#124; DV  Bands (20,2) &#124; **-0.012%** &#124;

Average daily returns are over 50% higher when buying below the mean using DV Bands versus bollinger bands. Average daily returns are 200% lower above the mean using DV Bands versus bollinger bands. The impact for traders, is actually quite large. Results are fairly consistent across different band combinations.The evidence seems to clearly indicate that normalization improves the usefulness of bollinger bands. The applications extend beyond simple mean reversion strategies, and probably have the most impact for options traders. A new option formula could be derived using these results to more accurately represent the fair price. In the future (part 2), i will present more extensive results, and check for robustness across different asset classes. |   |