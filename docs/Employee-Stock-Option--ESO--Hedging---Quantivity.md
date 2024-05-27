<!--yml

类别：未分类

日期：2024-05-18 13:52:58

-->

# 员工股票期权（ESO）套期保值 | 量化投资

> 来源：[`quantivity.wordpress.com/2010/11/28/employee-stock-option-eso-hedging/#0001-01-01`](https://quantivity.wordpress.com/2010/11/28/employee-stock-option-eso-hedging/#0001-01-01)

量化金融的实用性常常出人意料。一个例子是员工股票期权（ESO）。具体而言，许多 ESO 规划问题归结为动态套期保值及其与财务、税务和/或监管考虑的关系，这令人惊讶。

与 ESO 相关的两个问题始终是：*何时行使和何时出售*（包括可能进行多次部分行使），以及*每种情况下的数量*。

考虑以下情景：员工在时间![t](img/867074ff782cf54112401c2854672245.png)，以每月 12 个月悬崖后按比例分配授予底层![u](img/3e3dc85b695f49b6073b5656627101bb.png)的![n](img/4f0c9881324df3a61e8d3cc580ec06e6.png)期权，行使价格为![s](img/e73c5c00df00f12d725a7df478e44982.png)。不失一般性，该情景也适用于多个 ESO 授予。为了使分析更有趣，考虑以下常见复杂性：

+   不可交易：假设底层的![u](img/3e3dc85b695f49b6073b5656627101bb.png)无法交易所交易（同样不存在交易所交易的衍生品），要么是因为它们未上市，此类活动受到合约限制（直接或已抵押），要么员工受到监管限制

+   资格混合：假设期权是合格（ISO）和非合格（NQO）的混合，源于[IRC § 422(d)](http://www.taxalmanac.org/index.php/Internal_Revenue_Code:Sec._422._Incentive_stock_options)的限制

+   仅限交易所交易：假设员工只能使用交易所交易的工具，因此无法使用机构工具，如[VPFs](http://en.wikipedia.org/wiki/Variable_prepaid_forward_contract)或[NPCs](http://en.wikipedia.org/wiki/Notional_principal_contract)（请参阅[Anschutz v Comm](http://www.ustaxcourt.gov/InOpHistoric/Anschutz.TC.WPD.pdf)）

+   底层上涨：假设底层具有显著的价格波动，包括潜在的大幅上涨

进一步假设美国是员工的住所国，因此必须遵守以下监管和税务考虑：

+   [建设性（洗牌）交易](http://en.wikipedia.org/wiki/Wash_sale)：不得以亏损出售证券并在预定期内重新购买相同或实质相同的股票，根据 IRC [§ 1091](http://www.taxalmanac.org/index.php/Internal_Revenue_Code:Sec._1092._Straddles)和[§ 1259](http://www.taxalmanac.org/index.php/Sec._1259)，否则会导致建设性销售和不允许扣除

+   [短线交易规则](http://en.wikipedia.org/wiki/Short_swing)：在 6 个月的时间段内，防止交易公司股票的利润提取，参见 SEA 1934 16(b)，适用于选定的股东个人（高管、董事和 10%股东）

+   60/40 税收处理：根据[IRC § 1256(a)(3)](http://www.law.cornell.edu/uscode/uscode26/usc_sec_26_00001256----000-.html)的定义，对“广泛基准”的工具进行交易，应纳税 60/40 长期/短期资本利得税（参见[IRS 550](http://www.irs.gov/pub/irs-pdf/p550.pdf)）

+   交叉持仓规则：只有当对冲头寸的未实现损失大于对冲头寸的未实现收益时，才可以报告对冲头寸的损失清算，参见[IRC § 1092](http://www.taxalmanac.org/index.php/Internal_Revenue_Code:Sec._1092._Straddles)，但排除了确定的对冲头寸和合格的备用认购

+   对冲交易：在正常的贸易或业务过程中进行的交易，主要是为了管理风险，包括普通债务的价格变动，参见[IRC § 1221](http://www.law.cornell.edu/uscode/26/usc_sec_26_00001221----000-.html)

+   IRA（个人退休账户）的缴纳限额：根据调整后的总收入，年度对 IRA 的缴纳是有限制的，参见[IRC § 25b](http://www.taxalmanac.org/index.php/Internal_Revenue_Code:Sec._25B._Elective_deferrals_and_IRA_contributions_by_certain_individuals)

鉴于这种设置，鼓励读者考虑他们对上述问题的回答（或者阅读[Thomas](http://www.fairmark.com/books/consider.htm)、[Olagues](http://www.amazon.com/Getting-Started-Employee-Stock-Options/dp/0470471921/ref=ntt_at_ep_dpi_1)或[Gray](http://www.amazon.com/Employee-Stock-Options-Executive-Planning/dp/0979443814/ref=sr_1_1?ie=UTF8&s=books&qid=1291001574&sr=8-1)的入门读物）。随后的一篇文章将关注于在这一背景下的动态对冲，着眼于税收最小化。
