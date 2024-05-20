<!--yml
category: 未分类
date: 2024-05-18 14:35:26
-->

# XLLoop framework | Systematic Investor

> 来源：[https://systematicinvestor.wordpress.com/2012/12/08/xlloop-framework/#0001-01-01](https://systematicinvestor.wordpress.com/2012/12/08/xlloop-framework/#0001-01-01)

Today I want to highlight the [XLLoop framework](http://xlloop.sourceforge.net/) : Excel User-Define Functions in in any language.

The [XLLoop](http://xlloop.sourceforge.net/) consists of two main components:

*   An Excel addin implementation (XLL written in c++).
*   A server and framework written in R (or/and in many other languages).

The [XLLoop](http://xlloop.sourceforge.net/) allows you to connect Excel and R in very simple way with almost zero installation.

**To get started**, please download and unzip the [xlloop-basic.zip](http://www.systematicportfolio.com/xlloop-basic.zip) archive that contains all files you need to make my sample application work.

**Next**, start Excel and add [XLLoop](http://xlloop.sourceforge.net/) addin.
I.e. in Office 2007/2010 Click File->Options->Add-Ins, press Alt+G, Click Browse and locate xlloop-0.3.2.xll
in Office 2003, Click Tools->Add-Ins, Click Browse and locate xlloop-0.3.2.xll

**Next**, edit runr.bat that was extracted from the zip archive. Enter correct path to your R installation.

**Finally**, execute runr.bat, you will see a command window popup, next go to Excel and type following formula
=FS(“ProductTest”, 32, 1886.5)

If all works well, you would see 60368

This might seem like a bit of black magic, so let me explain what is going on:

The runr.bat batch file starts a new R session and executes rstart.r script. In the rstart.r script we load/define any libraries / functions that we want to access in Excel. Next we load code for the XLLoop server and start the server. Here is the code in the rstart.r script

```

# define function
ProductTest <- function(x, y) x*y

# start xlloop server
source('xlloop.R')
XLLoopServer()

```

Next to access R functionality in Excel, we use FS function, the first parameter is the R function that we want to execute, following by function parameters. For example the =FS("ProductTest", 32, 1886.5) formula calls ProductTest R fucntion with x = 32 and y = 1886.5

*If you get “Cannot connect to the server” error message, please make sure that runr.bat batch is running (i.e. there is a command window) and try recalculating Excel (i.e. press F9)*

Once, you are done working with Excel, you can just close the command window created by runr.bat batch file.

I have included a few examples in the xlloop.xls for you to explore.

I will show a few more examples of the [XLLoop framework](http://xlloop.sourceforge.net/) in the next post.

Please let me know what problems you run into while experimenting with [XLLoop](http://xlloop.sourceforge.net/).

A side note. There are many options for connecting Excel and R. For example I have previously showed examples of [RExcel](http://en.wikipedia.org/wiki/RExcel) to execute R functions and display their output in Excel.