<!--yml
category: 未分类
date: 2024-05-12 19:34:58
-->

# Tales on Python: in praise of the GIL | Coding the markets

> 来源：[https://etrading.wordpress.com/2011/11/28/tales-on-python-in-praise-of-the-gil/#0001-01-01](https://etrading.wordpress.com/2011/11/28/tales-on-python-in-praise-of-the-gil/#0001-01-01)

## Tales on Python: in praise of the GIL

### November 28, 2011

[Tales](http://mdavey.wordpress.com) notes the trend towards Python in a [recent post](http://mdavey.wordpress.com/2011/11/28/tier-1-sell-side-language-war-slang-vs-python-vs-scala/). Couple of points in response: firstly, slang at Goldman. I’m told by ex Goldmanites that slang is very close to Python anyway. Secondly, Python’s Global Interpreter Lock. The GIL always seems a disadvantage to developers accustomed to ‘traditional’ multi-threaded environments like C++, Java and C#. Those who criticise Python from that perspective are right to point out that the GIL prevents developers from achieving concurrency within a single process, because it puts locking around access to all memory owned by the Python runtime. That is a real constraint, but one that has benefits when dealing with mixed language environments. For example, if you’re implementing a pub sub API in C++ using Python’s C API, you’ll want a callback mechanism to handle incoming messages. Native pub sub APIs typically spawn another thread on which they dispatch new message callbacks. When that thread invokes the callback implementation, the callback implementation can invoke Python code without worrying about locking or mutexes or the fact that it’s invoking Python’s C API on a different thread than the main app thread. It’s not a concern, because the GIL serializes all access to Python’s memory. Which simplifies things hugely…