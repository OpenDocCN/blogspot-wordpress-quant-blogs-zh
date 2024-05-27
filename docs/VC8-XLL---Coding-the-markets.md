<!--yml

类别：未分类

日期：2024-05-12 19:48:10

-->

# VC8 XLL | 编码市场

> 来源：[`etrading.wordpress.com/2007/03/25/vc8-xll/#0001-01-01`](https://etrading.wordpress.com/2007/03/25/vc8-xll/#0001-01-01)

## VC8 XLL

### 2007 年 3 月 25 日

所以如果你在 VC8 中构建一个 XLL，并且你使用一个.def 文件来指定导出的符号，请确保你给链接器提供一个/DEF:myaddin.xll 选项。与 VC6 链接器不同，VC8 不会自动识别.def 文件。我花了不少时间才搞清楚这个问题，使用 depends 和 filemon 来寻找缺失的依赖关系等等。始终以来，depends 告诉我我的 XLL 没有导出任何符号，但我却看不到，所以我专注于更微妙的可能问题。
