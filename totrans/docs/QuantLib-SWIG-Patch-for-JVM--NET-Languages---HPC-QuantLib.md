<!--yml
category: 未分类
date: 2024-05-17 23:29:41
-->

# QuantLib-SWIG Patch for JVM/.NET Languages – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2014/05/11/quantlib-swig-patch-for-jvm-net-languages/#0001-01-01](https://hpcquantlib.wordpress.com/2014/05/11/quantlib-swig-patch-for-jvm-net-languages/#0001-01-01)

Update 23.11.2015: The latest version is now part of the official QuantLib Release 1.7.

Update 22.09.2015: Please find the latest and improved version of the patch for QuantLib 1.6.2 [here](https://hpcquantlib.wordpress.com/2015/09/20/quantlib-1-6-2-multithreading-patch-for-jvm-net/).

The usage of QuantLib in JVM and .NET languages (e.g. Java/Scala and C#/F#) via the SWIG interface has a known shortcoming. The implementation of QuantLib’s observer pattern does not tolerate a parallel garbage collector running in a different thread. As a result programs are randomly crashing or producing “pure virtual function calls”. A detailed description of this problem can be found e.g. [here](https://hpcquantlib.wordpress.com/2012/02/27/quantlib-swig-and-a-thread-safe-observer-pattern-in-c/) and within the references.

Please find [here](http://hpc-quantlib.de/src/observer.zip) a patch for QuantLib 1.4 to fix this issue. It contains

Installation instructions are included in the readme.txt file.