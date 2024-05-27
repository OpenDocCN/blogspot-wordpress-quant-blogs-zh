<!--yml

分类：未分类

日期：2024 年 05 月 12 日 19:45:33

-->

# has_key 和 ContainsKey | 编码市场

> 来源：[`etrading.wordpress.com/2007/10/11/has_key-containskey/#0001-01-01`](https://etrading.wordpress.com/2007/10/11/has_key-containskey/#0001-01-01)

## has_key 和 ContainsKey

### 2007 年 10 月 11 日

Python 内置的字典类型 - {} - 有一个 has_key 方法。C#的 System.Collections.Hashtable 有 ContainsKey 方法。我希望相同的 Python 代码能够在字典和哈希表上运行。幸运的是，IronPython 将 ContainsKey 方法添加到了内置字典类型中，因此简单地用 ContainsKey 替换 has_key 的调用就能解决问题。
