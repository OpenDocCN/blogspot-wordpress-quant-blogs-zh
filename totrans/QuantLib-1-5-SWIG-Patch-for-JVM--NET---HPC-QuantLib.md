<!--yml
category: 未分类
date: 2024-05-13 00:13:30
-->

# QuantLib-1.5 SWIG Patch for JVM/.NET – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2015/02/28/quantlib-1-5-swig-patch-for-jvm-net/#0001-01-01](https://hpcquantlib.wordpress.com/2015/02/28/quantlib-1-5-swig-patch-for-jvm-net/#0001-01-01)

Update 23.11.2015: A [modified version](https://wordpress.com/post/hpcquantlib.wordpress.com/1376) of the patch is now part of the official QuantLib Release 1.7.

Update 22.09.2015: Please find the latest and improved version of the patch for QuantLib 1.6.2 [here](https://hpcquantlib.wordpress.com/2015/09/20/quantlib-1-6-2-multithreading-patch-for-jvm-net/).

The usage of QuantLib in JVM and .NET languages (e.g. Java/Scala and C#/F#) via the SWIG interface has a known shortcoming. The implementation of QuantLib’s observer pattern does not tolerate a parallel garbage collector running in a different thread. As a result programs are randomly crashing or producing “pure virtual function calls”. A detailed description of this problem can be found e.g. [here](https://hpcquantlib.wordpress.com/2012/02/27/quantlib-swig-and-a-thread-safe-observer-pattern-in-c/) and within the references.

Please find [here](http://hpc-quantlib.de/src/observer15.zip) a patch for QuantLib 1.5 to fix this issue.