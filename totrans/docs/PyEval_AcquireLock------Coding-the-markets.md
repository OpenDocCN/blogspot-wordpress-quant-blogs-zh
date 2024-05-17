<!--yml
category: 未分类
date: 2024-05-12 19:42:11
-->

# PyEval_AcquireLock( ) | Coding the markets

> 来源：[https://etrading.wordpress.com/2008/06/20/pyeval_acquirelock/#0001-01-01](https://etrading.wordpress.com/2008/06/20/pyeval_acquirelock/#0001-01-01)

## PyEval_AcquireLock( )

### June 20, 2008

The Python docs [explain](http://docs.python.org/api/threads.html) that PyEval_AcquireLock( ) shouldn’t be called more than once by the same thread: “if this thread already has the lock, a deadlock ensues”. I ran into this recently while coding with our C++/Python application framework. At work I’m fortunate enough to use an excellent proprietary C++ application framework specifically designed for building electronic trading systems.  It has pub/sub messaging, RPC, monitoring, failover, persistence, caching, versioning and logging all built in. While C++ is the native language of the framework, Java, C# and Python are also supported.

The Python support is implemented in CPython using the [Python C API](http://docs.python.org/api/api.html). C++ framework callbacks are dispatched into Python. Before and after dispatch the GIL was  acquired with PyEval_AcquireLock and released with PyEval_ReleaseLock. All well and good until a Python callback invokes a C++ function which in turn calls another Python function, causing a second call to PyEval_AcquireLock which then deadlocks. Not good if your process is handling an RFQ !

The solution was to use PyGILState_Ensure and PyGILState_Release, as introduced in Python 2.2, instead.