<!--yml

类别：未分类

日期：2024 年 05 月 18 日 08 时 09 分 46 秒

-->

# 使用 C++计算基础风险和最小方差套期保值比率 | 量化角落

> 来源：[`quantcorner.wordpress.com/2011/03/04/basis-risk-and-minimum-variance-hedge-ratio-with-c/#0001-01-01`](https://quantcorner.wordpress.com/2011/03/04/basis-risk-and-minimum-variance-hedge-ratio-with-c/#0001-01-01)

这一次我们暂时不讨论**QuantLib**。我们展示一些基本的金融计算可以用 C++来处理。

我们希望编写一段 C++代码来计算：

– 一个由 1 个**现货**合约和一定数量的**期货**合约组成的投资组合的**基础风险**

– 同时，我们定义另一个 C++函数来计算**最小方差套期保值**。

**套期保值比率**（**h**）是一个人在**现货市场**中对其敞口进行套期保值时应该使用的**期货**合约数。

**基础风险**是基础的方差，后者是**现货价格**和**期货合约**价格之间的差异。

**最小方差套期保值比率**（**h***）是使基础风险最小化的套期保值比率。

[`www.bionicturtle.com`](http://www.bionicturtle.com/)的那位小伙子在一段[视频](http://www.youtube.com/watch?v=Bm54Lwd-27U)中很好地解释了这一切。而我们所做的就是编写与此视频中的 Excel 电子表格对应的 C++代码。这里有一个类似的[电子表格](https://quantcorner.wordpress.com/wp-content/uploads/2011/03/basis_risk_min_var_hedge.xlsx)。

下面，我们展示我们的 C++代码。

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
