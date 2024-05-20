<!--yml
category: 未分类
date: 2024-05-18 13:49:33
-->

# Optimal Equity Monetization: Part 2 | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/07/31/optimal-equity-monetization-part-2/#0001-01-01](https://quantivity.wordpress.com/2011/07/31/optimal-equity-monetization-part-2/#0001-01-01)

The previous post [Optimal Equity Monetization](https://quantivity.wordpress.com/2011/07/30/optimal-equity-monetization) introduced a mathematical model for optimizing equity monetization. In this follow-up post, we consider several solutions to that model under naïve assumptions about the dynamics of ![p_i](img/cf77e53f898b49e52240e8ba57932b24.png).

Begin by making the (unrealistic) assumption that the distribution of values for ![p_i](img/cf77e53f898b49e52240e8ba57932b24.png) is both known and deterministic. Given that, consider two scenarios for ![p_i](img/cf77e53f898b49e52240e8ba57932b24.png) dynamics that admit simple analytic solutions: monotonic first differences and flat. Collar overlays are considered for non-zero vesting. These solutions are notable as they hold true irrespective of the relative value of ![p_i](img/cf77e53f898b49e52240e8ba57932b24.png).

**Monotonic First Differences**

Consider when all first differences of p are either monotonically increasing or monotonically decreasing; in other words:

   ![\forall i : \Delta p_i < 0 \hspace{2 mm} \text{or} \hspace{2 mm} \Delta p_i > 0](img/a28985bb1a2295b0b08cbb701acb34c7.png)

where:

   ![\Delta p_i = \left( p_i - p_{i-1} \right) ](img/f5de57c8c1346f87fcccc5ce200f774f.png)

In other words, the price of the underlying is either increasing or decreasing consistently *every* period.

For monotonically decreasing ![\Delta p_i ](img/aae7efaf4404d6dd35df18b104264313.png), the solution is selling shares immediately as they vest:

   ![\forall i : q_i = v_i ](img/537f99a9d9cd022a25abd69b0c7d5fef.png)

If there is no vesting, then the solution simplifies to selling all shares in the first period:

   ![q_i = \begin{cases}  \sum\limits_j v_j & \text{if } 1\\  0 & \text{if } 1 < i \leq n  \end{cases} ](img/26929f1d90b24a4011da0182d679a3a0.png)

For monotonically increasing ![\Delta p_i ](img/aae7efaf4404d6dd35df18b104264313.png), the solution is to hold as long as possible and sell in the final period:

   ![q_i = \begin{cases}  0 & \text{if } 1 \leq i < n \\  \sum\limits_j v_j & \text{if } i = n  \end{cases} ](img/18affe03ec84f7eb0edea69d93a0da48.png)

Sadly, this scenario is rarely reality. Yet, from these two scenarios we can consider more realistic generalizations.

**Collared**

Consider again when ![p_i](img/cf77e53f898b49e52240e8ba57932b24.png) is monotonically decreasing with *non-zero* vesting. As exemplified by the zero vesting case, the optimal is selling all shares in the first period. Yet, non-zero vesting results in the inequity constraint for ![q_i](img/6df37a73ab6b36be431927e481053710.png) (see [Optimal Equity Monetization](https://quantivity.wordpress.com/2011/07/30/optimal-equity-monetization) for more details), and thus the inability to sell all shares in the first period. An obvious question to ask is how to relax this constraint in the presence of vesting.

As selling unvested shares is obviously not possible, use of options is a natural choice to replicate the equivalent cash flows. Specifically, one or more [collars](http://en.wikipedia.org/wiki/Collar_%28finance%29). Theoretical optimal solution matches cash flow: pairs each vesting period with a matching-expiry collar with equal size. For example, ![n](img/4f0c9881324df3a61e8d3cc580ec06e6.png) collars would be required to match ![n](img/4f0c9881324df3a61e8d3cc580ec06e6.png) months of vesting: expiry of collar 1 equal to period 1, expiry of collar 2 equal to period 2, *etc*.

A more simple alternative option strategy is to open a single collar with size equal to ![\hat q ](img/0e97d4897e028a363cf95f548632e2d3.png) during the first period, then decrease exposure each period by closing part of the collar. Size of the exposure decrease is equivalent to ![v_j](img/7286ac0c897ef30819e1c42a7bc0ec6c.png) shares in each period ![j](img/a6e466d0abe474abc54eedb751aa882e.png) (scaled by the options’ multiplier, obviously). While this more simple approach likely has lower transaction costs, it has [vega](http://en.wikipedia.org/wiki/Greeks_%28finance%29#Vega_.CE.BD) risk (due to option positions being closed prior to expiry). However, given comparatively lower theta decay exposure, cost to enter this position *could* also potentially be lower cost.

In both strategies, [European](http://en.wikipedia.org/wiki/Option_style#American_and_European_options) collars are usually preferred to [Americans](http://en.wikipedia.org/wiki/Option_style#American_and_European_options) for two reasons: eliminate assignment risk (on short call) and reduce cost.

Using this collared approach, the optimal equity monetization model simplifies to:

![\begin{aligned}  \underset{q_i}{\text{max}}  & \sum\limits_i [(q_i \times \gamma) - \hat t (q_i, p_1)] \\  \text{subject to}  & \sum_i{q_i} = \hat q  \end{aligned} ](img/e23100e4d8dad9546e44abf9ec216404.png)

where ![\gamma = (p_1 - c) ](img/403d1a710d5b648cec6a233f985bf4e9.png), which represents cash flow neutralization of downside risk in the underlying price throughout all periods, and ![p_1](img/065df3cc05be0da95f2cd751915fc985.png) is the price of underlying in period when collar is opened.

The solution is equal to selling shares as they vest, with corresponding offset in collar (either expiring or partially closing):

   ![\forall i : q_i = v_i ](img/537f99a9d9cd022a25abd69b0c7d5fef.png)

The corresponding profit, reduced by cost of the collar(s) ![\rho ](img/1ccd4b0fb7eabd84de1311cef8ae3f4c.png), is:

   ![\pi = \left( \sum\limits_i \left[ (q_i \times \gamma) - \hat t (q_i, p_1) \right] \right) - \rho ](img/d1e02169c70ca568c4797706e52c851d.png)

In other words, this model manifests a classic derivative tradeoff: guaranteed profit cashflow at the expense of a fixed one-time, upfront cost (*i.e.* ![\rho](img/3e72a82f16831a4135a859a809b7fe10.png)).

**Flat**

Price of the underlying trading flat over the entire period is the third simple scenario to consider; in other words:

   ![\forall i : \Delta p_i = 0 ](img/7a4848b82e4f53e720e89839eacd8124.png)

which is equivalent to:

   ![\forall i, j : p_1 = p_i = p_j ](img/2bac1fc7e01f4f983e970c792ae92284.png)

This equality expression is useful as it resembles the above collar approach, in which ![\gamma ](img/67d230c83502960645b847bcd66b2440.png) neutralized underlying price exposure (*i.e.* collar and underlying cash flows net to zero). Specifically, when the underlying price is known in advance to trade flat over all periods, the cash flow is equivalent to collaring (without requiring any options). Hence, the optimization model and solution remain the same as collar model:

   ![\forall i : q_i = v_i ](img/537f99a9d9cd022a25abd69b0c7d5fef.png)

Profit simplifies to the following, by eliminating the collar cost:

   ![\pi = \sum\limits_i \left[ (q_i \times \gamma) - \hat t (q_i, p_1) \right] ](img/c9c11f433f3163946533e803ecc08509.png)

Thus, flat profit is higher compared to collared profit in all cases, except when collar(s) are opened with credit premium (*i.e.* premium is positive, thus being paid to open the collar).