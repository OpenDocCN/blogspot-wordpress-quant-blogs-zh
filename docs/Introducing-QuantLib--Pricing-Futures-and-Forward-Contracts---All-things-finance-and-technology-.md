<!--yml

类别：未分类

日期：2024-05-18 06:46:55

-->

# 介绍 QuantLib：定价期货和远期合约 | 所有关于金融和科技的事物…

> 来源：[`mhittesdorf.wordpress.com/2013/04/02/introduction-to-quantlib-pricing-futures-and-forward-contracts/#0001-01-01`](https://mhittesdorf.wordpress.com/2013/04/02/introduction-to-quantlib-pricing-futures-and-forward-contracts/#0001-01-01)

在本系列关于 QuantLib 的安装中，我将向您展示如何定价固定利率债券的远期合约。远期合约要求买方在指定的未来时间点以特定的执行价格从远期合约的卖方那里购买基础资产，卖方同样有义务在约定的执行价格交付基础资产。在合约成立之初，执行价格被设定为预期未来基础资产的价值，关于如何计算这个价值，我们在本系列早些时候的帖子中已经学过。

期货合约是一种标准化的、交易所交易的远期合约，具有每日盯市。在本篇博文中，我们将假设期货和远期价格是等效的。对于可能导致期货和远期价格在现实世界中分离的细微差别，我建议您阅读约翰·赫尔的经典书籍《期权、期货和其他衍生品，第六版》的第五章。

要计算固定利率债券的远期合约的（执行）价格，这是一种具有已知、固定收入的资产，包括定期付息，使用以下公式，其中 K = 发行时的远期价格，S0 = 发行时基础资产的价格，I = 远期合约生命周期内收到任何收入的现值，r = 利率，T 是合约的期限：

K = (S0 – I)e^rT

随着时间推移以及/或利率在远期合约发行后变动，远期合约的价值会发生变化。要重新定价合约，可以使用以下公式，所有变量如前所定义：

F = S0 – I – Ke^-rT

以下是如何定价一个 15 个月期限的 3%固定利率债券的远期合约的 QuantLib 代码，该债券的面值为 100，每年支付 5%的票息。代码还展示了如何在利率水平上升或下降 1%的情况下重新估值远期合约。注意`[RelinkableHandle<YieldTermStructure>](http://quantlib.org/reference/class_quant_lib_1_1_relinkable_handle.html)`，这是一个强大的 QuantLib 编程结构，它允许一个新的、更新的收益率曲线“重新链接”到现有的远期合约，当调用`FixedRateBondForward::NPV()`方法时，远期合约会在更高的或更低的利率水平上重新定价自己。

```
#include <iostream>
#include <cstdlib>
#define BOOST_AUTO_TEST_MAIN
#include <boost/test/unit_test.hpp>
#include <boost/detail/lightweight_test.hpp>
#include <ql/quantlib.hpp>
#include <boost/math/distributions.hpp>
#include <vector>
#include <boost/function.hpp>
#include <boost/math/distributions.hpp>
#include <ql/instruments/bonds/fixedratebond.hpp> 
#include <ql/pricingengines/bond/bondfunctions.hpp>
#include <boost/format.hpp>
#include <ql/instruments/fixedratebondforward.hpp>
#include <ql/termstructures/yield/discountcurve.hpp>

using namespace QuantLib;

BOOST_AUTO_TEST_CASE(testCalculateForwardPriceOfFixedRateBond) {

Calendar calendar = UnitedStates(UnitedStates::GovernmentBond);
const Natural settlementDays = 1;
Date today = Date::todaysDate();
Date bondIssueDate = calendar.adjust(today, ModifiedFollowing);
Date bondMaturityDate = bondIssueDate + Period(3, Years);
Rate rate = .03;
Settings::instance().evaluationDate() = bondIssueDate;

//coupon schedule
std::vector coupons(1, .05);

//fixed rate bond
Real faceValue = 100.0;
boost::shared_ptr<FixedRateBond> fixedRateBondPtr(new FixedRateBond(settlementDays, calendar, 
faceValue, bondIssueDate, bondMaturityDate, Period(Annual), coupons, ActualActual(ActualActual::Bond)));
boost::shared_ptr<YieldTermStructure> flatForwardRates(new FlatForward(bondIssueDate,
rate, ActualActual(ActualActual::Bond), Compounded, Annual));
RelinkableHandle<YieldTermStructure> flatTermStructure(flatForwardRates);
boost::shared_ptr<PricingEngine> bondEngine(new DiscountingBondEngine(flatTermStructure));
fixedRateBondPtr->setPricingEngine(bondEngine);

//calculate bond price
Real bondPrice = fixedRateBondPtr->NPV();
std::cout << "Bond price: " << bondPrice << std::endl;

//print cash flows using C++ 11 range-based for loop
for (boost::shared_ptr<CashFlow> cashFlow : fixedRateBondPtr->cashflows()) {
     std::cout << boost::format("Cash flow: %s, %.2f") % cashFlow->date() % cashFlow->amount() << std::endl; 
}

//forward maturity tenor 
Date forwardMaturityDate = bondIssueDate + Period(15, Months); 
Natural daysToMaturityOfForwardContract = (forwardMaturityDate - bondIssueDate) - settlementDays;
std::cout << boost::format("Expiration of forward contract: %s") % forwardMaturityDate << std::endl;
std::cout << boost::format("Days to maturity of forward contract: %i") % daysToMaturityOfForwardContract << std::endl; 

//calculate strike price/future value of the bond using periodic, annual rate (not continuous) because this a bond		
Real income = (fixedRateBondPtr->nextCouponRate(bondIssueDate) * faceValue);
const Real strike = bondPrice * (1 + rate * daysToMaturityOfForwardContract/365) - income;  
std::cout << boost::format("Strike price of forward contract is: %.2f") % strike << std::endl;

//forward contract on a fixed rate bond
FixedRateBondForward fixedRateBondForward(bondIssueDate, forwardMaturityDate, Position::Type::Long, strike, settlementDays,
ActualActual(ActualActual::Bond), calendar, ModifiedFollowing, fixedRateBondPtr, flatTermStructure, flatTermStructure);

//calculate forward price of bond 
Real forwardPrice = fixedRateBondForward.NPV();
std::cout << boost::format("Bond forward contract value: %.2f") % forwardPrice << std::endl;

//evaluate forward contract by shocking interest rates +/- 1%
boost::shared_ptr<YieldTermStructure> flatForwardRatesUpOnePercent(new FlatForward(bondIssueDate,
rate + .01, ActualActual(ActualActual::Bond), Compounded, Annual));

flatTermStructure.linkTo(flatForwardRatesUpOnePercent);

//recalculate forward price of bond 
std::cout << boost::format("Bond forward contract value (rates up 1 percent): %.2f") % fixedRateBondForward.NPV() << std::endl;

boost::shared_ptr<YieldTermStructure> flatForwardRatesDownOnePercent(new FlatForward(bondIssueDate,
rate - .01, ActualActual(ActualActual::Bond), Compounded, Annual));

flatTermStructure.linkTo(flatForwardRatesDownOnePercent);

//recalculate forward price of bond 
std::cout << boost::format("Bond forward contract value (rates down 1 percent): %.2f") % fixedRateBondForward.NPV() << std::endl;

}
```

这段代码运行的输出结果是：

`债券价格：105.657

现金流：2014 年 4 月 2 日，5.00

现金流：2015 年 4 月 2 日，5.00

现金流：2016 年 4 月 4 日，5.00

现金流：2016 年 4 月 4 日，100.00

远期合同到期日：2014 年 7 月 2 日

远期合同到期日剩余天数：455 天

远期合同的执行价格为：104.61

债券远期合同价值：-0.00

债券远期合同价值（利率上升 1%）：-1.63

债券远期合同价值（利率下降 1%）：1.70

正如预期的那样，当远期合同首次发行时，其价值为零。当利率上升/债券价格下降时，远期合同的价值会下降，反之亦然，当利率下降/债券价格上涨时。

我希望您喜欢这篇最新文章，它解释了如何使用 QuantLib 估值远期和期货合同。请随时关注，并留下评论和问题。祝您在使用 QuantLib 时玩得开心！

## 关于 Mick Hittesdorf

我是一位多才多艺的技术领导者，对数据分析、数据科学和大数据技术充满热情。我在大型和小型组织中都有工作经验，担任过各种角色。我曾负责管理一个全球数据科学和分析平台，开发了低延迟的专有交易系统，管理过软件开发团队，制定了企业架构策略，撰写了白皮书和博客，在行业期刊上发表文章，并以咨询和技术销售的身份向客户提供创新解决方案。我当前的关注领域包括大数据、数据工程、数据科学、R 和云计算。
