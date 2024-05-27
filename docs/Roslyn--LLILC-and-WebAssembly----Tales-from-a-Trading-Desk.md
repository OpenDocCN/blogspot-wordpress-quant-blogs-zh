<!--yml

分类：未分类

日期：2024-05-18 05:41:07

-->

# Roslyn、LLILC 和 WebAssembly？| 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2015/06/29/roslyn-llilc-and-webassembly/#0001-01-01`](https://mdavey.wordpress.com/2015/06/29/roslyn-llilc-and-webassembly/#0001-01-01)

鉴于 Joe Duffy 的[博客](http://joeduffyblog.com/)最近非常安静，是时候进行猜测了。

LLILC [公告](http://www.dotnetfoundation.org/blog/announcing-llilc-llvm-for-dotnet)几个月前很有趣——微软持续的开放态度。Roslyn 和 LLILC 的主要区别，根据 LLILC[github](https://github.com/dotnet/llilc/wiki/LLILC-FAQ)提供的信息是：

> Roslyn 提供前端支持，而 LLILC（通过 LLVM）提供后端支持：
> 
> Roslyn 暴露了前端的数据结构——所以它非常适合构建诸如 IDE 之类的工具，具有语法高亮、警告波浪线、用法/定义查找、重构等功能；或者转换 C#至其他语言的转换器；或者美化格式化器；或者检查代码指南一致性的分析器（想想 FxCop）。
> 
> LLILC 通过 LLVM 暴露了后端的数据结构——所以它非常适合构建注入额外代码的工具（例如：性能分析器、代码跟踪器、调试器、并行性分析器、竞争检测器）；或者超优化代码（例如：自动向量化器、自动并行化器）；或者测试用例减少。

上述关键在于对[LLVM](http://blog.llvm.org/2015/04/llilc-llvm-based-compiler-for-dotnet.html)的引用，特别是如果你阅读了“从 ASM.JS 到[WebAssembly](https://brendaneich.com/2015/06/from-asm-js-to-webassembly/)”这篇文章，然后你又阅读了“WebAssembly LLVM [后端](https://www.phoronix.com/scan.php?page=news_item&px=LLVM-WebAssembly-RFC)正在讨论中”。

此外，Brendan Eich 关于 WebAssembly 的最新采访为我们提供了以下内容：

> 微软有自己的编译器，所以他们将会用不同的编译器框架来处理 wasm，但这很好。

鉴于 LLILC 的工作，逻辑上应该利用 LLVM 来生成 wasm

有趣的时代。

~ mdavey 于 2015 年 6 月 29 日。

发布在[.NET](https://mdavey.wordpress.com/category/languages/net/)、[语言](https://mdavey.wordpress.com/category/languages/)
