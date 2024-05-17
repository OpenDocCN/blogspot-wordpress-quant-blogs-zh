<!--yml
category: 未分类
date: 2024-05-12 23:13:57
-->

# Falkenblog: Espen Haug's Delusion

> 来源：[http://falkenblog.blogspot.com/2008/06/espen-haugs-delusion.html#0001-01-01](http://falkenblog.blogspot.com/2008/06/espen-haugs-delusion.html#0001-01-01)

Around 2004 I received an Excel workbook with 45 different worksheets containing derivative models from a friend of a friend, with a pretty useful GUI, and outputs included many greeks. Incredibly impressive. It was created by

[Espen Haug](http://www.espenhaug.com/articles.html)

, who has written some texts on derivatives. He clearly knows about derivatives formulas. But I hear he was in Stockholm last weekend, giving a

[talk](http://omxnordicexchange.com/derivativesweek)

at the OMX exchange with some other well-known finance types, which was described breathlessly as

[follows](http://www.dailyspeculations.com/wordpress/?p=2980)

over at Daily Speculations:

> Dr. Haug started the day by talking about fat tails, past, present and future. Among the most interesting part of his speech was his alluding to having in the drawer some theories on new distributions and implications for option trading. But he didn't go further on the record but said that he would probably write a bit about in on Wilmott. His gave a very good speech, so I for one will definitely be on the lookout for his findings.

I have

[read](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1012075)

where Haug is going, and find it boring. He basically argues that since stock prices have discontinuous fat tails that are hard to estimate, Black-Scholes fails. So, we should adjust Black-Scholes. But that's what the volatility smile, or smirk (depending on the market) does. Further, the bid-ask is sufficiently large that a price taker can't make money anticipating these 'unexpected' crashes. I know a couple of option market makers in little Minneapolis, and they all drive nice cars. Retail option traders, meanwhile, are forever operating on the hope that 1) no one knows the real risk that stock X will implode or 2) by putting on a complex of options, you can lock in some above average return. Thus, the nice cars.

As per Haug and Taleb's argument that we shouldn't call Black-Scholes Black-Scholes, I find this a bit like changing the name of the pterodactyl to a pterodon. Is it necessary? While Haug pooh-pooh's Black, Scholes, and Merton, for

merely

proving that the discount rate should be the riskless rate, I think this is a pretty important finding. Risk is supposed to be darn important, and so, taking risk out of the equation turned a really hairy problem into a much simpler one. There are lots of option formulas that add terms to account for skewness, jumps and fat tails, but practice shows that people prefer merely applying the 'inconsistent' volatility surface rather than adding these parameters. Over time, a good option trader can them memorize the vol/strike/maturity gridspace, then monitor the changes level and sometimes shape of the vol surface. Any discovery stands on the shoulders of others, but it's really academic hair splitting to start a crusade to change the name of a formula based on some earlier, more obscure work by Thorpe or Bachelier that had parameters unexplained (that's why they have fewer cites). Rules of thumb in financial markets can make you rich, but they don't give you Nobel Prizes or naming rights. In any case, what would renaming Black-Scholes at this point do, other than confuse everyone?

Pablo Tirana

[notes](http://www.portfolio.com/views/blogs/market-movers/2007/11/08/has-nassim-taleb-killed-black-scholes)

that Haug and Taleb have another new big idea.

> They argue that actual option prices on the open market may be simply the result of the interaction of supply and demand, with no formula involved. The second implication of Taleb and Haug is that implied volatility, a ubiquitous element of the markets, ceases to make sense. In fact, it would cease to exist... Rather than being the “market´s expected future turbulence” or the “market´s fear gauge”, as conventional wisdom would hold, implied volatility would have proven itself to be nothing but make-believe. A nonexistent ghost.

Well, if the implied of an option is 40, because this is the 'wrong vol in the wrong model to get the right price', and they think this implied is primarily due to supply and demand as opposed to actual volatility forecasts, then they should be able to make money pretty easily. Good luck with that. Given the bid-ask in option markets, you probably need only a 5-7 vol 'mismatch' to create an arbitrage via (gasp!) delta hedging an option. I think its really bad advice to tell people that implieds are almost arbitrary, hardly correlated with actual volatilities.

At the end of the day, no matter how smart someone is, how much math they know, they have one, or a couple, of 'big ideas'. Usually these ideas are just as silly as the big ideas that come from people who know very little math.