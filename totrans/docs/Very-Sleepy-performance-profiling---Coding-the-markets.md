<!--yml
category: 未分类
date: 2024-05-12 19:30:58
-->

# Very Sleepy performance profiling | Coding the markets

> 来源：[https://etrading.wordpress.com/2015/10/05/very-sleepy-performance-profiling/#0001-01-01](https://etrading.wordpress.com/2015/10/05/very-sleepy-performance-profiling/#0001-01-01)

## Very Sleepy performance profiling

### October 5, 2015

Recently I’ve been using the excellent [Very Sleepy profiler](https://github.com/VerySleepy/verysleepy) to performance tune the SpreadServeEngine’s loader, compiler and interpreter. One of our beta users had helpfully supplied a very large spreadsheet which was causing very long load and calc cycles. Back in the 90s you had to spend serious money on licenses for [Pure Software](https://en.wikipedia.org/wiki/Pure_Software)‘s Purify and Quantify tools for this kind of work. Now tools like [Dr Memory](http://www.drmemory.org/) and Very Sleepy are free and OSS. It’s a while since I did a real, systematic performance profiling and tuning exercise, and I was soon reminded of how quickly preconceptions about which parts of the code might be CPU hogs can be shattered. It wasn’t long before I was soon nose to nose with one of the eternal truths of C++ development, or indeed development in any language: malloc & free are expensive. That’s why the [LMAX team coded their own Java Collections](http://www.infoq.com/presentations/LMAX). Printf isn’t cheap either. The answer was to introduce memory pooling for many of the most heavily used compiler and interpreter classes, and to set up config switches for the interpreter tracing. Interpreter tracing needs to be available in release builds as it a tremendously useful way of looking inside the execution of your spreadsheet. The result was a thirty fold improvement in load time, and much snappier calc cycles on very large sheets.