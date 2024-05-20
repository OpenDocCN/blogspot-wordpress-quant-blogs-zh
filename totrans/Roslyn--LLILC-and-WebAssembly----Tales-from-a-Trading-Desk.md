<!--yml
category: 未分类
date: 2024-05-18 05:41:07
-->

# Roslyn, LLILC and WebAssembly? | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/06/29/roslyn-llilc-and-webassembly/#0001-01-01](https://mdavey.wordpress.com/2015/06/29/roslyn-llilc-and-webassembly/#0001-01-01)

Given Joe Duffy’s [blog](http://joeduffyblog.com/) is so quite these days, its time to speculate.

The LLILC [announcement](http://www.dotnetfoundation.org/blog/announcing-llilc-llvm-for-dotnet) some months ago is interesting – a continued openness from Microsoft.  The main difference between Roslyn and LLILC, as provided by LLILC [github](https://github.com/dotnet/llilc/wiki/LLILC-FAQ) is:

> Roslyn provides frontend support, whilst LLILC (via LLVM) provides backend support:
> 
> Roslyn exposes the data structures of a frontend – so it’s ideal for building tools such as IDEs, with syntax coloring, warning squiggles, use/definition lookup, refactoring, etc; or translators that convert C# to some other language; or pretty-print formatters; or analyzers that check conformance with coding guidelines (think FxCop).
> 
> LLILC, via LLVM, exposes the data structures of a backend – so it’s ideal for building tools that inject extra code (eg: performance profiler, code tracer, debugger, parallelism analyzer, race detector); or super-optimizing code (eg: auto-vectorizer, auto-parallelizer); or test-case reduction.

The key in the above is the reference to [LLVM](http://blog.llvm.org/2015/04/llilc-llvm-based-compiler-for-dotnet.html), especially if you read “From ASM.JS to [WebAssembly](https://brendaneich.com/2015/06/from-asm-js-to-webassembly/)“, and then you read “WebAssembly LLVM [Backend](https://www.phoronix.com/scan.php?page=news_item&px=LLVM-WebAssembly-RFC) Being Discussed”.

Further, Brendan Eich’s recent interview on WebAssembly provides us with this:

> Microsoft has their own compiler so they’ll be doing wasm from a different compiler framework, but that’s great.

Given the LLILC work, it would be logically to leverage the LLVM to generate wasm

Interesting times.

~ by mdavey on June 29, 2015.

Posted in [.NET](https://mdavey.wordpress.com/category/languages/net/), [Languages](https://mdavey.wordpress.com/category/languages/)