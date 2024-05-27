<!--yml

category: 未分类

date: 2024-05-18 08:10:31

-->

# 使用 MS Visual Basic 2010 创建 DLL 项目 | 量化角落

> 来源：[`quantcorner.wordpress.com/2011/03/28/creating-a-dll-project-with-ms-visual-basic-2010/#0001-01-01`](https://quantcorner.wordpress.com/2011/03/28/creating-a-dll-project-with-ms-visual-basic-2010/#0001-01-01)

我已经阅读了几本关于如何使用**MS Visual Studio**编写**DLL**的书籍。但是，大多数这些书实际上是基于旧版的 MS Visual Studio。对**Visual Studio 2010**（**VC10**）进行了改进（？），因此要创建**DLL 项目**所必须经过的窗口顺序与旧版的 MS Visual Studio 有所不同。这可能会令人困惑。

实际上，并不是那么复杂。想象一本描述如何使用旧版本的 Visual Studio 创建简单项目的教科书。如果你确实使用的是**VC10**，那么你需要按照以下步骤进行操作：

1)       **File** -> **Add** -> **New project …**

2)       在**Installed Templates**中，选择**Win32**，然后选择**Win32 Console Application**。在**Name :**字段中输入你的项目名称，然后点击**OK**。

3)       在**Welcome to the Win32 Application Wizard**面板上点击**Next**。

4)       在**Application Settings**中，选择**DLL**以及**Empty project**，然后点击**Finish**。

你已经完成了。现在，你可能会将至少两个文件添加到**Solution Explorer**中的**Source Files**文件夹中，在 VC10 中，这通常是一个***.cpp**文件和一个***.def**文件。对于后者，在**Code**模板中可以找到**Module Definition File**模板。
