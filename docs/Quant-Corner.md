<!--yml

分类：未分类

日期：2024-05-18 08:10:50

-->

# Quant Corner

> 来源：[`quantcorner.wordpress.com#0001-01-01`](https://quantcorner.wordpress.com#0001-01-01)

以下是一个示例代码，创建一个带有从标准 *.csv* 文件中提取的 OHLC（开盘价、最高价、最低价、收盘价）数据的 **QuantLib** 对象。

**QL** 提供了 *QuantLib::TimeSeries* 类，这是一个用于历史数据的容器。它可以用于简单的日期/报价时间序列（例如 [在此处](https://quantcorner.wordpress.com/2013/02/10/an-example-code-using-quantlib-timeseries/ "时间序列 & QuantLib")）。好处是，它还可以与 *QuantLib::IntervalPrice* 重载以创建 OHLC 对象。

不知何故，*QuantLib::IntervalPrice* 返回 OCHL 对象（？）。这并不是什么大问题，但在调用方法/使用检查员时可能会引起混淆。我们首先对 *QL* 的 *prices.hpp* 文件进行更改，本质上交换构造参数/变量名称。请注意，所做的一切更改并非都是为了实现我们想要的结果；有些纯粹是装饰性的。

以下是 *prices.hpp* 文件的 diff：

```
/* -*- mode: c++; tab-width: 4; indent-tabs-mode: nil; c-basic-offset: 4 -*- */

/*
 Copyright (C) 2015, Edouard 'tagoma' Tallent
 Copyright (C) 2006, 2007 Ferdinando Ametrano
 Copyright (C) 2006 Katiuscia Manzoni
 Copyright (C) 2006 Joseph Wang

 This file is part of QuantLib, a free-software/open-source library
 for financial quantitative analysts and developers - http://quantlib.org/

 QuantLib is free software: you can redistribute it and/or modify it
 under the terms of the QuantLib license.  You should have received a
 copy of the license along with this program; if not, please email
 <quantlib-dev@lists.sf.net>. The license is also available online at
 <http://quantlib.org/license.shtml>.

 This program is distributed in the hope that it will be useful, but WITHOUT
 ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS
 FOR A PARTICULAR PURPOSE.  See the license for more details.
*/

/*! \file prices.hpp
    \brief price classes
*/

#ifndef quantlib_prices_hpp
#define quantlib_prices_hpp

#include <ql/timeseries.hpp>
#include <ql/utilities/null.hpp>

namespace QuantLib {

    //! Price types
    enum PriceType {
         Bid,          /*!< Bid price. */
         Ask,          /*!< Ask price. */
         Last,         /*!< Last price. */
         Close,        /*!< Close price. */
         Mid,          /*!< Mid price, calculated as the arithmetic
                            average of bid and ask prices. */
         MidEquivalent, /*!< Mid equivalent price, calculated as
                            a) the arithmetic average of bid and ask prices
                            when both are available; b) either the bid or the
                            ask price if any of them is available;
                            c) the last price; or d) the close price. */
         MidSafe       /*!< Safe Mid price, returns the mid price only if
                            both bid and ask are available. */
    };

    /*! return the MidEquivalent price, i.e. the mid if available,
        or a suitable substitute if the proper mid is not available
    */
    Real midEquivalent(const Real bid,
                       const Real ask,
                       const Real last,
                       const Real close);

    /*! return the MidSafe price, i.e. the mid only if
        both bid and ask prices are available
    */
    Real midSafe(const Real bid,
                 const Real ask);

    //! interval price
    class IntervalPrice {
      public:
        enum Type { Open, High, Low, Close };

        IntervalPrice();
        IntervalPrice(Real open, Real high, Real low, Real close);
        //! \name Inspectors
        //@{
        Real open() const { return open_; }
        Real high() const { return high_; }
        Real low() const { return low_; }
        Real close() const { return close_; }
        Real value(IntervalPrice::Type) const;
        //@}

        //! \name Modifiers
        //@{
        void setValue(Real value, IntervalPrice::Type);
        void setValues(Real open, Real high, Real low, Real close);
        //@}

        //! \name Helper functions
        //@{
        static TimeSeries makeSeries(
            const std::vector& d,
            const std::vector& open,
            const std::vector& high,
            const std::vector& low,
            const std::vector& close);

        static std::vector extractValues(
                                          const TimeSeries&,
                                          IntervalPrice::Type);
        static TimeSeries extractComponent(
                                          const TimeSeries&,
                                          enum IntervalPrice::Type);
        //@}
      private:
          Real open_, high_, low_, close_;
    };

    template <>
    class Null 
    {
      public:
        Null() {}
        operator IntervalPrice() const { return IntervalPrice(); }
    };

}

#endif

```

我们现在可以转向我们的包装器：

```
/*
Copyright (C) 2015, Edouard 'tagoma' Tallent
OHLC timeseries factory based on QuantLib 
QuantCorner @ https://quantcorner.wordpress.com
*/

#include <fstream>
#include <string>
#include <iostream>
#include <vector>
#include <memory>
#include <ql\quantlib.hpp>
#include <boost\algorithm\string\split.hpp>
#include <boost\algorithm\string\classification.hpp>

// Wrapper creating a QuantLib OHLC time series from *.csv file
QuantLib::TimeSeries<QuantLib::IntervalPrice> QL_OHLC(char *filename){
    std::ifstream file(filename);
    std::string line;
    std::vector<QuantLib::Real> open, close, high, low;
    std::vector<QuantLib::Date> dates;
    std::vector<std::string> tokens;
    QuantLib::TimeSeries<QuantLib::IntervalPrice> ochl;

    while (std::getline(file, line))
    {
        std::stringstream stringStream(line);
        std::string content;
        int item = 0;
        while (std::getline(stringStream, content, ',')) {
            switch (item) {
            case 0:
                boost::algorithm::split(tokens, content, boost::algorithm::is_any_of("/"));
                dates.push_back(QuantLib::Date(QuantLib::Day(std::stoi(tokens.at(0))),
                    QuantLib::Month(std::stoi(tokens.at(1))),
                    QuantLib::Year(std::stoi(tokens.at(2)))));
                break;
            case 1: open.push_back(std::stod(content)); break;
            case 2: close.push_back(std::stod(content)); break;
            case 3: high.push_back(std::stod(content)); break;
            case 4: low.push_back(std::stod(content)); break;
            }
            item++;
        }
    }
    return QuantLib::IntervalPrice::makeSeries(dates, open, high, low, close);
}

auto main(int argc, char *argv []) -> int
{
    // Function call
    char* file = argv[1];
    QuantLib::TimeSeries<QuantLib::IntervalPrice> ohlc = QL_OHLC(file);

    // Start date of the time series
    std::cout << "Start date: " << ohlc.firstDate() << std::endl;

    // Is the time series empty?
    std::cout << "Time series empty (1:Yes; 0:No): "
        << ohlc.empty() << std::endl;

    // Return the number of dates/time series length
    std::cout << "Series length (number of time steps): "
        << ohlc.size() << std::endl;

    // Access the OHLC values
    std::vector<QuantLib::IntervalPrice> v;
    for (auto i : ohlc)
        v.push_back(i.second);
        std::cout << "\nOpen\tHigh\tLow\tClose" << std::endl;
    for (auto i : v)
        std::cout << i.open() << "\t" << i.high() << "\t" << i.low()
        << "\t" << i.close() << std::endl;
    std::cout << "\n";

    // Etc ....

    return 0;
}

/*
/////////////////////////
/ Demo datafile (*.csv) /
/////////////////////////
11/05/2015,51.18,51.99,51.06,51.21
12/05/2015,51.64,52.12,51.24,51.95
13/05/2015,50.61,51.80,50.47,51.64
14/05/2015,50.61,50.67,50.00,50.27
15/05/2015,49.55,50.91,49.54,50.91
18/05/2015,48.68,49.50,48.51,48.95
19/05/2015,48.42,49.04,48.01,48.68
20/05/2015,48.83,49.19,48.00,48.52
21/05/2015,48.54,48.96,47.69,48.45
22/05/2015,49.31,49.40,48.19,48.64
25/05/2015,49.34,50.22,49.03,49.63
26/05/2015,48.28,48.79,47.84,48.33
27/05/2015,47.97,48.86,47.31,47.66
28/05/2015,49.12,49.19,47.55,48.06
29/05/2015,51.21,51.37,50.57,51.16
01/06/2015,51.52,51.58,51.03,51.20
02/06/2015,52.30,52.39,51.52,51.52
*/

/*
//////////////////
/ Program output /
//////////////////
Start date : May 11th, 2015
Time series empty(1:Yes; 0:No) : 0
Series length(number of time steps) : 17

Open    High    Low     Close
51.18   51.99   51.06   51.21
51.64   52.12   51.24   51.95
50.61   51.8    50.47   51.64
50.61   50.67   50      50.27
49.55   50.91   49.54   50.91
48.68   49.5    48.51   48.95
48.42   49.04   48.01   48.68
48.83   49.19   48      48.52
48.54   48.96   47.69   48.45
49.31   49.4    48.19   48.64
49.34   50.22   49.03   49.63
48.28   48.79   47.84   48.33
47.97   48.86   47.31   47.66
49.12   49.19   47.55   48.06
51.21   51.37   50.57   51.16
51.52   51.58   51.03   51.2
52.3    52.39   51.52   51.52

Press any key to continue . . .
*/

```
