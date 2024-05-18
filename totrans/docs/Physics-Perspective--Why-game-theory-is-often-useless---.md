<!--yml
category: 未分类
date: 2024-05-18 07:04:04
-->

# Physics Perspective: Why game theory is often useless...

> 来源：[http://physicsoffinance.blogspot.com/2011/10/why-game-theory-is-often-useless.html#0001-01-01](http://physicsoffinance.blogspot.com/2011/10/why-game-theory-is-often-useless.html#0001-01-01)

Economic theory relies very heavily on the notion of equilibrium. This is true in any model for competitive equilibrium -- exploring how exchange can in principle lead to an optimal allocation of resources -- or more generally in the context of game theory, which explores stable Nash equilibria in strategic games.

One thing physicists find wholly unsatisfying about equilibrium in either case is economists' near total neglect of the crucial problem of whether the agents in such models might ever plausibly

*find*

an equilibrium. You can assume perfectly rational agents and prove the existence of an equilibrium, but this may be an irrelevant mathematical exercise. Realistic agents with finite reasoning powers might never be able to learn their way to such a solution.

More likely, at least in many cases, is that less-than-perfectly rational agents, even if they're quite clever at learning, may never find their way to a neat Nash equilibrium solution, but instead go on changing and adapting and responding to one another in a way that leads to ongoing chaos. Naively, this would seem especially likely in any situation -- think financial markets, or any economy as a whole -- in which the number of possible strategies is enormous and it is simply impossible to "solve the problem" of what to do through perfect rational reflection (no one plays chess by working out the Nash equilibrium).

A brilliant illustration of this insight comes in

[a new paper](http://arxiv.org/PS_cache/arxiv/pdf/1109/1109.4250v1.pdf)

by Tobias Galla and Doyne Farmer. This is the first study I've seen (though there may well be others) which addresses this matter of the relevance of equilibrium in complex, high-dimensional games in a  generic way. The conclusion is as important as it is intuitively reasonable:

> Here we show that if the players use a standard approach to learning, for complicated games there is a large parameter regime in which one should expect complex dynamics. By this we mean that the players never converge to a fixed strategy. Instead their strategies continually vary as each player responds to past conditions and attempts to do better than the other players. The trajectories in the strategy space display high-dimensional chaos, suggesting that for most intents and purposes the behavior is essentially random, and the future evolution is inherently unpredictable.

In other words, in games of sufficient complexity, the insights coming from equilibrium analyses just don't tell you much. If the agents learn in a plausible way, they never find any equilibrium at all, and the evolution of strategic behaviours simply carries on indefinitely. The system remains out of equilibrium.

A little more detail. Their basic approach is to consider general two player games between, say, Alice and Bob. Let each of the two players have N possible strategies to choose from. The payoff matrices for any such game are NxN matrice (one for each player) giving the payoffs they get for each pair of strategies being played. The cute idea in this analysis is to choose the game randomly by selecting the elements of the payoff matrices for both Alice and Bob from a normal distribution centered on zero. The authors simply choose a game and simulate play as the two players learn through experience -- playing strategies from their repertoire of N possibilities more frequently if those strategies give good results.

With N = 50, the results show clearly that many games do not ever settle into any kind of stable behaviour. Rather, no equilibrium is ever found. The typical dynamics is reflected in the figure below, which shows the difference in payoffs to the two players (Alice's - Bob's) over time. Even though the two agents work hard to learn the optimal strategies, the complexity of the game prevents their success, and the game shows no signs whatsoever of settling down:

[![](img/4507da64a6571a0ed4fd135fd31e8d42.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhbT4z12BUjqXYlAhvu4YXxDKxT4Uaz8aQeDa5pOBOOrB6GEgytyDe4gXJKstaBY3XBHLRKMsd9MPElJZatiM67QiA0ANkW11tRMzGinClIUlu4Aj9CLl6MZuEJUBJ09tDfEbEJiv9q_yO8/s1600/galla_farmer_fig.png)

As the authors note, this kind of rich, complex, ongoing dynamics looks quite similar to what one sees in real systems such as financial markets (the time series above exhibits clustered volatility, as do market fluctuations). There are periods of relative calm punctured by bouts of extreme volatility. Yet there's nothing intervening here -- no "shocks" to the system -- which would create these changes. It all comes from perfectly natural internal dynamics. And this is in a game with N = 50 strategies. It seems likely things will only grow more chaotic and less likely to settle down if N is larger than 50, as in the real world, or if the number of players grows beyond two.

Hence, I see this as a rather profound demonstration of the likely irrelevance of equilibrium analyses coming from game theory to complex real world settings. Dynamics really matters and cannot be theorized out of existence, however hard economists may try. As the paper concludes:

> Our results suggest that under many circumstances it is more useful to abandon the tools of classic game theory in favor of those of dynamical systems. It also suggests that many behaviors that have attracted considerable interest, such as clustered volatility in nancial markets, may simply be specific examples of a highly generic phenomenon, and should be expected to occur in a wide variety of different situations.