<!--yml

类别：未分类

日期：2024-05-18 08:08:58

-->

# US Treasury notes and QuantLib | Quant Corner

> 来源：[`quantcorner.wordpress.com/2011/01/31/us-treasury-notes-and-quantlib/#0001-01-01`](https://quantcorner.wordpress.com/2011/01/31/us-treasury-notes-and-quantlib/#0001-01-01)

在这里，我们处理的是**美国债务证券**，更具体地说是**美国国债票据**。在转向**C++/QuantLib**代码本身之前，我们提醒读者一些与债券相关的术语。最后，我们对代码进行简短的评论。

**债券术语回顾**

**本金**或**面值**：投资于债券的金额。

**息票**：直到债券到期为止的定期支付。这是发行方向债券持有人方向的金融流动。支付可以在不同的时间间隔发生，通常为**年度**或**半年**支付。而且，债券可以支付**固定息票**，或者更少见的是**浮动息票**。

**赎回价值**：在到期前，发行公司可以回购债券。这就是赎回。并且，赎回价值通常等于债券本金，但并不总是如此。

**干净价格**：不包含任何应计利息的债券报价。

**应计利息**：自上次息票支付以来积累的利息金额。

**脏价格**：等于干净价格加上应计利息。这是债券持有人实际收到的支付。

### C++/QuantLib 代码

现在我们来看代码。

__________________________

**美国国债证券类型**：票据

**本金**：100

**发行日**：2011 年 1 月 27 日

**结算日**：2011 年 1 月 28 日

**到期日**：2020 年 8 月 31 日

**息票率**：3,625%

**收益率**：3,4921%

________________________________

```
#include <ql/quantlib.hpp>
#include <iostream>
#include <iomanip>

#include <boost/timer.hpp>
using namespace QuantLib;

#if defined(QL_ENABLE_SESSIONS)
namespace QuantLib {
Integer sessionId() { return 0; }
}
#endif

int main(int, char* []) {

    try {

    boost::timer timer;
    std::cout << std::endl; 

	// date set up
	Calendar calendar = TARGET();

	Date settlementDate(28, January, 2011);
	// the settlement date must be a business day
	settlementDate = calendar.adjust(settlementDate);

	// Evaluation date
	Integer fixingDays = 1;
	Natural settlementDays = 1;
	Date todaysDate = calendar.advance(settlementDate, -fixingDays, Days);
	Settings::instance().evaluationDate() = todaysDate;

	// bond set up 
	Real faceAmount = 100.0;
	Real redemption = 100.0;
	Date issueDate(27, January, 2011);
	Date maturity(31, August, 2020);
	Real couponRate = 0.03625;
	Real yield = 0.034921;

	RelinkableHandle<YieldTermStructure> discountingTermStructure;
	boost::shared_ptr<YieldTermStructure> flatTermStructure(
	new FlatForward(
		settlementDate,
		yield,
		ActualActual(ActualActual::Bond),
		Compounding::Compounded,
		Semiannual));
	discountingTermStructure.linkTo(flatTermStructure);

	// Pricing engine
	boost::shared_ptr<PricingEngine> bondEngine(
		new DiscountingBondEngine(discountingTermStructure));

	 // Rate
	Schedule fixedBondSchedule(
		issueDate,
		maturity,
		Period(Semiannual),
		UnitedStates(UnitedStates::GovernmentBond),
		BusinessDayConvention::Unadjusted,
		BusinessDayConvention::Unadjusted,
		DateGeneration::Rule::Backward,
		false);

	FixedRateBond fixedRateBond(
		settlementDays,
		faceAmount,
		fixedBondSchedule,
		std::vector<Rate>(1, couponRate),
		ActualActual(ActualActual::Bond),
		BusinessDayConvention::Unadjusted,
		redemption,
		issueDate);

	fixedRateBond.setPricingEngine(bondEngine);

	std::cout << "Principal: " << faceAmount << std::endl;
	std::cout << "Issuing date: " << issueDate << std::endl;
	std::cout << "Maturity: " << maturity << std::endl;
	std::cout << "Coupon rate: " << std::setprecision (4) << io::percent(couponRate) << std::endl;
	std::cout << "Yield: " << std::setprecision (4) << io::percent(yield) << std::endl << std::endl;
	std::cout << "Net present value: " << std::setprecision (4) << fixedRateBond.NPV() << std::endl;
	std::cout << "Clean Price: " << std::setprecision (4) << fixedRateBond.cleanPrice() << std::endl;
	std::cout << "Dirty price: " <<  std::setprecision (4) << fixedRateBond.dirtyPrice() << std::endl;
	std::cout << "Accrued coupon: " <<  std::setprecision (4) << fixedRateBond.accruedAmount() << std::endl << std::endl;
	system("pause");
	return 0;

    } catch (std::exception& e) {
        std::cerr << e.what() << std::endl;
        return 1;
    } catch (...) {
        std::cerr << "unknown error" << std::endl;
        return 1;
    }
}
```

**QuantLib**拥有强大的工具来处理日期（日期计算、格式化等）。我们代码中的一个简单例子是：

```
Date settlementDate(28, January, 2011);
// the settlement date must be a business day
settlementDate = calendar.adjust(settlementDate);
```

根据给定的约定，**结算日**将调整为适当最近的营业日，得益于**calendar.adjust(settlementDate)**。

因此，**QuantLib**允许在此例中真实地估值美国国债票据。这暗示它需要对约定日期有精确的知识。*美国国债如何应对银行假期？*

读者可能已经注意到我们在最近的一篇文章中引入的**try**、**catch**和**throw**语句。在这里，**异常机制**实际上对我们并没有多大帮助。但是，编写**异常机制**是一个好的实践。

最后，我们引入了**RelinkableHandle**句柄，即使在这个代码示例中我们并没有充分利用它们。一个好处是，通过 relinkable handles 传递的值可以在稍后重新链接到其他数据源。
