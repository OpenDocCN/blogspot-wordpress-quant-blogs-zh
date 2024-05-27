<!--yml

分类：未分类

日期：2024-05-18 13:56:54

-->

# 正态分布计算 | 存在 NaN 数量的计算 - 量化交易、统计学习、编程和头脑风暴

> 来源：[`quantlife.wordpress.com/2013/04/21/normal-distribution-calculations/#0001-01-01`](https://quantlife.wordpress.com/2013/04/21/normal-distribution-calculations/#0001-01-01)

### 正态分布计算

```
// Cumulative N(0,1) and Inverse Cumulative N(0,1)
#include <iostream>
#include <vector>
#include <cmath>
using namespace std;

double f(double);							// N(0,1) density
double N(double);							// N(0,1) cdf
double Ni(double);							// N(0,1) inverse cdf
double Boole(double, double, int);			// Boole's numerical integration
double Bisection(double, double, double);	// Bisection algorithm

int main()
{
	cout << "A few cumulative N(0,1) probabilities" << endl;
	cout << "N(1.96)  = " << N(1.96)  << endl;
	cout << "N(2.33)  = " << N(2.33)  << endl;
	cout << "N(-1.96) = " << N(-1.96)  << endl;
	cout << "N(-2.33) = " << N(-2.33)  << endl;
	cout << endl;
	cout << "A few inverse cumulative N(0,1) probabilities" << endl;
	cout << "Ni(0.99)  = " << Ni(0.99)  << endl;
	cout << "Ni(0.975) = " << Ni(0.975) << endl;
	cout << "Ni(0.05)  = " << Ni(0.05)  << endl;
	return 0;
}

// N(0,1) density
double f(double x) {
	double pi =  4.0*atan(1.0);
	return exp(-x*x*0.5)/sqrt(2*pi);
}

// N(0,1) cdf by Boole's Rule
double N(double x) {
	return Boole(-10.0, x, 240);
}

// Boole's Rule
double Boole(double StartPoint, double EndPoint, int n) {
	vector<double> X(n+1, 0.0);
	vector<double> Y(n+1, 0.0);
	double delta_x = (EndPoint - StartPoint)/double(n);
	for (int i=0; i<=n; i++) {
		X[i] = StartPoint + i*delta_x;
		Y[i] = f(X[i]);
	}
	double sum = 0;
	for (int t=0; t<=(n-1)/4; t++) {
		int ind = 4*t;
		sum += (1/45.0)*(14*Y[ind] + 64*Y[ind+1] + 24*Y[ind+2] + 64*Y[ind+3] + 14*Y[ind+4])*delta_x;
	}
	return sum;
}

// Inverse cumulative N(0,1) by bisection algorithm
double Ni(double prob) {
	return Bisection(prob, -10.0, 10.0);
}

// Bisection Algorithm
double Bisection(double prob, double a, double b)
{
	const int MaxIter = 500;
	double Tol = 0.00001;
	double midP, midCdif;
	double  lowCdif = prob - N(a);
	double highCdif = prob - N(b);
	if (lowCdif*highCdif > 0)
	{
		double Temp = lowCdif;
		lowCdif = highCdif;
		highCdif = Temp;
	}
	else
	for (int i=0; i<=MaxIter; i++)
	{
		midP = (a + b) / 2.0;
		midCdif = prob - N(midP);
		if (abs(midCdif)<Tol) goto LastLine;
		else
		{
			if (midCdif>0) a = midP;
			else b = midP;
		}
	}
 LastLine:
	return midP;
}
// http://www.tohtml.com/cpp
```

目前尚无评论。
