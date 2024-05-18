<!--yml
category: 未分类
date: 2024-05-18 07:03:24
-->

# Physics Perspective: Private information and jumps in the market

> 来源：[http://physicsoffinance.blogspot.com/2011/10/private-information-and-jumps-in-market.html#0001-01-01](http://physicsoffinance.blogspot.com/2011/10/private-information-and-jumps-in-market.html#0001-01-01)

Following my

[second recent post](http://physicsoffinance.blogspot.com/2011/10/what-moves-markets-part-ii.html)

on what moves the markets, two readers posted interesting and noteworthy comments and I'd like to explore them a little. I had presented evidence in the post that many large market movements do not appear to be linked to the sudden arrival of public information in the form of news. Both comments noted that this may leave out of the picture another source of information -- private information brought into the market through the action of traders taking actions:

> and...
> 
> > Both of these comments note the possibility that every single trade taking place in the market (or at least many of them) may be revealing some fragment of private information on the part of whoever makes the trade. In principle, it might be such private information hitting the market which causes large movements (the s-jumps described in
> > 
> > [the work](http://arxiv.org/PS_cache/arxiv/pdf/0803/0803.1769v1.pdf)
> > 
> > of Joulin and colleagues).  
> > 
> > I think there are several things to note in this regard. The first is that, while this is a sensible and plausible idea, it shouldn't be stretched too far. Obviously, if you simply
> > 
> > *assume*
> > 
> > that all trades carry information about fundamentals, then the EMH -- interpreted in the sense that "prices move in response to new information about fundamentals" -- essentially becomes true by definition. After all, everyone agrees that trading drives markets. If all trading is assumed to reveal information, then we've simple assumed the truth of the EMH. It's a tautology.
> > 
> > More useful is to treat the idea as a hypothesis requiring further examination. Certainly some trades do reveal private information, as when a hedge fund suddenly buys X and sells Y, reflecting a belief based on research that Y is temporarily overvalued relative to X. Equally, some trades (as mentioned in the first comment) may reveal no information, simply being carried out for reasons having nothing to do with the value of the underlying stock. As there's no independent way -- that I know of -- to determine if a trade reveals new information or not, we're stuck with a hypothesis we cannot test.
> > 
> > But some research has tried to examine the matter from another angle. Again, consider large price movements -- those in the fat-tailed end of the return distribution. One proposed idea looking to private information as a cause proposes that large price movements are caused primarily by large-volume trades by big players such as hedge funds, mutual funds and the like. Some such trades might reveal new information, and some might not, but let's assume for now that most do. In
> > 
> > [a paper](http://polymer.bu.edu/hes/articles/ggps03.pdf)
> > 
> > in
> > 
> > *Nature*
> > 
> > in 2003, Xavier Gabaix and colleagues argued that you can explain the precise form of the power law tail for the distribution of market returns -- it has an exponent very close to 3 -- from data showing that the size distribution of mutual funds follows a similar power law with an exponent of 1.05\. A key assumption in their analysis is that the price impact
> > 
> > Δp
> > 
> > generated by a trade of volume V is roughly equal to
> > 
> > Δp = kV^(1/2)
> > 
> > .
> > 
> > This point of view seems to support the idea that the arrival of new private information, expressed in large trades, might account for the no-news s jumps noted in the Jouvin study. (It seems less plausible that such revealed information might account for anything as violent as the 1987 crash, or the general meltdown of 2008). But taken at face value, these arguments at least seem to be consistent with the EMH view that even many large market movements reflect changes in fundamentals. But again, this assumes that all or at least most large volume trades are driven by private information on fundamentals, which may not be the case. The authors of this study themselves don't make any claim about whether large volume trades really reflect fundamental information. Rather, they note that...
> > 
> > > Such a theory where large individual participants move the market is consistent with the evidence that stock market movements are difficult to explain with changes in fundamental values...
> > 
> > But more recent research (
> > 
> > [here](http://www.santafe.edu/media/workingpapers/04-02-006.pdf)
> > 
> > and
> > 
> > [here](http://arxiv.org/PS_cache/arxiv/pdf/0803/0803.1769v1.pdf)
> > 
> > , for example) suggest that this explanation doesn't quite hang together because the assumed relationship between large returns and large volume trades isn't correct. This analysis is fairly technical, but is based on the study of minute-by-minute NASDAQ trading and shows that, if you consider only extreme returns or extreme volumes, there is no general correlation between returns and volumes. The correlation assumed in the earlier study may be roughly correct on average, but it not true for extreme events. "Large jumps," the authors conclude, "are not induced by large trading volumes."
> > 
> > Indeed, as the authors of these latter studies point out, people who have valuable private information don't want it to be revealed immediately in one large lump because of the adverse market impact this entails (forcing prices to move against them). A well-known paper by Albert Kyle from 1985 showed how an informed trader with valuable private information, trading optimally, can hide his or her trading in the background of noisy, uninformed trading, supposing it exists. That may be rather too much to believe in practice, but large trades do routinely get broken up and executed as many small trades precisely to minimize impact. 
> > 
> > All in all, then, it seems we're left with the conclusion that public or private news does account for
> > 
> > *some*
> > 
> > large price movements, but cannot plausibly account for all of them. There are other factors. The important thing, again, is to consider what this means for the most meaningful sense of the EMH, which I take to be the view that market prices reflect fundamental values fairly accurately (because they have absorbed all relevant information and processed it correctly). The evidence suggests that prices often move quite dramatically on the basis of no new information, and that prices may be driven as a result quite far from fundamental values.
> > 
> > The latter papers do propose another mechanism as the driver of routine large market movements. This is a more mechanical process centering on the natural dynamics of orders in the order book. I'll explore this in detail some other time. For now, just a taster from
> > 
> > [this paper](http://arxiv.org/PS_cache/arxiv/pdf/0803/0803.1769v1.pdf)
> > 
> > , which describes the key idea:
> > 
> > > So what is left to explain the seemingly spontaneous large price jumps? We believe that the explanation comes from the fact that markets, even when they are ‘liquid’, operate in a regime of vanishing liquidity, and therefore are in a self-organized critical state [31]. On electronic markets, the total volume available in the order book is, at any instant of time, a tiny fraction of the stock capitalisation, say 10^(−5) −10^(−4) (see e.g. [15]). Liquidity providers take the risk of being “picked off”, i.e. selling just before a big upwards move or vice versa, and therefore place limit orders quite cautiously, and tend to cancel these orders as soon as uncertainty signals appear. Such signals may simply be due to natural fluctuations in the order flow, which may lead, in some cases, to a catastrophic decay in liquidity, and therefore price jumps. There is indeed evidence that large price jumps are due to local liquidity dry outs.