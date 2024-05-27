`<!--yml`

`category: 未分类`

日期：2024-05-18 06:47:03

`-->`

# 介绍 QuantLib：利率期限结构|金融与科技事务大全...

> 来源：[`mhittesdorf.wordpress.com/2013/02/25/introducing-quantlib-the-term-structure-of-interest-rates/#0001-01-01`](https://mhittesdorf.wordpress.com/2013/02/25/introducing-quantlib-the-term-structure-of-interest-rates/#0001-01-01)

在这个系列的最后一篇文章中，我开始谈论 QuantLib 对利率期限结构的支持，金融从业者通常将这称为“收益率曲线”。在正常经济条件下，收益率曲线呈上升趋势——长期利率高于短期利率。下面的图表图形地展示了利率与到期时间之间的关系。

![yield_curve](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/02/yield_curve.jpeg)

利率曲线的水平、斜率和形状是债券和债券组合定价和风险管理固有的。为了准确地定价债券，或者更一般地说，准确计算未来现金流的现值，必须从收益率曲线中推断出现金流发生时的利率。

所以让我们重新审视一下我们之前的债券定价示例，看看如何使用 QuantLib 的[YieldTermStructure](http://quantlib.org/reference/class_quant_lib_1_1_yield_term_structure.html)类构建收益率曲线并定价债券。考虑一个面值为 100 的 3 年固定利率债券，利率为 3%，每年支付 5%的年息，且每年复利。我们已经知道债券的价格是 105.66。下面的代码显示了如何使用显式收益率曲线而不是单一的恒定利率来复制这个价格。需要注意的是，恒定利率与平坦的收益率曲线相同，即所有到期时间的利率都相同。为了计算与之前相同的 105.66 的价格，示例使用了 QuantLib 的[FlatForward](http://quantlib.org/reference/class_quant_lib_1_1_flat_forward.html)类来表示收益率“曲线”。

`#include <cstdlib>`

`#include <iostream>`

`#define BOOST_AUTO_TEST_MAIN`

`#include <boost/test/unit_test.hpp>`

`#include <boost/detail/lightweight_test.hpp>`

`#include <ql/quantlib.hpp>`

`#include <vector>`

`#include <ql/instruments/bonds/fixedratebond.hpp>`

`BOOST_AUTO_TEST_CASE(testPriceBondWithFlatTermStructure) {

`Calendar calendar = UnitedStates(UnitedStates::GovernmentBond);`

`const Natural settlementDays = 3;`

`Date today = Date::todaysDate();`

`Date issueDate = today;`

`Date terminationDate = issueDate + Period(3, Years);`

`Rate rate = .03;`

`InterestRate couponRate(.05, ActualActual(ActualActual::Bond), Compounded, Annual);`

`Real faceValue = 100.0;`

`std::vector<InterestRate> coupons(3, couponRate);`

`Schedule schedule(issueDate, terminationDate, Period(Annual), calendar,

Unadjusted, Unadjusted, DateGeneration::Backward, false);

FixedRateBond fixedRateBond(settlementDays, faceValue, schedule, coupons);

boost::shared_ptr<YieldTermStructure> flatForward(new FlatForward(issueDate, rate, ActualActual(ActualActual::Bond), Compounded, Annual));

Handle<YieldTermStructure> flatTermStructure(flatForward);

boost::shared_ptr<PricingEngine> bondEngine(new DiscountingBondEngine(flatTermStructure));

fixedRateBond.setPricingEngine(bondEngine);

真实 NPV = fixedRateBond.NPV();

std::cout << "债券的 NPV 为： " << npv << std::endl;

}`

这段代码的一个关键特点是其使用了定价引擎，即 DiscountingBondEngine。定价引擎是 QuantLib 中一个常见的抽象，有效地封装了特定于工具的估值逻辑。DiscountingBondEngine 的构造函数接受收益率曲线作为参数，从中提取折现债券息票所需的利率。值得注意的是，QuantLib 的[Schedule](http://quantlib.org/reference/class_quant_lib_1_1_schedule.html)类生成了债券的付息日，该类考虑了提供的日历以确定营业日和假日。总的来说，这段代码展示了在现实世界中定价债券所需的内容，明显的假设是收益率结构是平坦的。为了纠正这一最后的不足，可以用[FittedBondDiscountCurve](http://quantlib.org/reference/class_quant_lib_1_1_fitted_bond_discount_curve.html)类替换 FlatForward 类。在 QuantLib 网站上，你可以找到一个完整的示例，[FittedBondCurve.cpp](http://quantlib.org/reference/_fitted_bond_curve_8cpp-example.html)，它展示了如何使用 FittedBondDiscountCurve“引导”一个给定市场利率报价的收益率曲线。我鼓励你查看一下。

这就到这里。在我的下一篇文章中，我将使用 QuantLib 求解器后退出一系列现金流利率。到时候见！

## 关于 Mick Hittesdorf

我是个多才多艺的技术领导者，对数据分析、数据科学和大数据技术充满热情。我在大型和小型组织中都有工作经验，担任过各种角色。我曾负责管理一个全球数据科学和分析平台，开发了低延迟的专有交易系统，管理过软件开发团队，制定了企业架构策略，撰写了白皮书和博客，在行业期刊上发表过文章，并以咨询和技术销售的身份向客户提供了创新的解决方案。我当前的关注领域包括大数据、数据工程、数据科学、R 和云计算。
