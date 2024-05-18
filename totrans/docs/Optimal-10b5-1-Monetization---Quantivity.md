<!--yml
category: 未分类
date: 2024-05-18 13:48:43
-->

# Optimal 10b5-1 Monetization | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/09/27/optimal-10b51-equity-monetization/#0001-01-01](https://quantivity.wordpress.com/2011/09/27/optimal-10b51-equity-monetization/#0001-01-01)

Increased IPO deal flow is motivating readers to privately inquire about *practical algos* for compliant [10b5-1](http://en.wikipedia.org/wiki/SEC_Rule_10b5-1) equity / ESO / RSU monetization plans, prompted by the recent three-post theoretical series on [Optimal Equity Monetization](https://quantivity.wordpress.com/2011/07/30/optimal-equity-monetization/). This topic is worth exploring for several reasons, prefaced by usual disclaimer of being provided for informational purposes only:

*   *Microcosm*: this topic is a microcosm of trading, as it encapsulates many common problems
*   *Importance*: choice of plan is arguably the single most influential lifetime financial decision
*   *Real life quant*: illustrative example of theory bumping into the vagaries of the financial services industry for retail investors
*   *Greenfield*: literature on this topic is minimal and disconnected from practical reality
*   *Exotic*: illustrative example of arguably the most prevalent [retail exotic](https://quantivity.wordpress.com/2009/09/17/coming-of-retail-exotics)

This topic will be explored via a new *10b5-1 plan monetization model*, compliant with SEC regs and compatible with common practical restrictions imposed by broker counterparties. This model and corresponding background will be presented in parts over several posts, given its non-trivial scope.

This first post begins by motivating the model via intuition, followed by a brief review of the existing literature. A second post will describe the model, provide practical R code, and generate results by applying it to a representative equity. For those familiar with portfolio optimization, this model is reminiscent of [Black-Litterman](http://en.wikipedia.org/wiki/Black%E2%80%93Litterman_model) as it depends upon “views” of the underlying stock.

**Stopping Criteria**

Intuitively, optimality of a plan can be measured by the *deviation in P&L of trades between plan and absence of a plan*. In other words, the benchmark for evaluating a plan is what would happen if the holder was not subject to a plan. This makes sense, as a plan effectively serves as a trading constraint (a *portfolio constraint*, of sorts), as the execution rule(s) for all trades must be specified in advance.

One simplistic approach is prediction: guess the evolution of the stock price and build a plan which maximizes corresponding profit. This approach is sufficient for only one class of holders: those who believe the stock is going to crash; for them, the plan is easy: sell as much, as fast, as possible at market prices.

For everyone else, the prediction approach is fairly naïve: given an infinite number of potential stock price paths, what justifies choice of one? In absence of precognition, an alternative choice is to use [optimal stopping](http://en.wikipedia.org/wiki/Optimal_stopping) and [optimal control](http://en.wikipedia.org/wiki/Optimal_control) (see Ferguson’s [Optimal Stopping and Applications](http://www.math.ucla.edu/~tom/Stopping/Contents.html), for a concise theoretical introduction).

Namely, *model the stock price as a stochastic process and express the problem as optimal stopping for each share to be monetized along that process*. Although not necessarily a [martingale](http://en.wikipedia.org/wiki/Martingale_%28probability_theory%29), this process can be assumed one given the holder must decide on plan prior to observing any realizations of the process. Also, this model is defined on real probability measure ![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png) (not risk-neutral ![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png)), as the market faced by the holder is *incomplete* due to legal constraints on short selling and trading derivatives.

Before diving into math and code, let’s begin by positing the attributes which an optimal plan algo should possess:

*   *Executable*: counterparties must be willing to execute plan
*   *Profit maximizing*: maximize monetization profit
*   *Time minimizing*: minimize duration of time to monetize
*   *Flexible risk*: able to adapt monetization to varying risk tolerance
*   *Dynamic*: optimal over a range of time, not just at plan initiation
*   *Adaptive*: adjusts monetization adaptively based upon prevailing market conditions
*   *Utility-free*: not depend upon unobservable utility functions

While perhaps obvious sounding, finding models which satisfy these attributes is surprisingly challenging. In fact, the literature is absent a model which possesses them all.

**Practical Literature Survey**

As the intent of this model is *practical implementation*, review of the literature will be through a pragmatic lens. In short, the literature is thin, devoid of practical examples, and written by well-intended academics clearly unfamiliar with the realities of monetization. From [People of Quant Research](https://quantivity.wordpress.com/2011/03/06/people-of-quant-research/), the only two academics whose primary research focus includes executive stock options are [Henderson](http://www.oxford-man.ox.ac.uk/people/members_henderson.html) and [Carpenter](http://people.stern.nyu.edu/jcarpen0/); from the accounting world, [Jagolinzer](http://leeds-faculty.colorado.edu/alja4277/10b5_1.html) is also doing good work (please comment, if you know of others).

A bit of historical context is useful: prior to 2000, researching the widespread practice of monetization was nearly impossible because nobody wanted to talk due to concern of insufficient affirmative defense against insider trading. Thus, monetization practice fell into two camps: the masses traded idiosyncratically in open windows and more sophisticated folks with sufficient notional executed OTC strategies (primarily [PVFs](http://en.wikipedia.org/wiki/Variable_prepaid_forward_contract) and [ZCCs](http://en.wikipedia.org/wiki/Collar_%28finance%29)). This changed in 2000, with the enactment of [10b5-1](http://en.wikipedia.org/wiki/SEC_Rule_10b5-1) providing affirmative defense for trades conducted via *mechanical* plan specified in advance. Hence the modern era of monetization began, with obvious alignment to quant finance and algorithmic trading.

More than a decade later, the literature is finally beginning to consider the *stylized facts of monetization* (*e.g.* apparently suboptimal option exercise, cross-hedging, contractual obligations, termination risk, block exercise, and broker constraints / costs). For example, [Leung](http://www.ieor.columbia.edu/fac-bios/leung/faculty.html) is the first to do a decent job surveying a few stylized facts in his 2011 article [Employee Stock Options: Accounting for Optimal Hedging, Suboptimal Exercises, and Contractual Restrictions](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1290404). Other articles attempting to scratch this surface, in decreasing order of insight:

*   [The Early Exercise of Executive Stock Options and Firms Future Systematic and Idiosyncratic Risks](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1466246), by Srivastava (2011)
*   [Accounting for Risk Aversion, Vesting, Job Termination Risk and Multiple Exercises in Valuation of Employee Stock Options](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=943926), by Leung and Sircar (2009)
*   [Estimation of Employee Stock Option Exercise Rates and Firm Cost](http://pages.stern.nyu.edu/~jcarpen0/pdfs/CarpenterStantonWallace2.pdf), by Carpenter, Stanton, and Wallace (2011)
*   [Optimal Exercise of Executive Stock Options and Implications for Firm Cost](http://people.stern.nyu.edu/jcarpen0/pdfs/CarpenterStantonWallace1.pdf), by Carpenter, Stanton, and Wallace (2010)
*   [Risk Aversion and Block Exercise of Executive Stock Options](http://ideas.repec.org/a/eee/dyncon/v33y2009i1p109-127.html), by Grasselli and Henderson (2009)
*   [Employee Stock Option Exercises: An Empirical Analysis](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=6072), by Huddart and Lang (1996)
*   [The Influence of Risk Diversification on the Early Exercise of Employee Stock Options by Executive Officers](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=294900), by Hemmer, Shevlin, and Matsunaga (1996)
*   [The Exercise and Valuation of Executive Stock Options](http://people.stern.nyu.edu/jcarpen0/pdfs/Carpenter1998.pdf), by Carpenter (1998)

In parallel with investigating stylized facts, an important theoretical insight was made: *optimal stopping theory could be applied to modeling stock option exercise* (and thus monetization, at large). Undoubtedly by accident, folks stumbled on the math that *precisely* describes the mental models of “normal” folks seeking to monetize; classic ![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png) thinking (as individualist duration plays no role in ![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png)).

This insight is captured in numerous papers by Leung, Henderson (working with [Hobson](http://www2.warwick.ac.uk/fac/sci/statistics/staff/academic-research/hobson/)), and Carpenter. Perhaps not coincidentally, Leung is from industrial engineering (apparently folks from finance and operations research do occasionally talk). While these papers provide some insight, their fundamental practical flaw is heavy implicit reliance on utility functions (albeit nicely exercising [prospect theory](http://en.wikipedia.org/wiki/Prospect_theory)), and thus formalization to the point of practical uselessness:

Yet, while adopting an optimal stopping model, these articles quickly derive results which conflict with the intuition of many “normal” folks. For example, from Henderson and Hobson (2011), p. 2:

> Optimal exercise strategy is of threshold form – the agent should exercise options the first time the asset price reaches a barrier level which depends on that part of the portfolio which has not yet been exercised. Just enough options are exercised to keep the portfolio holdings below the barrier, and thus the solution is a singular control.

Which arguably begs the question, by *assuming* a barrier threshold trigger model. Even less practical is the assumption of time homogeneity (p. 8), and thus time independence (p. 7):

> Is optimal not to exercise options at a given price level, then provided no options have been exercised in any intervening period, it will still be optimal to not exercise the options if the price returns to this level.

This obviously makes no sense in practice, as it admits solutions for which options may remain unmonetized forever (*i.e.* those above the threshold). More practical, time homogeneity should be *[endogeneous](http://en.wikipedia.org/wiki/Endogenous)*: the temporal equivalence of preference is determined by individual risk aversion. Folks with low risk tolerance will seek to monetize immediately upon price reaching a threshold (or even, at the extreme, monetize irrespective of thresholds). In contrast, folks with higher risk tolerance may prefer to monetize a percentage and then wait a variable duration of time to see how the price evolves.

The preceding optimal control insight builds upon a small, but nonetheless interesting, thread of probability theory represented by the following articles:

Finally, the following articles recognize monetization is *not necessarily a one-period problem* and thus introduce multiple stopping time:

Yet, despite all this wonderful literature, an effective practical model for monetization has yet to appear.