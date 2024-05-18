<!--yml
category: 未分类
date: 2024-05-18 08:08:58
-->

# US Treasury notes and QuantLib | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2011/01/31/us-treasury-notes-and-quantlib/#0001-01-01](https://quantcorner.wordpress.com/2011/01/31/us-treasury-notes-and-quantlib/#0001-01-01)

Here, we deal with **US debt securities**, and more specifically with **US Treasury note****s**. Before turning to the **C++/QuantLib** code itself, we remind the reader with some bond-related terminology. And, we will conclude with short comments on our code.

**Bond terminology refresh**

**Principal** or **face value**: the amount invested in the bond.

**Coupon**: the periodic payment until the bond expires. It is a financial flow from the issuer toward the holder of the bond. The payments can occur at different time interval, it is generally **annual** or **semi annual** coupon. And, a bond can pay a **fixed coupon** or much less frequently a **variable coupon**.

**Redemption value**: a bond can be repurchased by the issuing company before expiration. That is redemption. And, the redemption value often is equal to the bond principal, but not always.

**Clean price**: the bond quoted without any accrued interest.

**Accrued interest**: the amount of interest built up since the last coupon payment.

**Dirty price**: it equals clean price + accrued interest. It is the actual payment received by the bond holder.

### C++/QuantLib code

We now turn to the code.
__________________________
**US Treasury security type**:    note
**Principal**:                                            100
**Issuing date**:                                     January 27th, 2011
**Settlement**:                                       January 28th, 2011
**Maturity**:                                            August 31th, 2020
**Coupon rate**:                                    3,625%
**Yield**:                                                     3,4921%
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

**QuantLib** has powerful tools to handle dates (date calculations, formatting, …) . A simple example in our code is :

```
Date settlementDate(28, January, 2011);
// the settlement date must be a business day
settlementDate = calendar.adjust(settlementDate);
```

**settlementDate** will be adjusted to the appropriate near business day according to the given convention, thanks to **calendar.adjust(settlementDate)**.
Thus, **QuantLib** allows to value ‘for real’ in this case a US Treasury note. That implies it requires a precise knowledge of convention dates. *How does the US Treasury cope with bank holidays ?*

The reader may have noticed the **try**,  **catch** and **throw** statements that we introduced in a recent post. Here, the **exception mechanism** doesn’t actually do a great deal for us. But, coding **exception mechanisms** is a good practice to make.

Finally, we introduced the **RelinkableHandle** handles, even if we don’t take much advantage of them in this code example. One benefit is that values  passed in relinkable handles can then be relinked to some other data source later on.