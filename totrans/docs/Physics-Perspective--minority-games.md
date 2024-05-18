<!--yml
category: 未分类
date: 2024-05-18 07:01:26
-->

# Physics Perspective: minority games

> 来源：[http://physicsoffinance.blogspot.com/2012/02/minority-games.html#0001-01-01](http://physicsoffinance.blogspot.com/2012/02/minority-games.html#0001-01-01)

I have

[an essay just published](http://www.bloomberg.com/news/2012-02-07/a-bar-may-be-best-place-to-understand-markets-commentary-by-mark-buchanan.html)

in Bloomberg. The essay is quite short and I wanted to give interested readers a few more details and links to further reading on the subject: how to build simple yet plausible models of financial markets. Hence, this post.

Traditional models of markets in economics work from the idea of equilibrium. What happens in the market is assumed to reflect the interplay of two things: 1\. the decisions of countless market participants who act more or less rationally in their best interests, their actions collectively bringing the market toward a balance in which stocks, bonds, or other instruments take their realistic "fundamental" values (or at least something close to those values), and 2\. external shocks that hit the market in the form of new pieces of information concerning businesses, political events, changes in regulations, technological discoveries and so on. Without shocks from outside, these models imply, the market would settle down (very rapidly it is assumed) into an unchanging state. Everything that happens in the market, this perspective asserts, can be traced to new information perturbing that balance.

I've written before (

[here](http://physicsoffinance.blogspot.com/2011/05/whats-efficient-in-efficient-markets.html)

, for example, and

[here](http://physicsoffinance.blogspot.com/2011/10/what-moves-markets-part-i.html)

) about the considerable evidence against this picture. This includes many large market movements that occur in the absence of any apparent "shock" to the market, and "excess volatility" -- a general tendency for market prices to move more than they should by any rational reckoning of their true value. Many studies have established strong mathematical regularities in market fluctuations that reflect this excess volatility, including the

[fat tailed statistics of market returns](http://physicsoffinance.blogspot.com/2011/12/power-laws-in-finance.html)

and the long memory of returns -- the way markets absorb information, empirically, doesn't seem to be fast at all, but involves a long slow process of digestion stretching over a decade and more.

So, how to build models that go beyond this equilibrium picture? If the simple notion of equilibrium is too simple to explain market reality, why not non-equilibrium models? That is, models of markets in which the individuals' actions, even in the absence of outside shocks, never lead the market to settle down into some equilibrium balance. Rather, people might instead perpetually change their ideas and strategies, interacting in a way that gives the market a rich internal dynamics, much as the weather. Studies of very simple two player strategic games actually show that

[this kind of outcome should be expected](http://physicsoffinance.blogspot.com/2011/10/why-game-theory-is-often-useless.html)

in any case in which the decisions facing individuals are quite complex and not open to simple rational solution -- that is, in other words, in most cases (and obviously in the case of any real world market).

Science often makes progress by posing toy models that capture the logical essence of some problem. By struggling with it, people learn new ways of thinking. In my Bloomberg column I touched on one of the toy models that has recently inspired non-equilibrium models of markets. This is the so-called El Farol Bar problem invented by economist Brian Arthur in1994\.

[The original paper](http://tuvalu.santafe.edu/%7Ewbarthur/Papers/Pdf_files/El_Farol.pdf)

is still well worth a read; it's one of those papers that puts forth an idea so sound and plausible that it seems obvious, and it is hard to believe that its ideas were revolutionary and against everything in mainstream economic habit. To this day, this remains true. But enough background.

My Bloomberg column gives a rough introduction to the idea of the bar problem -- it is an archetype of a situation in which it is not possible for people to make decisions through rational deliberation, but rather have to take a more practical approach, forming hypotheses and theories, and learning from experience. The result is a dis-equilibrium situation that continues to evolve in time, never settling into an equilibrium. There are plenty of articles giving more detailed synopses of the model and how it works.

But the essence of the bar model has since then been explored in much greater detail through another model -- the so-called minority game. It's just the bar model stripped down to be as simple as possible while still preserving the essential element that no one in the game can "figure it out." There is no strictly rational way to play; intelligent play requires perpetual adaptation and learning. The minority game is probably the simplest mathematical model of a market in this sense. It is, of course, too simple to be anything more than a toy model. But it is, at least, a toy model looks a lot more like real markets than does the EMH or anything else in economics. And the benefit of its relative simplicity is that it is possible to see how various fundamental factors influence how it works, without thousands of other potential complications that obscure matters.

So --what is the minority game?

Arthur assumed that people would enjoy the bar is 60% of less attended, and would be miserable if more than 60% attended. The minority game simplifies the cutoff to 50%, giving symmetry to the problem -- now the people who do well on any week are those who act so as to be in the minority (going when most others stay home, and vice versa). The minority game also dispenses with the story of the bar. Just let each N agents on each play choose either 1 or -1, with those in the minority gaining some payoff (let N be odd). Now let them play many times. Each agent just goes along trying each time to be in the minority. How does one do that?

Of course, everything hinges on how we suppose the agents play. Following Arthur, the typical approach is to suppose that they use some kind of trial and error learning. The record of outcomes of the game is given by some sequence of 1s and -1s -- these giving the winning choices that would have been in the minority in each instance. For example, the last 5 outcomes might be 1,1,-1,-1,1\. A "strategy" in the minority game associates every such recent history with a choice of what to do next -- a choice of 1 or -1\. A strategy may say that IF (1,1,-1,-1,1) THEN choose 1, or instead IF (1,1,-1,-1,1) THEN choose -1\. If we suppose that agents look back to the past M outcomes in trying to forecast the future (this is often referred to as their "brain size"), then there are P=2

^M

different histories that the agents can resolve or discern. A strategy, mathematically speaking, is a map or association that assigns a choice 1 or -1 to each and every one of the possible P=2

^M

different histories. A strategy is a plan for action, if you will, an IF...THEN statement of what to do for every possible sequence of happenings (at the level the agents can perceive).

Now, since each possible sequence can be associated with 1 or -1, there are actually 2

^P

or 2

^(2^M)

different possible strategies. Even with M as low as 5, this is already 2

^(32)

which is well over one trillion different possible strategies. It grows extremely fast as M gets bigger.

The way the minority game is played is that, at the outset, each one of the players gets assigned a number S of these strategies at random. You can think of this as their intellectual inheritance. It's a collection of S different "ways to think" about how to predict the world. (The interesting properties of the model do not depend on this choice.) Agents use these strategies to play the game, and keep track of which strategies seem to work well, and which ones don't. This is generally done through some simple algorithm wherein each strategy in an agent's bag gains a point when it makes a good prediction, and gets docked a point if it predicts incorrectly. On each play, the agents look into their bag and play the strategy with the highest score. This is like a person mulling over the various theories in their head, and using the one that seems to have been most successful in the past.

So that's it. You have a collection of agents using simple learning dynamics to try to predict the future based on the past. They try at each moment to choose what most others will not choose. Clearly no one strategy can emerge as the winner, because if it did and everyone started using it then they would all be in the majority, and all be losers. Successful strategies, therefore, sow the seeds of their own demise. This is what makes the game interesting. But wait -- how is this linked to markets?

Qualitatively, the minority game is a little like a market. It's a situation in which each person tries to profit by choosing the right strategy, but where what is "right" is determined by the collective actions of everyone together. There is no "right" independent of what others do. The minority game, like any market, is a game involving an enormous and complex ecology of interacting strategies. Except there is no price. A minor addition can change that, however.

We get the simplest crude model of a market if we think of those choosing 1 as "buyers"  and those choosing -1 as "sellers" of some stock. Naturally, more buyers than sellers drives a price up, and an imbalance the other way drives it down. Mathematically, you can take the change in the logarithm of the price (the return) at time t as being proportional to Number(buyers) - Number(sellers). The resulting price has a highly erratic behaviour that very roughly resembles the movements of financial markets. In particular, even without any external information hitting the market, no shocks from outside or perturbations of any kind, the price fluctuates up and down unpredictably merely through the perpetual evolution of the agents' trading strategies. One day, apparently caused by nothing, the price may suddenly drop by 10% -- all because many agents chose to sell just as a part of trying to predict what was about to happen next.

This post has already gone on long enough. For lots of detail, I highly recommend

[this excellent review](http://arxiv.org/abs/physics/0608091)

of the minority game by Tobias Galla, Giancarlo Mosetti and Yi-Cheng Zhang, which I highly recommend (Zhang is one of the co-inventors of the minority game). There is a great deal more to say, but two points are most important for now:

1\. This simplest version of a minority-game market does NOT give rise to the so-called "stylized facts" of real markets -- the fat tailed statistics of return distributions, and the long memory and persistence of market volatility. In fact, the returns for this simplest minority game market are Gaussian, at least when the number of players is large. However, this model is only a beginning, and these stylized facts emerge quite naturally as soon as one includes a few more realistic features. For example, in this version of the game, every agent must either choose 1 (buy) or -1 (sell) at each moment. Hence, the volume of trading is always the same; it is forced to be fixed, which is of course completely unnatural.

An easy way to relax this is to give the agents the ability also to abstain -- they might just hold what they have, neither buying or selling. This can be included with some measure of confidence, whereby an agent doesn't trade unless one of its strategies has been very successful in the recent past. This immediately leads to a market with fluctuations in volume, and this market does turn out to have stylized facts much like those of real markets, with fat tailed returns and long memory. Another way to allow for a fluctuating volume is to let the agents accrue wealth over time, and let the volume of their trading grow in proportion to that wealth. Again, this is an obvious step toward reality, and again leads to market fluctuations with many of the rich statistical features seen in real markets, even in such simple models.

2\. The other important point is that the minority game is so simple that it can be solved with some analytical techniques borrowed from physics. The details aren't so important, but the results show a fascinating behaviour in the market with a kind of phase transition separating two distinct regimes of behaviour. The picture that emerges gives a beautiful coarse grain understanding of markets as ecologies of interacting agents.

The basic story is that one key parameter in the minority game determines its overall character. The parameter is α=P/N, where N is the number of agents in the game. If this is small, then there are lots of players relative to the number of different market histories they can perceive. If this is big, then there are many different possible histories relative to only a few people. These two extremes lead to very different market behaviour and it's not hard to see why.

The figure below (from the Galla et al paper) shows what is effectively the market predictability as a function of this parameter α=P/N. In other words, this shows how much a past record of prices can be used to make accurate predictions of future prices. For large α, this predictability is positive, and it grows as α grows. Why? In principle, this kind of predictability ought to make for easy success in the game. But only if the agents' have enough flexibility in their behaviour to pounce on the pattern and exploit it. In this regime, it happens frequently that patterns emerge in the prices and yet no agent has the intellectual capacity to exploit it. Recall that each individual is given a random set of strategies to work with. With very few people in the market, that means very few strategies relative to the many possible market histories on which the agents make their decisions. In short, if the diversity of agents and their behavioural strategies is insufficient to let them jump on all possible patterns, the market retains a degree of predictability.  

![](img/cf247eb1a5347c274534040039eac241.png)

For the opposite limit, α small, things look very different. Now we have an oversupply of agents and strategies in play relative to the number of discernible histories. Now it is very likely that any predictable pattern will suit some agent's bag of strategies, and that agent will jump on it, profit, and their activity will tend to wipe out that pattern. This phase looks rather like the efficient market -- such a rich diversity of agents with different skills and mindsets that any predictable patterns are immediately washed away.

One of the

[most interesting conjectures](http://arxiv.org/abs/cond-mat/9901243)

emerging from this picture is that real markets are probably something like "marginally efficient", at least much of the time. If fully efficient and hence unpredictable (many agents in the market, low α), then it's very hard to make profits in the market. This should make the market less attractive and some people should leave to do something else. But as the number of people falls, this pushed the market toward higher α and into the inefficient phase in which the market becomes predictable. This should in turn attract more people into the market to profit from easy patterns. In this simple picture, the market should tend to evolved toward a value of α where the predictability of prices is low but not zero, making it hard but not impossible to find patterns in the market. This is, judging in a loose non-scientific way, just about where markets often seem to be.  

Works on the minority game now number on the thousands, and I only wanted to get across the most basic points. It's a beautiful simple model that captures a great deal of the qualitative character of markets, and with further changes can be taken step by step toward more sophisticated models of markets. There's no reason to stick to idea that payoff go to those in the minority. The game has generalized, for example, to majority type games (where  trend following pays off) or mixed majority-minority games (where market reversion and trend following both play a role). A few steps further and you can forget the game itself and simply model markets as systems in which people interact with various trading strategies, each buying and selling, and where prices move through their collective action. Lots of models study a simple mixture of fundamentalists, who try to trade on the base of real information about stocks, and trend followers who ride the momentum. Computing power and imagination present the only limits.

I'm going to explore some of these more sophisticated models in future, but the minority game remains extremely important precisely because of its simplicity. That simplicity allows full analysis leading to the picture of two phases shown above. But this is already considerably more complex than market models based on assumed fully rational behaviour. It's crude, very much so, but a small step in the right direction.