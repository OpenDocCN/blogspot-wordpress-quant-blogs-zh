<!--yml
category: 未分类
date: 2024-05-18 07:04:44
-->

# Physics Perspective: High-frequency trading, the downside -- Part II

> 来源：[http://physicsoffinance.blogspot.com/2011/09/high-frequency-trading-downside-part-ii.html#0001-01-01](http://physicsoffinance.blogspot.com/2011/09/high-frequency-trading-downside-part-ii.html#0001-01-01)

In this post I'm going to look a little further at Andrew Haldane's

[recent Bank of England speech](http://www.bankofengland.co.uk/publications/speeches/2011/speech509.pdf)

on high-frequency trading.

[In Part I](http://physicsoffinance.blogspot.com/2011/09/high-frequency-trading-downside-part-i.html)

of this post I explored the first part of the speech which looked at evidence that HFT has indeed lowered bid-ask spreads over the past decade, but also seems to have brought about an increase in volatility. Not surprisingly, one measure doesn't even begin to tell the story of how HFT is changing the markets. Haldane explores this further in the second part of the speech, but also considers in a little more detail where this volatility comes from.

In

[well known study back in 1999](http://polymer.bu.edu/hes/articles/gpams99.pdf)

, physicist Parameswaran Gopikrishnan and colleagues (from Gene Stanley's group in Boston) undertook what was then the most detailed look at market fluctuations (using data from the S&P Index in this case) over periods ranging from 1 minute up to 1 month. This early study established a finding which (I believe) has now been replicated across many markets -- market returns over timescales from 1 minute up to about 4 days all followed a fat-tailed power law distribution with exponent α close to 3\. This study found that the return distribution became more Gaussian for times longer than about 4 days. Hence, there seems to be rich self-similarity and fractal structure to market returns on times down to 1 around second.

What about shorter times? I haven't followed this story for a few years. It turns out that in 2007, Eisler and Kertesz

[looked at a different set of data](http://arxiv.org/abs/physics/0606161)

-- for total transactions on the NYSE between 2000 and 2002 -- and found that the behaviour at short times (less than 60 minutes) was more Gaussian. This is reflected in the so-called Hurst exponent H having an estimated value close to 0.5\. Roughly speaking, the Hurst exponent describes -- based on empirical estimates -- how rapidly a time series tends to wander away from its current value with increasing time. Calculate the root mean square deviation over a time interval T and for a Gaussian random walk (Brownian motion) this should grow in proportion to T to the power H= 1/2\. A Hurst exponent higher than 1/2 indicates some kind of interesting persistent correlations in movements.

However, as Haldane notes, Reginald Smith

[last year showed](http://arxiv.org/PS_cache/arxiv/pdf/1006/1006.5490v1.pdf)

that stock movements over short times since around 2005 have begun showing more fat-tailed behaviour with H above 0.5\. That paper shows a number of figures showing H rising gradually over the period 2002-2009 from 0.5 to around 0.6 (with considerable  fluctuation on top of the trend). This rise means that the market on short times has increasingly violent excursions, as Haldane's chart 11 below illustrates with several simulations of time series having different Hurst exponents:

[![](img/bb1b2a9a3ab44058065bc113160920ee.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg8zckvqRdXupKJuWW1XoOrMqZRStpMugLSq5tBzmxL-YvHqpqQsFFh1-WJ1qLLKa8S__lAU-euwtToPLWrjURLkSuXh-NCLXPXbawmd5XMbXyDI98eShpCljwyjdGDK9vYyJOBYI2eUfC0/s1600/haldane_hft_chart11.jpg)

The increasing wildness of market movements has direct implications for the risks facing HFT market makers, and hence, the size of the bid-ask spread reflecting the premium they charge. As Haldane notes, the risk a market maker faces -- in holding stocks which may lose value or in encountering counterparties with superior information about true prices -- grows with the likely size of price excursions over any time period. And this size is directly linked to the Hurst exponent.

Hence, in increasingly volatile markets, HFTs become less able to provide liquidity to the market precisely because they have to protect themselves:

> This has implications for the dynamics of bid-ask spreads, and hence liquidity, among HFT firms. During a market crash, the volatility of prices (σ) is likely to spike. From equation (1), fractality heightens the risk sensitivity of HFT bid-ask spreads to such a volatility event. In other words, liquidity under stress is likely to prove less resilient. This is because one extreme event, one flood or drought on the Nile, is more likely to be followed by a second, a third and a fourth. Reorganising that greater risk, market makers’ insurance premium will rise accordingly.
> 
> This is the HFT inventory problem. But the information problem for HFT market-makers in situations of stress is in many ways even more acute. Price dynamics are the fruits of trader interaction or, more accurately, algorithmic interaction. These interactions will be close to impossible for an individual trader to observe or understand. This algorithmic risk is not new. In 2003, a US trading firm became insolvent in 16 seconds when an employee inadvertently turned an algorithm on. It took the company 47 minutes to realise it had gone bust.
> 
> Since then, things have stepped up several gears. For a 14-second period during the Flash Crash, algorithmic interactions caused 27,000 contracts of the S&P 500 E-mini futures contracts to change hands. Yet, in net terms, only 200 contracts were purchased. HFT algorithms were automatically offloading contracts in a frenetic, and in net terms fruitless, game of pass-the-parcel. The result was a magnification of the fat tail in stock prices due to fire-sale forced machine selling.
> 
> These algorithmic interactions, and the uncertainty they create, will magnify the effect on spreads of a market event. Pricing becomes near-impossible and with it the making of markets. During the Flash Crash, Accenture shares traded at 1 cent, and Sotheby’s at $99,999.99, because these were the lowest and highest quotes admissible by HFT market-makers consistent with fulfilling their obligations. Bid-ask spreads did not just widen, they ballooned. Liquidity entered a void. That trades were executed at these “stub quotes” demonstrated algorithms were running on autopilot with liquidity spent. Prices were not just information inefficient; they were dislocated to the point where they had no information content whatsoever.

This simply follow from the natural dynamics of the market, and the situation market makers find themselves in. If they want to profit, if they want to survive, they need to manage their risks, and these risks grow rapidly in times of high volatility. Their response is quite understandable -- to leave the market, or least charge much more for their service. 

Individually this is all quite rational, yet the systemic effects aren't likely to benefit anyone. The situation, Haldane notes, resembles a Tragedy of the Commons in which individually rational actions lead to a collective disaster, fantasies about the Invisible Hand notwithstanding:

> If the way to make money is to make markets, and the way to market markets is to make haste, the result is likely to be a race – an arms race to zero latency. Competitive forces will generate incentives to break the speed barrier, as this is the passport to lower spreads which is in turn the passport to making markets. This arms race to zero is precisely what has played out in financial markets over the past few years.
> 
> Arms races rarely have a winner. This one may be no exception. In the trading sphere, there is a risk the individually optimising actions of participants generate an outcome for the system which benefits no-one – a latter-day “tragedy of the commons”. How so? Because speed increases the risk of feasts and famines in market liquidity. HFT contribute to the feast through lower bid-ask spreads. But they also contribute to the famine if their liquidity provision is fickle in situations of stress.

Haldane then goes on to explore what might be done to counter these trends. I'll finish with a third post on this part of the speech very soon. 

But what is perhaps most interesting in all this is how much of Haldane's speech refers to recent work done by physicists -- Janos Kertesz, Jean-Philippe Bouchaud, Gene Stanley, Doyne Farmer and others -- rather than studies more in the style of neo-classical efficiency theory. It's encouraging to see that at least one very senior banking authority is taking this stuff seriously.