<!--yml
category: 未分类
date: 2024-05-18 15:42:14
-->

# Trading with Python: Boosting performance with Cython

> 来源：[http://tradingwithpython.blogspot.com/2014/06/even-with-my-old-pc-amd-athlon-ii-3gb.html#0001-01-01](http://tradingwithpython.blogspot.com/2014/06/even-with-my-old-pc-amd-athlon-ii-3gb.html#0001-01-01)

Even with my old pc (AMD Athlon II, 3GB ram), I seldom run into performance issues when running vectorized code. But unfortunately there are plenty of cases where that can not be easily vectorized, for example the

*drawdown*

 function. My implementation of such was extremely slow, so I decided to use it as a test case for speeding things up. I'll be using the SPY timeseries with ~5k samples as test data. Here comes the original version of my

*drawdown*

 function (as it is now implemented in the

*TradingWithPython*

library)

```
def drawdown(pnl):
    """
    calculate max drawdown and duration

    Returns:
        drawdown : vector of drawdwon values
        duration : vector of drawdown duration
    """
    cumret = pnl

    highwatermark = [0]

    idx = pnl.index
    drawdown = pd.Series(index = idx)
    drawdowndur = pd.Series(index = idx)

    for t in range(1, len(idx)) :
        highwatermark.append(max(highwatermark[t-1], cumret[t]))
        drawdown[t]= (highwatermark[t]-cumret[t])
        drawdowndur[t]= (0 if drawdown[t] == 0 else drawdowndur[t-1]+1)

    return drawdown, drawdowndur

%timeit drawdown(spy)
1 loops, best of 3: 1.21 s per loop

```

Hmm 1.2 seconds is not too speedy for such a simple function. There are some things here that could be a great drag to performance, such as a list *highwatermark* that is being appended on each loop iteration. Accessing Series by their index should also involve some processing that is not strictly necesarry. Let's take a look at what happens when this function is rewritten to work with numpy data

```
def dd(s):
#    ''' simple drawdown function '''

    highwatermark = np.zeros(len(s))
    drawdown = np.zeros(len(s))
    drawdowndur = np.zeros(len(s))

    for t in range(1,len(s)):
        highwatermark[t] = max(highwatermark[t-1], s[t])
        drawdown[t] = (highwatermark[t]-s[t])
        drawdowndur[t]= (0 if drawdown[t] == 0 else drawdowndur[t-1]+1)

    return drawdown , drawdowndur

%timeit dd(spy.values)
10 loops, best of 3: 27.9 ms per loop

```

Well, this is

**much**

 faster than the original function, approximately 40x speed increase. Still there is much room for improvement by moving to compiled code with

*[cython](http://cython.org/)*

 Now I rewrite the dd function from above, but using optimisation tips that I've found on the

[cython tutorial](http://docs.cython.org/src/tutorial/numpy.html)

. Note that this is my first try ever at optimizing functions with Cython.

```
%%cython
import numpy as np
cimport numpy as np

DTYPE = np.float64
ctypedef np.float64_t DTYPE_t

cimport cython
@cython.boundscheck(False) # turn of bounds-checking for entire function
def dd_c(np.ndarray[DTYPE_t] s):
#    ''' simple drawdown function '''
    cdef np.ndarray[DTYPE_t] highwatermark = np.zeros(len(s),dtype=DTYPE)
    cdef np.ndarray[DTYPE_t] drawdown = np.zeros(len(s),dtype=DTYPE)
    cdef np.ndarray[DTYPE_t] drawdowndur = np.zeros(len(s),dtype=DTYPE)

    cdef int t
    for t in range(1,len(s)):
        highwatermark[t] = max(highwatermark[t-1], s[t])
        drawdown[t] = (highwatermark[t]-s[t])
        drawdowndur[t]= (0 if drawdown[t] == 0 else drawdowndur[t-1]+1)

    return drawdown , drawdowndur

%timeit dd_c(spy.values)
10000 loops, best of 3: 121 µs per loop

```

Wow, this version runs in 122

*micro*

seconds, making it

**ten thousand**

 times faster than my original version! I must say that I'm very impressed by what the Cython and IPython teams have achieved! The speed compared with ease of use is just awesome!

 P.S. I used to do code optimisations in Matlab using pure C and .mex wrapping, it was all just pain in the ass compared to this.