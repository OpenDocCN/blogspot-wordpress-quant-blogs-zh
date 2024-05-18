<!--yml
category: 未分类
date: 2024-05-18 07:03:33
-->

# Physics Perspective: What moves the markets? Part II

> 来源：[http://physicsoffinance.blogspot.com/2011/10/what-moves-markets-part-ii.html#0001-01-01](http://physicsoffinance.blogspot.com/2011/10/what-moves-markets-part-ii.html#0001-01-01)

High frequency trading makes for markets that produce enormous volumes of data. Such data make it possible to test some of the old chestnuts of market theory -- the efficient markets hypothesis, in particular -- more carefully than ever before. Studies in the past few years show quite clearly, it seems to me, that the EMH is very seriously misleading and isn't really even a good first approximation.

Let me give a little more detail. In

[a recent post](http://physicsoffinance.blogspot.com/2011/10/what-moves-markets-part-i.html)

I began a somewhat leisurely exploration of considerable evidence which contradicts the efficient markets idea. As the efficient markets hypothesis (the "weak" version, at least) claims, market prices fully reflect all publicly available information. When new information becomes available, prices respond. In the absence of new information, prices should remain more or less fixed.

Striking evidence against this view comes from studies (now almost ten or twenty years old) showing that markets often make quite dramatic movements even in the *absence* of any news. I looked at some older studies along these lines in the last post, but stronger evidence comes from studies using electronic news feeds and high-frequency stock data. Are sudden jumps in prices in high frequency markets linked to the arrival of new information, as the EMH says? In a word -- no!

The idea in these studies is to look for big price movements which, in a sense, "stand out" from what is typical, and then see if such movements might have been caused by some "news". A good example is

[this study](http://arxiv.org/PS_cache/arxiv/pdf/0803/0803.1769v1.pdf)

by Armand Joulin and colleagues from 2008\. Here's how they proceeded. Suppose R(t) is the minute by minute return for some stock. You might take the absolute value of these returns, average them over a couple hours and use this as a crude measure -- call it σ -- of the "typical size" of one-minute stock movements over this interval. An unusually big jump over any minute-long interval will be one for which the magnitude of R is much bigger than σ. 

To make this more specific, Joulin and colleagues defined "s jumps" as jumps for which the ratio |R/σ| > s. The value of s can be 2 or 10 or anything you like. You can look at the data for different values of s, and the first thing the data shows -- and this isn't surprising -- is a distinctive pattern for the probability of observing jumps of size s. It falls off with increasing s, meaning that larger jumps are less likely, and the mathematical form is very simple -- a power law with P(s) being proportional to s

^(-4)

, especially as s becomes large (from 2 up to 10 and beyond). This is shown in the figure below (the upper curve):

This pattern reflects the well known "fat tailed" distribution of market returns, with large returns being much more likely than they would be if the statistics followed a Gaussian curve. Translating the numbers into daily events, s jumps of size s = 4 turn out to happen about 8 times each day, while larger jumps of s = 8 occur about once every day and one-half (this is true for each stock).

Now the question is -- are these jumps linked to the announcement of some new information? To test this idea, Joulin and colleagues looked at various news feeds including feeds from Dow Jones and Reuters covering about 900 stocks. These can be automatically scanned for mention of any specific company, and then compared to price movements for that company. The first thing they found is that, on average, a new piece of news arrives for a company about once every 3 days. Given that a stock on average experiences one jump every day and one-half, this immediately implies an imbalance between the number of stock movements and the number of news items. There's not enough news to cause the jumps observed. Stocks move -- indeed, jump -- too frequently.

Conclusion: News sometimes but not always causes market movements, and significant market movements are sometimes but not always caused by news. The EMH is wrong, unless you want to make further excuses that there could have been news that caused the movement, and we just don't recognize it or haven't yet figured out what it is. But that seems like simply positing the existence of further epicycles.

But another part of the Joulin

*et al.*

study is even more interesting. Having found a way to divide price jumps into two categories: A) those caused by news (clearly linked to some item in a news feed) and B) those unrelated to any news, it is then possible to look for any systematic differences in the way the market settled down after such a jump. The data show that the volatility of prices, just after a jump, becomes quite high; it then relaxes over time back to the average volatility before the jump. But the relaxation works differently depending on whether the jump was of type A or B: caused by news or not caused by news. The figure below shows how the volatility relaxes back to the norm first for jumps linked to news, and second to jumps not linked to news. The later shows a much slower relaxation:

As the authors comment on this figure,

> In both cases, we find (Figure 5) that the relaxation of the excess-volatility follows a power-law in time σ(t) − σ(∞) ∝ t− β (see also [22, 23]). The exponent of the decay is, however, markedly different in the two cases: for news jumps, we find β ≈ 1, whereas for endogenous jumps one has β ≈ 1/2\. Our results are compatible with those of [22], who find β ≈ 0.35.

Of course, β ≈ 1/2 implies a much slower relaxation back to the norm (whatever that is!) than does β ≈ 1\. Hence, it seems that the market takes a longer time to get back to normal after a no-news jump, whereas it goes back to normal quite quickly after a news-related jump.

No one knows why this should be, but Joulin and colleagues made the quite sensible speculation that a jump clearly related to news is not really surprising, and certainly not unnerving. It's understandable, and traders and investors can decide what they think it means and get on with their usual business. In contrast, a no-news event -- think of the Flash Crash, for example -- is very different. It is a real shock and presents a lingering unexplained mystery. It is unnerving and makes investors uneasy. The resulting uncertainty registers in high volatility.

What I've written here only scratches the surface of this study. For example, one might object that lots of news isn't just linked to the fate of one company, but pertains to larger macroeconomic factors. It may not even mention a specific company but point to a likely rise in the prices of oil or semiconductors, changes influencing whole sectors of the economy and many stocks all at once. Joulin and colleagues tried to take this into account by looking for correlated jumps in the prices of multiple stocks, and indeed changes driven by this kind of news do show up quite frequently. But even accounting for this more broad-based kind of news, they still found that a large fraction of the price movements of individual stocks do not appear to be linked to anything coming in through news feeds. As they concluded in the paper:

> Our main result is indeed that most large jumps... are not related to any broadcasted news, even if we extend the notion of ‘news’ to a (possibly endogenous) collective market or sector jump. We find that the volatility pattern around jumps and around news is quite different, confirming that these are distinct market phenomena [17]. We also provide direct evidence that large transaction volumes are not responsible for large price jumps, as also shown in [30]. We conjecture that most price jumps are in fact due to endogenous liquidity micro-crises [19], induced by order flow fluctuations in a situation close to vanishing outstanding liquidity.

Their suggestion in the final sentence is intriguing and may suggest the roots of a theory going far beyond the EMH. I've

[touched before](http://physicsoffinance.blogspot.com/2011/05/physics-envy.html)

on early work developing this theory, but there is much more to be said. In any event, however, data emerging from high-frequency markets backs up everything found before -- markets often make violent movements which have no link to news. Markets do not just respond to new information. Like the weather, they have a rich -- and as yet mostly unstudied -- internal dynamics.