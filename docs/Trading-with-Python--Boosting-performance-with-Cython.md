<!--yml

类别：未分类

日期：2024-05-18 15:42:14

-->

# Trading with Python：使用 Cython 提高性能

> 来源：[`tradingwithpython.blogspot.com/2014/06/even-with-my-old-pc-amd-athlon-ii-3gb.html#0001-01-01`](http://tradingwithpython.blogspot.com/2014/06/even-with-my-old-pc-amd-athlon-ii-3gb.html#0001-01-01)

即使在我的旧电脑上（AMD Athlon II，3GB 内存），运行向量化代码时也很少遇到性能问题。但不幸的是，有许多情况无法轻松地向量化，例如

*drawdown*

函数。我实现的此类函数极其缓慢，因此我决定将其作为提高速度的测试用例。我将使用大约 5k 个样本的 SPY 时间序列作为测试数据。下面是我在上述博客中提到的原始版本。

*drawdown*

函数（如现在在

*TradingWithPython*

库中实现）

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

Hmm 1.2 秒对于这样一个简单的函数来说并不是太快。有些东西可能会对性能产生很大的影响，比如每次循环迭代都在追加的列表*highwatermark*。通过索引访问 Series 也应该涉及一些不必要的处理。让我们看看当这个函数被重写以使用 numpy 数据时会发生什么。

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

嗯，这是

**很多**

比原始函数快，大约提高了 40 倍的运行速度。仍有很大的改进空间，通过移动到编译代码来实现。

*[cython](http://cython.org/)*

现在我用上面提到的 dd 函数重写，但使用我在

[cython 教程](http://docs.cython.org/src/tutorial/numpy.html)

上找到的优化提示。注意，这是我用 Cython 优化函数的第一次尝试。

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

哇，这个版本在 122

*micro*

秒，使其

**十万**

比我的原始版本快很多倍！我必须说我对 Cython 和 IPython 团队所取得的成就印象深刻！速度与易用性之间的比较真是太棒了！

P.S. 我以前在 Matlab 中使用纯 C 和.mex 包装进行代码优化，这和现在比起来就是小菜一碟。
