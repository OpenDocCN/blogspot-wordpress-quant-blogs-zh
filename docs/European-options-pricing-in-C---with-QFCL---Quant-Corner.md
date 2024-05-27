<!--yml

category: 未分类

date: 2024-05-18 08:09:29

-->

# 用 QFCL 在 C++ 中定价欧式期权 | 量化角落

> 来源：[`quantcorner.wordpress.com/2012/07/16/european-options-pricing-in-c-with-qfcl/#0001-01-01`](https://quantcorner.wordpress.com/2012/07/16/european-options-pricing-in-c-with-qfcl/#0001-01-01)

这次，我们从[QFCL](http://qfcl.wilmott.com/)项目实现了一些类，允许定价**欧式期权**，并计算**希腊字母**。

我们借用了**QFCL**的[core.hpp](http://qfcl.wilmott.com/p/bmlib/source/tree/HEAD/trunk/cpp/bmlib/core.hpp)和[gbm_option_vanilla.hpp](http://qfcl.wilmott.com/p/bmlib/source/tree/HEAD/trunk/cpp/bmlib/gbm_vanilla.hpp)两个文件。这是两个头文件。请注意，我们对原始的**gbm_option_vanilla.hpp**文件进行了一些更改（我们纠正了一些公式）。

下面是 C++ 实现的片段。这是简单的编码，可行的。

```
// Édouard Tallent @ TAGOMA.tech (July, 2012)
// GBM_Vanilla Implementation from the QFCL project, http://fcl.wilmott.com/
// Header files core.hpp and gbm_vanilla.hpp coded by M.A. (Thijs) van den Berg (2011), http://sitmo.com/

#include<iostream>
#include<cmath>
#include "core.hpp"
#include "gbm_vanilla.hpp"

using namespace std;
using namespace bmlib;

void Call_Option (
    double S,
    double Y,
    double v,
    double r,
    double X,
    double t){
        cout << "\n\nCall price:\t" << gbm_vanilla_call_price(S, Y, v, r, X, t) << endl;
        cout << "Delta:\t\t" << gbm_vanilla_call_delta(S, Y, v, r, X, t) << endl;
        cout << "Gamma:\t\t" << gbm_vanilla_gamma(S, Y, v, r, X, t) << endl;
        cout << "Theta:\t\t" << gbm_vanilla_call_theta(S, Y, v, r, X, t) << endl;
        cout << "Vega:\t\t" << gbm_vanilla_vega(S, Y, v, r, X, t) << endl;        
        cout << "Rho:\t\t" << gbm_vanilla_call_rho(S, Y, v, r, X, t) << endl;

}

void Put_Option (
    double S,
    double Y,
    double v,
    double r,
    double X,
    double t){
        cout << "\n\nPut price:\t" << gbm_vanilla_put_price(S, Y, v, r, X, t) << endl;
        cout << "Delta:\t\t" << gbm_vanilla_put_delta(S, Y, v, r, X, t) << endl;
        cout << "Gamma:\t\t" << gbm_vanilla_gamma(S, Y, v, r, X, t) << endl;
        cout << "Theta:\t\t" << gbm_vanilla_put_theta(S, Y, v, r, X, t) << endl;
        cout << "Vega:\t\t" << gbm_vanilla_vega(S, Y, v, r, X, t) << endl;        
        cout << "Rho:\t\t" << gbm_vanilla_put_rho(S, Y, v, r, X, t) << endl;

}

int main(int argc, char* argv[])
{

    bool end = false;
    do
    {
    try{

        // Variable initialization
        char option_type;
        double S;
        double Y;
        double v;
        double r;
        double X ;
        double t ;

        // Console inputs
        cout << "\n\nCall or put option (C or P)?\t";
        cin >> option_type ;

        cout << "Strike:\t\t\t\t";
        cin >> X ;

        cout << "Underlying price (S):\t\t";
        cin >> S;

        cout << "Risk-free rate (%):\t\t";
        cin >> r;

        cout << "Volatility:\t\t\t";
        cin >> v;

        cout << "Yield rate:\t\t\t";
        cin >> Y ;        

        cout << "Time to maturity (in years):\t";
        cin >> t ;

        if (option_type == 'c' || option_type == 'C')
        {
            Call_Option (S, Y, v, r, X, t);
        }
        else
        {
        Put_Option (S, Y, v, r, X, t);
        }
    }

    catch (std::exception& e)
        {
            std::cerr << e.what() << endl;
            return 1;
        }
        catch (...)
        {
            std::cerr << "unknown error" << endl;
            return 1;
        }

    } while (end != true);

return 0;

}
```

最后，这是一个压缩文件中项目的网页链接：[`docs.google.com/open?id=0B4cGI2MhdkteaE9lTzdnU1U4LUk`](https://docs.google.com/open?id=0B4cGI2MhdkteaE9lTzdnU1U4LUk "https://docs.google.com/open?id=0B4cGI2MhdkteaE9lTzdnU1U4LUk")
