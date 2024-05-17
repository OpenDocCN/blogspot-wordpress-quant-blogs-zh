<!--yml
category: 未分类
date: 2024-05-18 07:07:01
-->

# Physics Perspective: How derivatives make markets unstable: Part I

> 来源：[http://physicsoffinance.blogspot.com/2011/07/how-derivatives-make-markets-unstable.html#0001-01-01](http://physicsoffinance.blogspot.com/2011/07/how-derivatives-make-markets-unstable.html#0001-01-01)

I posted a while back on some of the

[dirty secrets of the derivatives industry](http://physicsoffinance.blogspot.com/2011/06/dirty-little-derivatives-secrets.html)

. I promised then to give a little more discussion at some point of two terrifically important pieces of research -- still not widely known, especially in mainstream finance -- which show how adding more derivatives to a market can make it less stable, not more stable. This goes directly against the received wisdom of economic (equilibrium) theory which claims that markets become more efficient as they become more complete, i.e. as it becomes possible to take essentially any kind of market position by virtue of a dense spectrum of financial instruments.

One of the papers I had in mind was

[this landmark study](http://www1.fee.uva.nl/cendef/upload/2/BroHomWagHedging2009Feb.pdf.pdf)

from several years ago in which William Brock, Cars Hommes and Florian Wagener considered the question of whether, in the run up to the recent crisis, "... highly leveraged positions using complex financial instruments may have amplified market volatility." The answer to which their analysis leads is -- yes, quite probably. More generally, they illustrate how more derivatives in general should make markets more unstable, increasing volatility.

Their paper is a little technical, but worth a read. I'll outline the gist of their argument, which starts with several straightforward observations and moves to a not-so-obvious conclusion:

Observation 1: They start by noting that people aren't the hyper-rational automatons of Milton Friedman's (or other neo-classical economists') favorite fantasies. Rather, people in the real world form their expectations and craft their behaviour in an adaptive way -- that is, they learn from experience.

Observation 2: They also note that people aren't identical. We not only learn, but our brains are different and we've all had different experiences in the past, so, at any moment, we've probably learned different things and have slightly different expectations (heterogeneous expectations, in economic lingo) about the future.

Observation 3: People are generally risk averse -- if they're willing to bet $100 on a gamble that could pay off, but involves risks, they'll be willing to bet more than $100 in the same gamble if you reduce the risks. In other words, people shy away from gambles more the riskier they are. This is basic empirical psychology.

Starting from these observations, Brock and colleagues then consider an "intertemporal" asset market (economist-speak meaning a market in which time exists) in which a lot of people look to past prices and try to predict future prices, buying and selling as they see fit. This market contains both risky and non-risky things to invest in -- stocks and risk-free bonds (which are guaranteed to increase in value by a factor R>1 over each interval of time). Stocks might rise more, but are less certain and hence riskier. In addition, the people can buy derivatives -- instruments which act like pure bets and give a pay off in certain circumstances.

What this all amounts to is that people in this market can 1) play it safe by buying bonds, 2) gamble more by buying stocks, and also 3) buy derivatives if they want which (in this model) have no effect except to offset some of the risks involved in buying stocks.

What Brock and colleagues then show is that the combination of the derivatives, the risk aversion of investors, and their tendency to learn by "reinforcement" -- to be more likely to follow strategies which have paid off in the past -- leads directly to trouble. I'll describe how in a moment, but one final thing before I do: the strength of reinforcement learning in the model (how quickly people shift to use better performing strategies) is controlled by one parameter β; bigger β means faster switching. In previous work, Brock and Hommes have shown that in an asset market in which people learn by the reinforcement process, there is a natural "tipping point" -- at a certain critical value of β -- where the market goes from being stable to being unstable. Intuitively, when people switch too quickly, taking even scanty short term evidence as proof of a strategy's superiority, fluctuations in the market become much stronger.

OK, so what happens in this market when you currently have, say, 15 possible derivatives covering lots of different possible outcomes, and now add a 16th derivative to cover other outcomes (i.e. we have derivatives on stocks and commodities, and suddenly invent some new ones to cover mortgage bonds)? Brock and colleagues show that the addition of this one new derivative makes the market go unstable more quickly, i.e. at a lower value of β. The mechanism involves a simple interplay of reduced risk and human confidence. This new derivative, by making it possible for investors to lower the risks associated with investments, leads them to invest more money. They take bigger bets. These bigger bets naturally amplify how quickly the bets that turn out to be correct amass profits. So, there are bigger differences in the payoffs to recent winning and losing strategies, which draws more followers to the winners more quickly (even if the fundamental switching rate of people haven't changed).

In brief: by the very act of reducing the risk of some strategies, the derivative invites more vigorous gambling on that strategy, leading to faster flows of people from one strategy to another. The extra derivative makes the market more volatile.

This model doesn't involve many questionable assumptions. It's a very basic model of the most central facts of any market, respecting some realities of human psychology. It suggests that derivatives hold inherent dangers. Yet as far as I can see, the ongoing discussion of regulating derivatives isn't taking this perspective into account. As Satyajit Das

[notes](http://www.wilmott.com/blogs/satyajitdas/index.cfm/2011/1/24/Derivative-Regulation-Dances--Part-1)

, the drive toward greater returns that is an essential part of the dynamics in the Brock, Hommes and Wagener model is a very real force in today's derivatives markets:

> Investors searching for return drive speculation. Concerned about stagnant real incomes and inadequate retirement savings, individual investors seek out higher yielding investment structures, often based on derivatives. Pension funds and other institutional investors use derivatives to enhance returns to fully fund and meet their contracted liabilities. In an environment of diminishing returns and fierce competition for attractive investments, fund managers use derivative strategies to enhance returns through readily accessible leverage and capacity to create risk “cocktails”.
> 
> Facing increased pressure on earnings, corporations have increasingly “financialised”, resorting to speculative derivative trading to meet profit expectations. ... [Such] seculative activity amplifies rather than reduces volatility and systemic risks. Perversely, this may impede capital formation and also increase the cost of capital for companies.

What happens in the real world backs up the lesson of this simple model. Derivatives reduce risks only in a very narrow and restricted sense, while undermining the functioning of markets more generally. Of course, there's lots of money to be made by the people selling derivatives, so don't expect them to admit (or care about) any of this.