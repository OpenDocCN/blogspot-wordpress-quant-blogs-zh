<!--yml

category: 未分类

date: 2024-05-12 21:19:40

-->

# Falkenblog: Why Volatility Innovation Can't Save the Risk Premium

> 来源：[`falkenblog.blogspot.com/2010/10/why-volatility-innovation-cant-save.html#0001-01-01`](http://falkenblog.blogspot.com/2010/10/why-volatility-innovation-cant-save.html#0001-01-01)

I

[noted that a paper](http://falkenblog.blogspot.com/2010/10/never-trust-experts.html)

referenced the fact that an asset's correlation with volatility changes is a priced risk factor. Thus, instead of the CAPM, where you have

E(R

[i]

)=R

[i]

+E*Beta*(R

[m]

-R

[f]

)

You have

E(R

[i]

)=R

[f]

+E*Beta*(ShortVolatilityInnovation)

In the 'volatility innovation' story of risk, you are worried about not some market return proxy, but rather some volatility index. We all wish we had assets that appreciated when markets go crazy, like in 2001 or 2008, but we would have to pay a premium for that, which is why (supposedly) there's a market premium for it.

Research on option strategies tend to find that selling volatility does make more of a premium than buying volatility. There are large transaction costs to this direct strategy, especially historically, so it is not clear how economically meaningful this all is in terms of a realizable premium to selling volatility. See

[Sophie Ni (2008)](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1259703)

,

[Bonderanko (2003)](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=375784)

, or

[Shumway and Coval (2000)](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=189840)

, for data on the returns from selling volatility (all w/o good data on transaction costs). The VIX index is derived from 30 day implied volatilities on the SPX index. Since 1995 the average has been 21.5, whereas realized vol was 20.3\. Thus, it seems you could have made money 1 vol selling at-the-money volatility.

Note this is the 'selling Black Swans' strategy, or Victor Niederhoffer as opposed to Nassim Taleb. As we know from

[Niederhoffer's record](http://seekingalpha.com/article/49251-the-third-fall-of-victor-niederhoffer)

, this strategy can be dangerous, with fat tails wiping out years of returns, so it might not be a good strategy everything considered. I have backtested such strategies using historical option data and find that over time selling vol makes a decent profit. Just good luck telling your investors that after events like in 1987, 2001, or 2008, when you get crushed.

[One paper argues](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1340575)

that 'jump risk' underlies the premium to selling volatility, and that makes sense, in that, you simply can't sell volatility as easily as buy, because of the capital requirements, so, return per underlying might look different, but on capital required via the market, not so different.

The problem with volatility correlations saving the risk premium story is that it is highly correlated with the market. Here is a daily return scatterplot:

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjeQtoLQbgU7jCDCJ6fKPPT_g48YpiMMMaSS3_vJC7HWnXLDs_7Wqh-YrkGM458yp59oZH2wVFMZ1nhtE8AAulifX5OMxpMHwTK9pdL1Ax-ZAojGXzbRq90KnBqs9B2pR-zLo9c0A/s1600/dailyspy.jpg)

和一个每月的：

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgNWL0MalwP41ExsMVGtvF_lvyVQWAEZrKV-KFY0L_zXj_t6TC0Q6Jf_5nvr_x2DIKP4Fq5bPlWT449uj-t4xauiseuifYzkiLdY0r7Q5jrBIzgOgMutWWyYPSIbrbMO-IbwkFZXw/s1600/monspy.jpg)

如果对波动创新的敏感性捕获了风险溢价，那么标准 CAPM beta 的平（最好）回报意味着一定存在某种风险因素来抵消波动性和市场之间的负相关性。无论是什么，都毫无意义。也就是说，在 1987 年 10 月、2001 年 9 月和 2008 年 10 月可能取得了不错的回报，但仍然是正平均收益。我愿意听取建议，但这听起来很莫名其妙。

[飞行意大利面因子](http://www.venganza.org/)

。

请注意，一个失败理论的标志是随着数据变得更加清晰和更加丰富，理论变得不那么清晰。首先，风险是与股市的协方差相关，但自那以后，它变得更加细致，并且总是为风险溢价找到一个新的代理人，据说是“强大的新计量经济学技术”所能揭示的。
