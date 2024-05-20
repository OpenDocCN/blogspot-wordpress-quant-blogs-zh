<!--yml
category: 未分类
date: 2024-05-18 08:09:46
-->

# Basis risk and minimum variance hedge ratio with C++ | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2011/03/04/basis-risk-and-minimum-variance-hedge-ratio-with-c/#0001-01-01](https://quantcorner.wordpress.com/2011/03/04/basis-risk-and-minimum-variance-hedge-ratio-with-c/#0001-01-01)

This time we leave **QuantLib** aside. We show that some basic financial calculations can be dealt with with C++.

We wish to write a piece of C++ code to calculate :
– the **basis risk** of a portfolio made of 1 **spot** contract and a certain number of **futures** contracts
– and, we define another C++ function to compute the **minimum variance hedge**.

The **hedge ratio** (**h**) is the number of **futures** contracts one should use to hedge his exposure in the **spot market**.

**Basic risk** is the variance of the basis, the latter being the difference between the s**pot price** and the price of the **futures contract**.

The **minimum variance hedge ratio** (**h***) is the hedge ratio that minimizes the basis risk.

The guy of [http://www.bionicturtle.com](http://www.bionicturtle.com/) explains all that nicely in a [video](http://www.youtube.com/watch?v=Bm54Lwd-27U) . And, what we do is writing the C++ code corresponding to the Excel spreadsheet in this video. Here is a similar [spreadsheet](https://quantcorner.wordpress.com/wp-content/uploads/2011/03/basis_risk_min_var_hedge.xlsx).

Below, we show our C++ code.

```
#include<iostream>

using namespace std;

struct Inputs{
	double spot_vol;
	double futures_vol;
	double rho;
	};

void setupExample (Inputs &i){
i.spot_vol = 0.2;
i.futures_vol = 0.3;
i.rho = 0.9;
}

void basis_risk (const Inputs &i){
	double hedgeRatio = 0.3;
	do {
		cout << "Hedge ratio = " << hedgeRatio
			<< " Basis risk = "
			<< (i.spot_vol*i.spot_vol+(hedgeRatio*i.futures_vol)
			*(hedgeRatio*i.futures_vol)
			- (2*hedgeRatio*i.spot_vol*i.futures_vol*i.rho)) << endl;
		hedgeRatio = hedgeRatio + 0.1;
	 } while (hedgeRatio < 1) ;
}

void min_var_hedge(const Inputs &i){
	cout << endl;
	cout << "Min Var Hedge : " << i.rho*i.spot_vol/i.futures_vol << endl;
}

int main (int, char*[]){
	Inputs i;
	setupExample (i);
	basis_risk (i);
	min_var_hedge (i);
}
```