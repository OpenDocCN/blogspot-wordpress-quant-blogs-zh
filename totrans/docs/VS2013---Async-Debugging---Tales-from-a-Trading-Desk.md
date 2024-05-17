<!--yml
category: 未分类
date: 2024-05-18 06:23:18
-->

# VS2013 – Async Debugging | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/06/28/vs2013-async-debugging/#0001-01-01](https://mdavey.wordpress.com/2013/06/28/vs2013-async-debugging/#0001-01-01)

## VS2013 – Async Debugging

VS2013 adds asynchronous [debugging](http://www.zdnet.com/microsoft-delivers-new-visual-studio-2013-and-net-4-5-1-previews-7000017336/) for C#, VB, JavaScript and C++ developers.  Somasegar’s [blog](http://blogs.msdn.com/b/somasegar/archive/2013/06/26/visual-studio-2013-preview.aspx) provide further details:

> Previously, it could be very difficult for a developer stopped at a breakpoint to know the asynchronous sequence of calls that brought them to the current location.  Now in Visual Studio 2013, the Call Stack window surfaces this information, factoring in new diagnostics information provided by the runtime.  Further, when an application stops making visible forward progress, it’s often difficult to diagnose and to understand what asynchronous operations are currently in flight such that their lack of completion might be causing the app to hang.  In Visual Studio 2013, the Tasks window (formerly called Parallel Tasks in Visual Studio 2010 and Visual Studio 2012) now includes details on these async operations so that you can break into your app in the debugger and easily see and navigate to everything that’s in flight.

Very cool

![](img/5cde04a47164aafb05521d6cf6a77edd.png)

~ by mdavey on June 28, 2013.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)