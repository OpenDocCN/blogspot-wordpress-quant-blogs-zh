<!--yml
category: 未分类
date: 2024-05-12 21:49:58
-->

# Falkenblog: Physicists 'Solve' Two-Envelopes Paradox

> 来源：[http://falkenblog.blogspot.com/2009/09/physicists-solve-two-envelopes-paradox.html#0001-01-01](http://falkenblog.blogspot.com/2009/09/physicists-solve-two-envelopes-paradox.html#0001-01-01)

I was reading about a

[new solution](http://www.physorg.com/news169811689.html)

to the two-envelope problem over at some science/physics website:

> Researchers from Australia have taken a step toward resolving a seemingly simple yet unsolved paradox known as the "two-envelope" problem. They’ve worked out a new strategy that can enable a player to beat the game in terms of increasing their payoff. The strategy could have applications in optimizing gains in investments and other areas...The researchers explained that the strategy emerges from recent advances in two-state switching phenomena that are emerging in the fields of physics, engineering, and economics.

Hmmm. Everyone can be make better off in a two-person, zero sum exchange? Please tell. I think the paradox comes from not looking at the true state space. It is funny to think these guys think they figured out how to get blood out of stone via 'emerging fields of physics, engineering and economics'. Asserting the solution they do is like asserting a mixed strategy is dominant for the

[Monty Hall problem](http://en.wikipedia.org/wiki/Monty_Hall_problem)

. I think they get results via jerry-rigged simulations with particular

a priori

payoff distributions.

The problem is simple to state:

> In the two-envelope paradox, a player must choose between two envelopes, one of which contains twice as much money as the other. The player can open the envelope they choose, and then they have the option of switching envelopes. The other envelope, of course, has either twice the money or half the money as the first envelope, but the player does not know which

It may seem that given an amount $X in your envelope, switching generates 0.5*2*X+0.5*0.5*X=1.25*X, which is 0.25 times more than the $X you have. But if they both apply such logic, how can that be rational, they both have the same expected, positive return in a zero-sum game (one's gain is the other's loss)?

There are

[many known solutions](http://en.wikipedia.org/wiki/Two_envelopes_problem)

to this problem, some of which are inconsistent, but I think the simplest is as follows.

You might think you have $X in your envelope, and can trade to $2X or $0.5*X, giving you a gain of New Envelope minus value of Current Envelope, or 0.5*($2X+$0.5X)-$X, or +$0.25X. However, you must consider, symmetrically, you are the 'other guy', and so your envelope contains the $2X or the $0.5X. In that case, your expected gain is the opposite, trading gives you a new envelope with $X, giving up the random 0.5*($2X+$0.5X), generating an expected loss of $X-0.5*($2X+$0.5X), or -$0.25X. As you are either in the first or second case with equal probability, the expected value is zero, 0.5*(+$0.25X-$0.25*X).

The seeming paradox comes from thinking

you

have the envelop with the $X that is either doubled or halved, ignoring the chance you could be the one who starts out with $2X or $0.5X. If one player has $X, you have a 50% chance of being that guy, a 25% chance of having 0.5*X and a 25% chance of having the 2X. When you look in your envelope, and see $10, you can't assume X=$10\. It could be that X=$20 or $5, conditional upon seeing $10 in your envelope. Weighting everything probabilistically leads to no increase in value from exchange.