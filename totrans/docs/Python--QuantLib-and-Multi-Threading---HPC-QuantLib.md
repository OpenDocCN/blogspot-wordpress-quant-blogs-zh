<!--yml
category: 未分类
date: 2024-05-13 00:11:00
-->

# Python, QuantLib and Multi-Threading – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2021/11/29/python-quantlib-and-multithreading/#0001-01-01](https://hpcquantlib.wordpress.com/2021/11/29/python-quantlib-and-multithreading/#0001-01-01)

Python is – thanks to the [GIL](https://en.wikipedia.org/wiki/Global_interpreter_lock) – not the language of choice for modern multi-threading programming and also is QuantLib not really thread safe, even though the thread safe observer pattern implementation and the thread safe singleton initialization are helping to mitigate the risks (In short as a general advise do not share objects between threads, do not change global state like e.g. the evaluation date in an uncontrolled manner and enable QL_ENABLE_THREAD_SAFE_OBSERVER_PATTERN.).

Even then – other than in Java/Scala/C# or C++ – there is not much to gain in Python by default because the [SWIG](http://www.swig.org/) generated interface code will not release the GIL while running C++ code. Hence all threads except one will block when running long lasting QuantLib computations. But not all hope is lost, SWIG can be instructed to release the GIL before calling QuantLib methods with the command line parameter “-threads”. The only caveat here is that some of QuantLib’s SWIG interface files contain low level Python C API calls like e.g. Py_XDECREF. Every block with low level Python C API calls has to be guarded with the SWIG_PYTHON_THREAD_BEGIN_BLOCK macro at the beginning of the block to acquire the GIL, in total 60 times.

As a reward, the GIL will be released when running QuantLib code in Python and multi-threading can be used to speed-up multiple, long lasting QuantLib calls in the same manner as in the other languages.