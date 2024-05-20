<!--yml
category: 未分类
date: 2024-05-18 06:16:29
-->

# BUILD: Windows Runtime – .winmd files | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2011/09/14/build-windows-runtime-winmd-files/#0001-01-01](https://mdavey.wordpress.com/2011/09/14/build-windows-runtime-winmd-files/#0001-01-01)

## BUILD: Windows Runtime – .winmd files

First off what is the Windows Runtime? Straight off [Windows](http://msdn.microsoft.com/en-us/library/windows/apps/hh464947(v=VS.85).aspx) Dev Centre:

> The Windows Runtime is exposed using API metadata (.winmd files). This is the same format used by the .NET framework (Ecma-335). The underlying binary contract makes it easy for you to access the Windows Runtime APIs directly in the development language of your choice. The shape and structure of the Windows Runtime APIs can be understood by both static languages such as C# and dynamic languages such as JavaScript. IntelliSense is available in JavaScript, C#, Visual Basic, and C++.

The .winmd files on Windows 8 are located at c:\Windows\System32\WinMetadata. If you first up .NET Reflector you can open the files are have a look at the WinRT types and classes, coupled with what the WinRT references itself – the CLR. Windows.System contains the Launcher that was shown in some of the BUILD keynote code if I remember correctly.

~ by mdavey on September 14, 2011.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [BUILD](https://mdavey.wordpress.com/tag/build/), [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)