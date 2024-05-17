<!--yml
category: 未分类
date: 2024-05-12 21:32:46
-->

# Falkenblog: Felix Salmon Highlights Financial Inconsistency

> 来源：[http://falkenblog.blogspot.com/2010/05/felix-salmon-highlights-financial.html#0001-01-01](http://falkenblog.blogspot.com/2010/05/felix-salmon-highlights-financial.html#0001-01-01)

Felix Salmon was on the HuffPost on May 10,

[telling people to sell](http://www.huffingtonpost.com/2010/05/08/felix-salmons-message-to_n_568989.html)

, and generated 2904 comments and counting. This was just after the big system debacle, where volatility spiked and markets swooned. With hindsight, this was a bad idea, but that's not important.

In

[this](http://blogs.reuters.com/felix-salmon/2010/05/10/why-volatility-means-you-should-sell-stocks/)

blog post, Felix explains his logic. The basic idea comes straight out of our standard utility model of risk and return. The idea is basically that if you have a utility function that is standard

^*

, your desire for stocks should obey the equation:

> % wealth in stock = Expected Return / (volatility^2 × RiskCoefficient)

So, we have three variables determining one's equity allocation. The risk coefficient constant is usually considered to be between 1 and 3, lets say 2 (as Salmon assumes). A higher risk coefficient means you are more risk averse, and note that if you increase it, your percent allocation of wealth to stocks goes to zero. The numerator is the expected return premium one gets for investing in the stock market. Most people assume this is 5% annually (I think it's

[practically zero](http://falkenblog.blogspot.com/2009/07/is-equity-risk-premium-actually-zero.html)

). Finally, we have the variance of returns, or volatility squared. As 'the market' is diversified (unlike a single stock), the market's variance should be linearly related to priced risk. Luckily, we have a good proxy for that, the

[VIX index](http://en.wikipedia.org/wiki/VIX)

, which is a forward looking estimate of future volatility based on option values. This is really what changed, and drove Felix's recommendation.

On May 6 implied volatility on options went from 25% to 40%, implying to Salmon one should drastically reduces their market exposure. Plugging in the numbers, we see this allocation goes from 40% to 15.63%, a massive re-allocation. That is, theoretically, one should sell over half your equities according to the ineluctable logic of economics!

One way to note it's wrong, is that prices and quantities exist in an equilibrium. In the short run, quantities don't change, so if preferences or expectations change, then prices must adjust, not quantities. If this theory explains what everyone is doing (on average), it must affect prices and not the allocation to equities, because not everyone can sell over half their equities overnight: someone would have to buy them! So in equilibrium, the only way this allocation percentage applied to stocks stayed constant, if 1) risk aversion

decreased

, or 2) their expected return

increased

.

As volatility

²

went up by 2.56 in my example (from 0.25

²

to 0.40

²

), is it reasonable to think people became, suddenly, 2.56 times

less

risk averse? One can't observe 'risk aversion' directly, but this is highly implausible, because intuitively during a panic, people become more risk averse. That leaves the expected return. Presumably, the risk premium, the return you get for the displeasure of bearing undiversifiable risk, had to have risen 2.56 times. But this turns out to be an empirical matter: do expected returns rise when volatility rises? Is it plausible that during this cataclysm, people were simultaneously increasing their prospective anticipation of future returns?

I think anyone with common sense realizes these are bat-shiat crazy interpretations of what the representative investor was thinking.

The data on actual returns and market volatility is, if anything, negatively correlated. That is, think of volatile years, and you'll think of the worst years: 1990, 2008, 2001, 2002\. But the standard response to such empirical rejections is to note that actual returns aren't the same as expected returns, they vary by some statistical noise, and so perhaps we just don't have enough data. Logically possible, though after over 50 years mining all the data ever recorded for the elusive 'risk factor' that explains asset return variability, I'm thinking it's improbable.

[Steve Sharpe and Gene Amromin](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1327134)

actually got around this objection by looking at survey data, and found that in questionnaires investors tended to have higher return expectations when they forecast volatility as being relatively low, and lower return expectations when they forecast higher volatility. Exactly the opposite of what they should be thinking. This isn't a missing a constant in the second decimal, rather, screwing up the sign.

As this is consistent with the theme of my book

[Finding Alpha](http://www.efalken.com/video/index.html)

, I thought this paper was awesome, and asked Steve Sharpe why it wasn't in a journal. He noted that referees just kept sending it back for various reasons. This is unsurprising, because all the referees presume there must be some sort of mistake, that this can't be true; it's counter to all their theoretical training. It reminds me of my attempt to get

[this paper](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1420356)

published, which was rejected at several publications for being wrong, obvious, and irrelevant, which merely highlighted to me they didn't like it. I don't think it's a conspiracy, just another example that theory can make you see facts as noisy exceptions or highly important and causes you to respond accordingly. People see what they believe, not vice versa, so Sharpe's fact has to be wrong according to these referees.

Sharpe's result really puts the standard model in a box. Unlike the CAPM betas, for which we can say we 'just don't know the true market portfolio', this result takes fewer assumptions, so its empirical failure is all the more fatal to the core financial theory. People should be increasing their expected returns in volatile markets, and on average that should manifest itself in actual returns. We don't see that in actual returns, or in surveys of expected returns.

A powerfully bad theory is like a lie--it has many inconsistencies because it isn't true (a worse bad theory is wrong and consistent with the data, but merely because it doesn't predict anything). One of the many bad implications of having the delusion that risk begets a higher expected return is that people invest in the stock market thinking they then deserve a higher return, a strategy that worked pretty well in the US in the 20th century, as long as you implemented a low-cost strategy that minimized trading and taxes. In reality, you either have to hope for lady luck, or actually do a lot of work finding your investing alpha looking for subtle patterns, or like Warren Buffet actually manage the companies you own to perform better than average. The idea that a passive approach to equities implies higher-than-average returns puts you at the mercy of brokers who may be selling diamonds in the rough, but usually are selling hope (

it's a Black Swan, trust me, I'm smart!

).

If you don't expect a return merely for shelling out your dough, you see investing in a risky asset class as merely a necessary condition for higher-than-average returns, not a sufficient condition. This insight would encourage a great deal more prudence where it is needed.

* a standard utility function is of the form U(x)=x^(1-a)/(1-a), where x is your wealth or consumption, and 'a' is your coefficient of relative risk aversion. It has the desirable condition that your relative pain to a 40% loss is the same whether you are rich or poor (desirable because otherwise risk aversion should have gone down a lot over the past 100 years as we have gotten wealthier).