<!--yml

分类：未分类

日期：2024-05-12 19:34:58

-->

# Python 传奇：赞美 GIL | 编码市场

> 来源：[`etrading.wordpress.com/2011/11/28/tales-on-python-in-praise-of-the-gil/#0001-01-01`](https://etrading.wordpress.com/2011/11/28/tales-on-python-in-praise-of-the-gil/#0001-01-01)

## Python 传奇：赞美 GIL

### 2011 年 11 月 28 日

在[Tales](http://mdavey.wordpress.com)的一篇最近帖子中，提到了 Python 逐渐受到重视的趋势。[近期帖子](http://mdavey.wordpress.com/2011/11/28/tier-1-sell-side-language-war-slang-vs-python-vs-scala/)中提到了几点回应：首先，Goldman 的 slang 非常接近 Python。据前 Goldmanites 说，slang 本来就与 Python 很相似。其次，Python 的全局解释器锁（GIL）。GIL 对于习惯了 C++、Java 和 C#等传统多线程环境的开发者来说，似乎总是一个劣势。从这种角度来看批评 Python 的人是正确的，他们指出 GIL 阻止了开发者在一个进程中实现并发性，因为它对 Python 运行时拥有的所有内存进行了锁定。这是一个真正的限制，但在处理混合语言环境时却有好处。例如，如果您正在使用 Python 的 C API 实现 C++的发布/订阅 API，您将需要一个回调机制来处理传入的消息。本地的发布/订阅 API 通常会在另一个线程上生成，在该线程上调度新的消息回调。当该线程调用回调实现时，回调实现可以调用 Python 代码，而不用担心锁定或互斥量，或者它是在主应用线程不同的线程上调用 Python 的 C API。这不是一个担忧，因为 GIL 将所有对 Python 内存的访问序列化。这大大简化了事情…
