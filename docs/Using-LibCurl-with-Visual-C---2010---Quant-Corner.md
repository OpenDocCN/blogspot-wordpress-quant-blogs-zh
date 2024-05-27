<!--yml

分类：未分类

日期：2024-05-18 08:08:26

-->

# Using LibCurl with Visual C++ 2010 | Quant Corner

> 来源：[`quantcorner.wordpress.com/2012/04/08/using-libcurl-with-visual-c-2010/#0001-01-01`](https://quantcorner.wordpress.com/2012/04/08/using-libcurl-with-visual-c-2010/#0001-01-01)

我曾经一段时间困在**LibCurl**和**Visual C++ 2010**（**VC10**）上。在**[Curl](http://curl.haxx.se/libcurl/ "Curl")**项目网站上的文档[**Using libcurl in Visual Studio**](http://curl.haxx.se/libcurl/c/visual_studio.pdf "Using libcurl in Visual Studio")并没有提供太多帮助（注意它追溯到 2002 年）。我在互联网上寻找线索，但找不到“正确”的解决方案。与此同时**对我的自尊心有益**，我意识到我不是唯一一个遇到困难的人。😉

以下是我在**VC10**（在 32 位机器上）使**LibCurl**工作的方法。

首先，下载**VC10**的最新版**LibCurl** [这里](http://curl.haxx.se/latest.cgi?curl=win32-ssl-devel-msvc "here")。

现在，创建一个新的 C++项目。

（以下内容假设解决方案是在**Debug mode**构建的，但很容易推导出针对**Release mode**的步骤。）

首先去**Properties > Configuration Properties > VC++ Directories > Include directories**。在这里，添加**curl**目录，该目录位于解压后的**Libcurl**文件的**include directory**中（C:\ … \libcurl-7.19.3-win32-ssl-msvc\include\curl）。

现在去**VC++ Directories > Library directories**。添加包含**curllib_static.lib**, **curllib.dll**和**curllib.lib**的**Debug**目录（C:\Users\Édouard\Documents\Visual Studio 2010\LibCurl\lib\Debug）。

仍然在**Configuration Properties**，去**Linker > Input > Additional Dependencies**。在这里，你必须添加**curllib.lib 文件**（C:\ … \lib\Debug\curllib.lib）。输入 lib 文件的名称。

下一步是向你的项目的**Debug directory**中添加**curllib.dll**, **libeay32.dll**, **openldap.dll**和**ssleay32.dll**。所有这些都可以在**Libcurl**的根目录中找到。你还需要在这个目录中添加**libsasl.dll**。只需谷歌搜索即可。

（这不应该是最先一步吗？）现在，打开**curl.h**文件。将#include «curl/curlbuild.h»替换为#include «curlbuild.h».

你完成了。
