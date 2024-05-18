<!--yml
category: 未分类
date: 2024-05-18 13:52:58
-->

# Employee Stock Option (ESO) Hedging | Quantivity

> 来源：[https://quantivity.wordpress.com/2010/11/28/employee-stock-option-eso-hedging/#0001-01-01](https://quantivity.wordpress.com/2010/11/28/employee-stock-option-eso-hedging/#0001-01-01)

Utility of quantitative finance often arises in unexpected places. An example is employee stock options (ESO). Specifically, a surprising number of ESO planning questions boil down to dynamic hedging and its relationship to financial, tax, and/or regulatory considerations.

As always, the two questions for ESOs are: *when to exercise and when to sell* (including potential for multiple partials of each), and *what quantities for each*.

Consider the following scenario: employee is granted ![n](img/4f0c9881324df3a61e8d3cc580ec06e6.png) options on underlying ![u](img/3e3dc85b695f49b6073b5656627101bb.png) at strike ![s](img/e73c5c00df00f12d725a7df478e44982.png) at time ![t](img/867074ff782cf54112401c2854672245.png), vesting ratably by month after a 12 month cliff. Without loss of generality, this scenario also is applicable to multiple ESO grants. To make the analysis more fun, consider the following common complexities:

*   Non-tradeable: assume the underlying ![u](img/3e3dc85b695f49b6073b5656627101bb.png) cannot be exchange-traded (and similarly no exchange-traded derivatives exist), either because they are not listed, such activity is contractually restricted (either directly or pledged), or the employee is subject to regulatory restriction(s)
*   Mix of qualification: assume options are a mix of qualified (ISO) and non-qualified (NQO), arising from [IRC § 422(d)](http://www.taxalmanac.org/index.php/Internal_Revenue_Code:Sec._422._Incentive_stock_options) limitation
*   Exchange-traded only: assume employee may only use exchange-traded instruments, and thus does not have access to institutional vehicles such as [VPFs](http://en.wikipedia.org/wiki/Variable_prepaid_forward_contract) or [NPCs](http://en.wikipedia.org/wiki/Notional_principal_contract) (see [Anschutz v Comm](http://www.ustaxcourt.gov/InOpHistoric/Anschutz.TC.WPD.pdf))
*   Underlying upside: assume underlying exhibits significant price volatility, including potential for significant increase

Assume further the United States is domicile for the employee, and thus is subject to compliance with the following regulatory and tax considerations:

*   [Constructive (wash) sale](http://en.wikipedia.org/wiki/Wash_sale): cannot sell a security at a loss and repurchase the same or substantially identical stock within predefined period, per IRC [§ 1091](http://www.taxalmanac.org/index.php/Internal_Revenue_Code:Sec._1092._Straddles) and [§ 1259](http://www.taxalmanac.org/index.php/Sec._1259), without resulting in constructive sale and disallowance of deduction
*   [Short swing rule](http://en.wikipedia.org/wiki/Short_swing): prevent profit taking with respect to trading company’s stock during 6 month period, per SEA 1934 16(b), for selected stockholders individuals (officers, directors, and 10% holders)
*   60/40 tax treatment: trades of “broad-based” instruments, as defined by [IRC § 1256(a)(3)](http://www.law.cornell.edu/uscode/uscode26/usc_sec_26_00001256----000-.html), are subject to 60/40 mix of long/short-term capital gains taxes (see [IRS 550](http://www.irs.gov/pub/irs-pdf/p550.pdf))
*   Straddle rule: liquidation of loss on offsetting positions may only be reported to the extent that it is greater than the unrecognized gain of the offsetting position, per [IRC § 1092](http://www.taxalmanac.org/index.php/Internal_Revenue_Code:Sec._1092._Straddles), excepting identified straddles and qualified covered calls
*   Hedging transactions: transactions undertaken in the normal course of trade or business primarily to manage risk, including price changes on ordinary obligations, per [IRC § 1221](http://www.law.cornell.edu/uscode/26/usc_sec_26_00001221----000-.html)
*   IRA contribution limits: annual contribution to IRA is limited based upon adjusted gross income, per [IRC § 25b](http://www.taxalmanac.org/index.php/Internal_Revenue_Code:Sec._25B._Elective_deferrals_and_IRA_contributions_by_certain_individuals)

Given this setup, readers are encouraged to consider their answers to the questions posed above (or, read primers from either [Thomas](http://www.fairmark.com/books/consider.htm), [Olagues](http://www.amazon.com/Getting-Started-Employee-Stock-Options/dp/0470471921/ref=ntt_at_ep_dpi_1), or [Gray](http://www.amazon.com/Employee-Stock-Options-Executive-Planning/dp/0979443814/ref=sr_1_1?ie=UTF8&s=books&qid=1291001574&sr=8-1)). A subsequent post will focus on dynamic hedging in this context, with an eye towards tax minimization.