<!--yml
category: 未分类
date: 2024-05-12 19:52:52
-->

# Excel 12 | Coding the markets

> 来源：[https://etrading.wordpress.com/2006/06/09/excel-12/#0001-01-01](https://etrading.wordpress.com/2006/06/09/excel-12/#0001-01-01)

## Excel 12

### June 9, 2006

[Excel 12](http://blogs.msdn.com/excel/) aka Excel 2007 is going to be a big one for front office developers. Having [coded XLLs for real time pricing](https://etrading.wordpress.com/excel/) and autoquoting, I was wondering when Excel would support multi threaded calcs. The [good news](http://blogs.msdn.com/excel/archive/2006/01/03/508985.aspx) is that Excel 12 adds multi threaded execution of XLL worksheet functions. This means that pricing sheets will now be able to fully exploit multi processor hosts.

So the next question has to be: can one run pricing XLLs in the new [Excel Server](http://blogs.msdn.com/excel/archive/category/11361.aspx) environment ?  There's a limit to how much processing oomph we can have at a trading desk. Our traders are limited to two 2CPU PCs per desk, due to heat and power restrictions. If they need any more CPU we have to use blades in the machine room as remote desktops. Server hosting of pricing sheets would resolve these issues nicely.

 Fortunately, it looks like the answer is yes, given a bit of [wrapping in managed code](http://blogs.msdn.com/excel/archive/2006/05/03/589094.aspx).