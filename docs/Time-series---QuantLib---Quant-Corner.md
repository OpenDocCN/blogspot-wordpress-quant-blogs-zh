<!--yml

分类：未分类

日期：2024-05-18 08:07:40

-->

# 时间序列与 QuantLib | 量化角

> 来源：[`quantcorner.wordpress.com/2013/02/10/an-example-code-using-quantlib-timeseries/#0001-01-01`](https://quantcorner.wordpress.com/2013/02/10/an-example-code-using-quantlib-timeseries/#0001-01-01)

我们编写了一个示例代码，实现了**QuantLib**库的**TimeSeries**类。

这段代码实际上解析了一个从**Yahoo! Finance**下载的包含时间的***.csv**文件。文件中的每一行都包含了一个日期以及相应的开盘价、最高价、最低价、收盘价、交易量和调整后的收盘价。

在这里，我们使用调整后的收盘价创建了**QuantLib::TimeSeries**对象，但代码很容易适应其他需求。

以下是代码、输送到控制台的输出结果以及源数据文件。

```
/*
Copyright (C) 2013, Edouard 'tagoma' Tallent
QL timeseries wrapper 
QuantCorner @ https://quantcorner.wordpress.com
*/

#include
#include
#include
#include
#include<boost\algorithmstring.hpp>
#include<ql\quantlib.hpp>

QuantLib::TimeSeries<double> PriceSeries(char* filename)
{
    // Read the file provided via command line
    std::ifstream in (filename);
    std::string line;
    std::vector lines;
    while (in >> line)
        lines.push_back(line);

    // Container tools
    std::vector dates;
    std::vector quotes;

    for (unsigned int i = 0; i < lines.size(); i++)
        {
            std::vector outerArray;

            boost::split(outerArray, lines[i], boost::is_any_of(","));

            std::vector innerArray;
            boost::split(innerArray, outerArray[0], boost::is_any_of("-")); 

            QuantLib::Year year = (QuantLib::Year) std::stoi(innerArray[0]);
            QuantLib::Month month = (QuantLib::Month) std::stoi(innerArray[1]);
            QuantLib::Day day = (QuantLib::Day) std::stoi(innerArray[2]);

            dates.push_back(QuantLib::Date(day, month, year));
            quotes.push_back(atof(outerArray[6].c_str()));
        }

    // Create a QuantLib::TimeSeries object
    QuantLib::TimeSeries series(dates.begin(), dates.end(), quotes.begin());

    // Return the time series
    return series;
}

int main(int argc, char *argv[])
{
    // Source file
    char* filename = argv[1];

    // Call to the function
    QuantLib::TimeSeries mySeries = PriceSeries(filename);

    ///////////////////////////////////////////////////////////////
    // Below are implementations of some methods of QL Timeseries//
    ///////////////////////////////////////////////////////////////

    // Is the time series empty?
    std::cout << "Is the series empty? (0 = not empty)\t" << mySeries.empty() << std::endl;

    // Start date of the time series
    std::cout << "Start date of the time series:\t" << mySeries.firstDate() << std::endl;

    // Last date of the time series
    std::cout << "Last date of the time series:\t" << mySeries.lastDate() << std::endl;

    // What was the Adj.close value on November 14th, 2012?
    std::cout << "Adjusted close on November 14th, 2012:\t" << mySeries[QuantLib::Date(14, QuantLib::Nov, 2012)] << std::endl;

    return 0;
}

```

![QL_TimeSeries_source](https://quantcorner.wordpress.com/wp-content/uploads/2013/02/ql_timeseries_source.jpg)

感谢 Wilmott 社区的成员们提供了这些技巧，也感谢 Daniel Duffy（[Boost C++ Libraries](http://www.datasim-press.com/BoostVolumeI.html "Introduction to the Boost C++ Libraries")一书的作者之一）回答了我所有的问题。
