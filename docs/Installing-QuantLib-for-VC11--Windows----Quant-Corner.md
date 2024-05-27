<!--yml

类别：未分类

date: 2024-05-18 08:08:53

-->

# Installing QuantLib for VC11 (Windows) | Quant Corner

> 来源：[`quantcorner.wordpress.com/2012/11/13/installing-quantlib-for-vc11-windows/#0001-01-01`](https://quantcorner.wordpress.com/2012/11/13/installing-quantlib-for-vc11-windows/#0001-01-01)

以下是在运行于**Windows**（32 位）的电脑上安装和使用**QuantLib 1.2**用于**VC11**的说明。我们只会安装**QuantLib**的核心库，即解决方案文件中的 15 个项目中的只有 1 个。因此，我们只需要**Boost**的头文件。无需安装**Boost**库。

**(I) 要求**

**a)** 你的电脑上必须有**VC11**环境，即 Visual Studio 11 Beta、Visual Studio 2012、Visual C++ 2012 Express 等。

**b)** **Boost**库可以在这里[下载](http://www.boost.org/users/download/)。目前可用的最新版本是**Boost 1.52.0**。

**c)** **QuantLib**库。**VC11**的**QuantLib 1.2.1**解决方案文件可以从一篇[之前的帖子](https://quantcorner.wordpress.com/2012/10/28/quantlib-1-2-with-vc11/)下载。

**(II) 构建 QuantLib**

我们将会在**Visual Studio**中以调试模式构建解决方案。在这里，请按照即将到来的安装步骤来以任何其他模式（例如，以发布模式）构建**QuantLib**。从现在开始，我们假定**(I)**中的所有要求都是没有问题的。

**a)** 在你的图形用户界面（GUI）中或者直接通过双击文件，打开名为 QuantLib_vc11.sln 的解决方案文件（*… \QuantLib-1.2.1\ QuantLib_vc11.sln*）。这将打开解决方案中的 15 个项目（见下面的图片）。

![vc11 1](https://quantcorner.wordpress.com/wp-content/uploads/2012/11/vc11-1.jpg)

**b)** 确保“QuantLib”项目被选中，即在“解决方案资源管理器”面板中突出显示。然后，在上下文菜单中右键点击并选择“属性”。

**c)** 将文件夹*… \boost_1_52*的路径添加到*配置属性/*VC++ 目录/包含目录*。然后，将文件夹*… \boost_1_52\libs*的路径添加到配置属性/*VC++ 目录/库目录*（见下面的加粗图片）。显然，你需要点击“应用”以使你的更改生效。

![vc11 2](https://quantcorner.wordpress.com/wp-content/uploads/2012/11/vc11-2.jpg)

**d)** 现在，在“QuantLib 属性页面”面板中，将*配置属性/*C/C++/*预编译头/预编译头*项设置为“不使用预编译头”。

![vc11 3](https://quantcorner.wordpress.com/wp-content/uploads/2012/11/vc11-3.jpg)

-   **f)** 在 ‘Solution Explorer’ 面板上，右键点击 ‘Solution_vc11’（15 个项目）’，选择 ‘Properties’。在 *Configuration Properties/Configuration* 中，取消选择所有 ‘Build’ 中的项目，只留下 ‘QuantLib’ 项目。

![](https://quantcorner.wordpress.com/wp-content/uploads/2012/11/vc11-4.jpg)

-   **g)** 现在，再次在 ‘Solution Explorer’ 面板上点击 ‘Solution_vc11’（15 个项目）’，然后点击 ‘Build Solution’。或者，可以按下 F7 键。构建过程应该会开始。

-   编译过程中可能会出现警告信息，但这并不是真正的问题。

-   **(III) QuantLib 使用**

-   **a)** 每次你编写的 C++ 程序依赖于 **QuantLib** 库时，你都需要按照上面步骤 **(II,c)** 的所示，让你的项目能够看到 *… \boost_1_52* 和 *… \boost_1_52\libs* 文件夹。

-   **b)** 然后，将 *… /QuantLib-1.2.1* 文件夹的路径添加到 Configuration Properties/*C/C++/General/Additional Include Directories*。

![](https://quantcorner.wordpress.com/wp-content/uploads/2012/11/vc11-5.jpg)

-   **c)** 最后，将 *… /QuantLib-1.2.1/lib* 文件夹的路径添加到 Configuration Properties/*Librarian/General*。

![](https://quantcorner.wordpress.com/wp-content/uploads/2012/11/vc11-61.jpg)

-   或者，可以让步骤 **(III, a)** 和 **(III, b)** 更简单一些，一次性指定 **QuantLib** 所需的全部目录，例如，通过指定一个 [每用户目录列表](http://msdn.microsoft.com/en-us/library/vstudio/ee855621.aspx "Per-user directory list")，或者你喜欢的任何其他方法*****。

-   ****** 感谢 **Polter** 在 Wilmott 论坛上的评论。*
