<!--yml
category: 未分类
date: 2024-05-18 13:49:53
-->

# Optimal Equity Monetization | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/07/30/optimal-equity-monetization/#0001-01-01](https://quantivity.wordpress.com/2011/07/30/optimal-equity-monetization/#0001-01-01)

A reader recently asked an interesting question regarding *equity monetization*, most frequently associated with [10b5-1](http://en.wikipedia.org/wiki/SEC_Rule_10b5-1) (closely related to previous post on [Employee Stock Option Hedging](https://quantivity.wordpress.com/2010/11/28/employee-stock-option-eso-hedging)):

> What is the right way to model the monetization of a large concentrated equity position, including tax considerations?

This is a fun topic to demystify, as many financial advisers struggle to explain the answer in rigorous terms, often use grossly oversimplified assumptions (*e.g.* linear price change on underlying), and almost never provide analytic or code models. Towards this end, this post builds such an analytic model and walks through some (but *not* all) of the corresponding considerations.

Conceptually, the liquidation model is fairly simple:

   profit = (realized gain) – (exercise price) – (tax liability)

In other words, profit ![\pi ](img/595a968a94f661a66cf16bd05b5771b3.png) is the sum of the realized proceeds from equity liquidation, minus any exercise price (applicable to options, not RSUs), minus the corresponding tax liability. Of course, concentrated positions must be liquidated gradually to minimize *market impact*. Thus, the model extends over an ![i](img/6aed483d693a0743f647c27ec4372c2a.png)-period liquidation schedule (hopefully not front-run too badly by the counterparty):

   ![\pi = \sum\limits_i \left( g_i - e_i - t_i \right) ](img/e38bf01cf881784ca0c99ebdc5116cf3.png)

Where ![g_i](img/516501b92511125f84525f27f1b93b6f.png) is the gain in period ![i](img/6aed483d693a0743f647c27ec4372c2a.png), ![e_i](img/c40aada96b6f9e93a0c4d104cb144761.png) is the exercise cost in period ![i](img/6aed483d693a0743f647c27ec4372c2a.png), and ![t_i](img/696dde9329f2f0772faee015e6c7ee40.png) is the tax liability in period ![i](img/6aed483d693a0743f647c27ec4372c2a.png). Each of these can be subsequently defined as:

   ![g_i = q_i \times p_i ](img/9deb7663104c31e42a6273b514210b87.png)
   ![e_i = q_i \times c_i ](img/10609fcc1647770bd9e2d82256c54e02.png)
   ![t_i = \hat t (g_i) ](img/a2a30fe16b211aed5cf8bef7a8a7f4e7.png)

Where ![q_i](img/6df37a73ab6b36be431927e481053710.png) is the quantity of shares sold in period ![i](img/6aed483d693a0743f647c27ec4372c2a.png), ![p_i](img/cf77e53f898b49e52240e8ba57932b24.png) is the *average* price per share of the shares sold in period ![i](img/6aed483d693a0743f647c27ec4372c2a.png), ![c_i](img/938afe5cb02db372c36203e82340f7c6.png) is the *average* exercise cost of the shares sold in period ![i](img/6aed483d693a0743f647c27ec4372c2a.png), and ![\hat t ](img/08b7621fabd99ce0a01fa79da7c76bcd.png) is a non-trivial function for calculating the tax liability based upon the period gain during the tax year corresponding to period ![i](img/6aed483d693a0743f647c27ec4372c2a.png). Substituting back, the model becomes:

   ![\pi = \sum\limits_i \left[ (q_i \times p_i) - (q_i \times c_i) - \hat t (q_i, p_i) \right] ](img/7497d17786a1b09f5aaa86d2cc50783d.png)

Which simplifies to:

   ![\pi = \sum\limits_i \left[ (q_i \times (p_i - c_i)) - \hat t (q_i, p_i) \right] ](img/1fab9959894ea7e0abeb7119ec18d24b.png)

To begin, both ![c_i](img/938afe5cb02db372c36203e82340f7c6.png) and ![\hat t ()](img/e1b0363060cc3881064ffea37fa31246.png) are taken as given in this model; the former because it is known in advance (either zero for RSUs or fixed exercise price for ISO / NQOs) and the latter because it is formulaic and rarely effects the liquidation schedule *in basic models*.

This leaves three free variables: ![i](img/6aed483d693a0743f647c27ec4372c2a.png), ![q_i](img/6df37a73ab6b36be431927e481053710.png), and ![p_i](img/cf77e53f898b49e52240e8ba57932b24.png). Thus, the model all boils down to a single discretionary variable q (whose cardinality implies the value of ![i](img/6aed483d693a0743f647c27ec4372c2a.png)), whose value is chosen based upon a non-discretionary variable decided by the almighty market (![p_i](img/cf77e53f898b49e52240e8ba57932b24.png)). Of course, the ![q_i](img/6df37a73ab6b36be431927e481053710.png) are subject to one or more bounds.

First bound is the total number of shares ![\hat q ](img/0e97d4897e028a363cf95f548632e2d3.png) available for monetization:

   ![\sum\limits_i q_i = \hat q](img/163858fbb242feeed61fd1d469c74626.png)

For shares subject to vesting schedule of ![j](img/a6e466d0abe474abc54eedb751aa882e.png) periods, the number of shares to be monetized in each period is lower bounded by zero and upper bounded by the vesting of shares in previous periods ![j](img/a6e466d0abe474abc54eedb751aa882e.png) (where ![j \le i)](img/5db936791e0285d62094b3f171c87a13.png):

   ![\forall i : 0 \leq q_i \leq \left( \sum\limits_{j=1}^i v_j - \sum\limits_{j=1}^{i-1} q_j \right) ](img/4e01ba25d78c00a81d465c5d817eef0a.png)

In other words, the maximum number of shares to be monetized in period ![i](img/6aed483d693a0743f647c27ec4372c2a.png) is equal to the number of shares which have vested in the ![j](img/a6e466d0abe474abc54eedb751aa882e.png) periods up to and including ![i](img/6aed483d693a0743f647c27ec4372c2a.png), less the number of shares which have been sold in previous periods ![1, ... , (i-1) ](img/b0e269f59f5dcd5843a461f917218e6c.png).

Coming full circle, the objective of equity monetization is to maximize profit from liquidated shares:

    ![\text{max} \hspace{2 mm} \pi](img/469d3c049d6e0e1f2eef94663baefdce.png)

Which leads to an *optimal equity monetization model*:

![\begin{aligned}  \underset{q_i}{\text{max}}  &\sum\limits_i [(q_i \times (p_i - c_i)) - \hat t (q_i, p_i)] \\  \text{subject to}  & \sum_i{q_i} = \hat q, \\  & \forall i : 0 \leq q_i \leq \left( \sum\limits_{j=1}^i v_j - \sum\limits_{j=1}^{i-1} q_j \right)  \end{aligned} ](img/ff3cd85d82af3e18c07acbf58d3aec49.png)

Whose solution boils down to a prediction of all ![p_i](img/cf77e53f898b49e52240e8ba57932b24.png), wherein lies the fun. Depending on reader interest, subsequent posts may consider solution to this model, including additional wrinkles such as hedges and OTC [exotics](http://en.wikipedia.org/wiki/Exotic_option).