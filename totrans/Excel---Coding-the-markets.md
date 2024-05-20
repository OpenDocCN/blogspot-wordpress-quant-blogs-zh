<!--yml
category: 未分类
date: 2024-05-12 19:31:59
-->

# Excel | Coding the markets

> 来源：[https://etrading.wordpress.com/excel/#0001-01-01](https://etrading.wordpress.com/excel/#0001-01-01)

**Stuff you’ll need to know when coding an Excel Add In for a trader in C++**

Excel Add Ins are a special kind of DLL – an XLL – that exports certain function signatures that Excel expects to find. For example xlAutoOpen, xlAutoClose and xlAddInManagerInfo. Coding an XLL means you can implement worksheet functions and commands in C++. Worksheet functions can be called from Excel formulae, and commands can be invoked from menu items you can add to the Excel menubar in initialisation code. To get to grips with all this you need…

*   The MS Excel 97 SDK – get it [here](http://support.microsoft.com/default.aspx?scid=kb;EN-US;152152). Download Frmwrk32.exe. Essentially the SDK is two files: xlcall.h and xlcall32.lib.
*   You need a copy of Steve Dalton’s [Excel add-in development in C/C++.](http://www.amazon.co.uk/exec/obidos/ASIN/0470024690) Don’t skimp on spending the 40 quid, you do really need this book.
*   Another MS knowledgebase [article](http://support.microsoft.com/kb/178474/EN-US/) giving a simple example of an XLL. This will give you some boilerplate code to get started.

If you want to get real time data into your worksheet, you’ll have to master the mysteries of DDE, or else go the Excel RTD route. I haven’t done RTD, so won’t comment here. I have done DDE. Here’s a [useful starting point](http://support.microsoft.com/?kbid=279721).

Why do we need DDE ? Because you can only do this…

Excel4( xlSet, &xRet, 2, (LPXLOPER)&xRef, (LPXLOPER)&xValue);

…from Excel’s own main thread. That is, you can only make that call when Excel has called you, and you’re in the stack context of a worksheet function you have supplied. When you’re pushing real time data into a worksheet, you’re typically getting a callback on another thread from your pub/sub messaging API – TIB RV or whatever. You can’t call the Excel API from that thread, so you use DDE to put a Windows message on Excel’s message queue, which will hopefully be picked up quite soon by Excel’s main event loop. There’s no reason why you can’t have more than one thread operating inside your Excel process, executing the code in your add in. So long as your code is threadsafe, of course ! So your message handling callback will make the DDE call to post to Excel’s main thread.

Bearing that in mind, there are some guidelines you should follow…

*   Always remember that Excel is effectively single threaded.
*   You should only have one real time data source per Excel process. For a pricing sheet, that might mean only one futures contract. Don’t attempt to have two sheets driven by two futures contracts in the same Excel instance: Excel’s recalcs will be slower.
*   If your sheet does a lot of calcs in response to an incoming tick, you’ll need a throttling mechanism that’s aware of your calc cycle. Otherwise you may find yourself starting a new calc cycle before the last one ended !
*   And look out for string pooling. If you’re doing a release build with /GF, you may get the “not a valid add-in” message box. This [KB article](http://support.microsoft.com/kb/824459) desribes the issue and workaround.

When you’ve got your addin and pricing or risk sheet running, and you want to serverize it, take a look at [SpreadServe](http://spreadserve.com).

**Some other useful content**