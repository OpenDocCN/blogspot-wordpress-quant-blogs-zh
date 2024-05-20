<!--yml
category: 未分类
date: 2024-05-17 23:29:47
-->

# QuantLib-SWIG and a Thread-Safe Observer Pattern in C++ – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2012/02/27/quantlib-swig-and-a-thread-safe-observer-pattern-in-c/#0001-01-01](https://hpcquantlib.wordpress.com/2012/02/27/quantlib-swig-and-a-thread-safe-observer-pattern-in-c/#0001-01-01)

Update 23.11.2015: A modified version of the patch is now part of the official QuantLib Release 1.7.

Update 28.02.2015: Please find the latest version of the patch for QuantLib 1.5 [here](http://hpc-quantlib.de/src/observer15.zip).

Update 11.05.2014: Please find the latest version of the patch for QuantLib 1.4 [here](http://hpc-quantlib.de/src/observer.zip).

The [QuantLib](http://www.quantlib.org) library is not really thread-safe. Successful usage in multi-core and parallel environments is often achieved by message passing between multiple processes rather than shared memory and multi-threading. If different threads are acting on distinct objects then QuantLib can also be used in the multi-threading environment (define QL_ENABLE_SESSIONS to make the singletons thread dependent.).

If you are using QuantLib in Java or Scala via SWIG [1] then the QuantLib routines are automatically executed in a multi-threading environment even if your main routine is single threaded. The garbage collector of the JVM is usually running in different thread. In conjunction with QuantLib’s implementation of the Observer pattern this can lead to serious problems, e.g. the following single threaded Scala code crashes on a multi-core computer after a short period of time.

```
import org.quantlib.{Array => QArray, _}
object ObserverTest {
    def main(args: Array[String]) : Unit = {
        System.loadLibrary("QuantLibJNI");
        val aSimpleQuote = new SimpleQuote(0)

        while (true) {
            (0 until 10).foreach(_ => {
                new QuoteHandle(aSimpleQuote)
                aSimpleQuote.setValue(aSimpleQuote.value + 1)
            })
            System.gc
        }
    }
}
```

The garbage collector might call the destructor of an observer (QuoteHandle) at the same point in time when the update method on the same object is invoked by aSimpleQuote.setValue. (Find [here](http://old.nabble.com/Issues-with-C--Swig-Bindings,-NUnit-and-Settings.instance%28%29.setEvaluationDate%28%29-td30549787.html) the original postings on the QuantLib mailing list regarding this problem.). For a greenfield project the author in [2] has a nice solution for this problem in C++. Unfortunately this solution can not be applied to the QuantLib because the solution involves a change of signature of the Observer interface and thereafter would lead to a lot of change in the QuantLib library.

The main problem here is that we have to disable the Observer before the destructor starts to work. This could in theory be achieved by adding a special “Deleter” to every new instance of a boost::shared_ptr. But again this would lead to a lot of changes in the library.

When compiled with the preprocessor directive BOOST_SP_ENABLE_DEBUG_HOOKS the boost library adds a callback hook before a destructor is called by any boost smart pointer. This hook can be utilized to disable an Observer before the actual destructor is executed. In addition the boost::signals2 library [3] provides a simple and thread-safe notification mechanism.

The corresponding thread-safe implementation of the original QuantLib Observer/Observable interface can be found [here](http://hpc-quantlib.de/src/observable.zip). Set the preprocessor directive BOOST_SP_ENABLE_DEBUG_HOOKS for every source file. Replace/Add the files observable.hpp and observable.cpp and recompile the QuantLib library and the QuantLib-SWIG module.

Note: if you want to use the patch with QL 1.2 and not for the trunk, please see the comment by gk below.

[1] Simplified Wrapper and Interface Generator, [SWIG](http://swig.sourceforge.net/)

[2] Shuo Chen, [Where Destructors meet Threads](http://www.slideshare.net/chenshuo/where-destructors-meet-threads)

[3] Douglas G., Mori Hess F., [Boost.Signals2](http://www.boost.org/doc/libs/1_48_0/doc/html/signals2.html)