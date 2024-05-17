<!--yml
category: 未分类
date: 2024-05-12 19:43:17
-->

# Python: mutability is the key | Coding the markets

> 来源：[https://etrading.wordpress.com/2008/04/28/python-mutability-is-the-key/#0001-01-01](https://etrading.wordpress.com/2008/04/28/python-mutability-is-the-key/#0001-01-01)

## Python: mutability is the key

### April 28, 2008

I’ve been coding in Python since 2000, so I surprised myself by discovering a gap in my coding knowledge this morning. Reading the [docs on sets](http://www.python.org/doc/2.4.1/lib/types-set.html), I came across: “The `set` type is mutable — the contents can be changed using methods like `add()` and `remove()`. Since it is mutable, it has no hash value and cannot be used as either a dictionary key or as an element of another set.”

I’d never realized that mutability decides whether an object can be a key. I guess I always just coded that way, with my keys generally being ints or strings, or tuples thereof.