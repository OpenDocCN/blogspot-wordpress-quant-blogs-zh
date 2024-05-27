<!--yml

分类: 未分类

日期: 2024-05-12 19:36:08

-->

# 调试 Twisted Matrix 网络代码 | 编码市场

> 来源：[`etrading.wordpress.com/2011/01/24/debugging-twisted-matrix-networking-code/#0001-01-01`](https://etrading.wordpress.com/2011/01/24/debugging-twisted-matrix-networking-code/#0001-01-01)

## 调试 Twisted 网络代码

### 2011 年 1 月 24 日

调试 Twisted 代码是一种横向思维的练习。错误消息和异常可能会很模糊，特别是当包含在 Deferred 中的代码失败时。当在 Deferred 内部收到未处理的错误时，请检查您的代码是否存在基本错误：参数不匹配、对未定义变量的引用或未导入的类型或模块等等。并且在从 Twisted 基类派生时，请检查您是否意外地覆盖了成员变量。例如，不要有一个名为 'clients' 的成员变量！
