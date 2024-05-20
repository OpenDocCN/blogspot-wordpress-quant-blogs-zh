<!--yml
category: 未分类
date: 2024-05-18 05:42:58
-->

# LLVM-Based Compiler For .NET | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/04/14/llvm-based-compiler-for-net/#0001-01-01](https://mdavey.wordpress.com/2015/04/14/llvm-based-compiler-for-net/#0001-01-01)

## LLVM-Based Compiler For .NET

The NEW [Microsoft](http://blogs.msdn.com/b/dotnet/archive/2015/02/03/coreclr-is-now-open-source.aspx) is somewhat embracing Open Source.  2015 started with the [CoreCLR](http://www.phoronix.com/scan.php?page=news_item&px=Microsoft-Open-Source-CoreCLR) being open [sourced](http://blogs.msdn.com/b/dotnet/archive/2015/02/03/coreclr-is-now-open-source.aspx) – the CoreCLR is the execution engine for .NET apps and performs compilation to machine code, garbage collection, and other core functionality to .NET.

Today,we hear that Russell Hadley on the LLVM [mailing](http://lists.cs.uiuc.edu/pipermail/llvmdev/2015-April/084459.html) list that [Microsoft](http://www.phoronix.com/scan.php?page=news_item&px=Microsoft-LLVM-dotNET-LLILC) has a new effort to

> Produce MSIL code generators based on [LLVM](https://github.com/dotnet/llilc/wiki) and targeting the open source dotnet CoreCLR

> This new JIT will allow any C# program written for the .NET Core class libraries to run on any platform that CoreCLR can be ported to and that [LLVM](http://lists.cs.uiuc.edu/pipermail/llvmdev/2015-April/084459.html) will target.

~ by mdavey on April 14, 2015.

Posted in [.NET](https://mdavey.wordpress.com/category/languages/net/)