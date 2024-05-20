<!--yml
category: 未分类
date: 2024-05-18 08:09:29
-->

# European options pricing in C++ with QFCL | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2012/07/16/european-options-pricing-in-c-with-qfcl/#0001-01-01](https://quantcorner.wordpress.com/2012/07/16/european-options-pricing-in-c-with-qfcl/#0001-01-01)

This time, we implement classes from the [QFCL](http://qfcl.wilmott.com/) project allowing to price **European vanilla options**, and to compute the **Greeks**.

We borrowed both the [core.hpp](http://qfcl.wilmott.com/p/bmlib/source/tree/HEAD/trunk/cpp/bmlib/core.hpp) and the [gbm_option_vanilla.hpp](http://qfcl.wilmott.com/p/bmlib/source/tree/HEAD/trunk/cpp/bmlib/gbm_vanilla.hpp) files of **QFCL**. These are two header files. Notice that we made some changes in the original **gbm_option_vanilla.hpp** file (we corrected some formulae.

Below, is the snippet in C++ of the implementation. This is simple coding, workable.

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

Finally, here is a web link to this project in a zipped folder: [https://docs.google.com/open?id=0B4cGI2MhdkteaE9lTzdnU1U4LUk](https://docs.google.com/open?id=0B4cGI2MhdkteaE9lTzdnU1U4LUk "https://docs.google.com/open?id=0B4cGI2MhdkteaE9lTzdnU1U4LUk")