<!--yml

分类：未分类

日期：2024 年 05 月 18 日 06:16:29

-->

# 构建：Windows Runtime – .winmd 文件 | 交易台的传奇故事

> 来源：[`mdavey.wordpress.com/2011/09/14/build-windows-runtime-winmd-files/#0001-01-01`](https://mdavey.wordpress.com/2011/09/14/build-windows-runtime-winmd-files/#0001-01-01)

## 构建：Windows Runtime – .winmd 文件

首先，什么是 Windows Runtime？直接从 [Windows](http://msdn.microsoft.com/en-us/library/windows/apps/hh464947(v=VS.85).aspx) 开发中心：

> Windows Runtime 使用 API 元数据（.winmd 文件）暴露。这与 .NET 框架（Ecma-335）使用的格式相同。底层的二进制契约使您能够直接在您选择的开发语言中访问 Windows Runtime API。Windows Runtime API 的形状和结构可以被静态语言（如 C#）和动态语言（如 JavaScript）理解。在 JavaScript、C#、Visual Basic 和 C++ 中提供了 IntelliSense。

在 Windows 8 上，.winmd 文件位于 c:\Windows\System32\WinMetadata。如果您首先启动 .NET 反编译器，您可以打开文件并查看 WinRT 类型和类，以及 WinRT 本身引用的内容 - CLR。Windows.System 包含了 BUILD 主题演讲中显示的 Launcher，如果我没记错的话。

由 mdavey 于 2011 年 9 月 14 日发布。

发布于[未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签：[构建](https://mdavey.wordpress.com/tag/build/)，[微软](https://mdavey.wordpress.com/tag/microsoft/)
