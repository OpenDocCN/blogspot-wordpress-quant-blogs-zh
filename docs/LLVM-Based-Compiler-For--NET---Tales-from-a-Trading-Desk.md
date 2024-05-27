<!--yml

分类：未分类

日期：2024-05-18 05:42:58

-->

# LLVM-Based Compiler For .NET | Tales from a Trading Desk

> 来源：[`mdavey.wordpress.com/2015/04/14/llvm-based-compiler-for-net/#0001-01-01`](https://mdavey.wordpress.com/2015/04/14/llvm-based-compiler-for-net/#0001-01-01)

## LLVM-Based Compiler For .NET

微软（**Microsoft**）正在某种程度上拥抱开源。2015 年以[CoreCLR](http://www.phoronix.com/scan.php?page=news_item&px=Microsoft-Open-Source-CoreCLR)的开源开始——CoreCLR 是.NET 应用的执行引擎，负责.NET 的编译到机器码、垃圾回收和其他核心功能。

现在，我们听说 Russell Hadley 在 LLVM 的[邮件列表](http://lists.cs.uiuc.edu/pipermail/llvmdev/2015-April/084459.html)上提到[微软](http://www.phoronix.com/scan.php?page=news_item&px=Microsoft-LLVM-dotNET-LLILC)有一个新的努力来：

> 基于[LLVM](https://github.com/dotnet/llilc/wiki)产生 MSIL 代码生成器，针对开源的.NET CoreCLR
> 
> 这个新的 JIT 将允许任何为.NET Core 类库编写的 C#程序在任何可以移植 CoreCLR 并且[LLVM](http://lists.cs.uiuc.edu/pipermail/llvmdev/2015-April/084459.html)将针对的平台运行。

~ mdavey 于 2015 年 4 月 14 日发表。

发表于：[.NET](https://mdavey.wordpress.com/category/languages/net/)分类
