<!--yml

类别：未分类

日期：2024-05-18 08:07:48

-->

# QuantLib 在 Visual Studio Express 2013 中的安装 | Quant Corner

> 来源：[`quantcorner.wordpress.com/2015/05/07/quantlib-installation-in-visual-studio-express-2013/#0001-01-01`](https://quantcorner.wordpress.com/2015/05/07/quantlib-installation-in-visual-studio-express-2013/#0001-01-01)

假设***VS2013 Express***已经在你的机器上安装好了（它可以从[这里](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx "Microsoft Visual Studio")下载）。编译***QuantLib***（简称***QL***）需要一个工作的***Boost***安装。我们将首先从安装***Boost***库开始。

# **Boost 下载及安装**

**Boost**项目现在提供了二进制文件，使得安装过程变得无痛。

（1）访问[`sourceforge.net/projects/boost/files/boost-binaries`](http://sourceforge.net/projects/boost/files/boost-binaries)，

（2）选择与你希望下载和安装的版本对应的**Boost**文件（我们将使用**Boost 1.57.0**，见下文）。

（3）选择与你的编译器和平台相对应的安装程序。

（4）在你的机器上下载安装程序并运行它。

在以下内容中，***Boost 1.57.0***已安装在 C:\Boost\boost_1_57_0 文件夹中。

**QuantLib 下载及安装**

（1）访问[`sourceforge.net/projects/quantlib/files`](http://sourceforge.net/projects/quantlib/files "sourceforge.quantlib")。

（2）下载***QL***（截至编写时最新版本为***QL 1.5***）。

***QL***已安装在 C:\QuantLib-1.5 文件夹中。

（3）启动 VC++，文件 > 打开文件… > C:\QuantLib-1.5\QuantLib_vc12.sln。你将在 VS2013 的“解决方案资源管理器”窗口中看到 Quantlib_vc12 和它包含的 19 个项目。

（4）打开***VS2013***的*属性管理器*窗口，按照视图 > 其他窗口… > 属性管理器。在*属性管理器*中，选择*QuantLib*并展开它。它将显示构建*模式/平台*节点。

（5）选择你希望用***QL***构建的构建模式/平台，例如展开节点*Debug | x64*并选择内部的*Microsoft.Cpp.x64.User*。

![Visual Studio - QuantLib - 属性管理器](https://quantcorner.wordpress.com/wp-content/uploads/2015/05/installing_quantlib_vs2013_1.jpg)

VS2013 的“属性管理器”窗口，同时选择多个解决方案配置

（6）然后右键点击，在上下文菜单中选择*属性*。将弹出*属性页*。点击*VC++目录*标签。

（7）在*包含目录*中，添加 C:\Boost\boost_1_57_0。

（8）在“库目录”中，添加 C:\Boost\boost_1_57_0\libs。

（9）点击*应用*，然后*确定*以关闭*属性页*窗口。

(10) 现在，选择你想要的配置，例如*发布*模式和 x64。回到*解决方案资源管理器*。在*解决方案资源管理器*中选择**Quantlib_vc12 解决方案**，右键点击并选择*构建*。此时，***QL*** 将开始构建。

注意：官方***QL** *安装文档可以在此处找到[这里](http://quantlib.org/install/vc10.shtml "QuantLib 安装文档")。我们之前在此处[这里](https://quantcorner.wordpress.com/2012/11/13/installing-quantlib-for-vc11-windows/ "在 VC11 上安装 Quantlib")写了关于这个话题的内容。
