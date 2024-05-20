<!--yml
category: 未分类
date: 2024-05-12 19:29:41
-->

# SSAddin: Google Analytics, Baremetrics, Quandl & Tiingo | Coding the markets

> 来源：[https://etrading.wordpress.com/2017/06/05/ssaddin-google-analytics-baremetrics-quandl-tiingo/#0001-01-01](https://etrading.wordpress.com/2017/06/05/ssaddin-google-analytics-baremetrics-quandl-tiingo/#0001-01-01)

## SSAddin: Google Analytics, Baremetrics, Quandl & Tiingo

### June 5, 2017

I’ve [mentioned SSAddin](https://etrading.wordpress.com/2016/05/26/threading-is-hard-tiingo-iex-ssaddin/) on this blog before, but not given much detail about it. SSAddin is an XLL Excel addin exposing APIs for Google Analytics, Baremetrics, Quandl, Tiingo as worksheet functions. It’s distributed under a permissive Apache 2.0 license, so you can use, repurpose or redistribute however you like with no fees so long as you include license and copyright notices. You can download 32 and 64 bit .xll binaries from here: [http://spreadserve.com/s3/downloads.html](http://spreadserve.com/s3/downloads.html)

Don’t forget to take a copy of SSAddin.xll.config too and put it next to SSAddin.xll on your PC. You’ll need to edit the .config to add your license keys for Google, Baremetrics, Quandl and Tiingo. There’s [documentation here](https://spreadserve-addin.readthedocs.io/en/latest/index.html), but I suggest you start by playing with example spreadsheets from GitHub: [https://github.com/SpreadServe/SSAddin/tree/master/xls](https://github.com/SpreadServe/SSAddin/tree/master/xls)

Don’t hesitate to ask questions in the comments here, or on the download page, or to [raise an issue on GitHub](https://github.com/SpreadServe/SSAddin/issues).