<!--yml
category: 未分类
date: 2024-05-18 08:10:31
-->

# Creating a DLL project with MS Visual Basic 2010 | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2011/03/28/creating-a-dll-project-with-ms-visual-basic-2010/#0001-01-01](https://quantcorner.wordpress.com/2011/03/28/creating-a-dll-project-with-ms-visual-basic-2010/#0001-01-01)

I’ve got through several books on how to write **DLL**s with **MS Visual Studio**. But, most of those books are actually based on old MS Visual Studio versions. Improvements (?) were made to **Visual Studio 2010** (**VC10**), and the sequence of windows to get through in order to create a **DLL project** is somehow different from older versions of MS Visual Studio. That may be confusing.

In fact, it is not so complicated. Imagine a textbook describing how to create a simple project using an old Visual Studio version. If you actually use **VC10**, the corresponding steps you have to follow should be the following ones :

1)       **File** -> **Add** -> **New project …**

2)       Amongst the **Installed Templates**, select **Win32**, then **Win32 Console Application**. Enter the name of your project in the field **Name :** , and click on **OK**.

3)       In the **Welcome to the Win32 Application Wizard** panel click on **Next**.

4)       In the **Application Settings**, select **DLL** as well as **Empty project**, and click on **Finish**.

You are done. Now, you will probably add at least two files to the **Source Files** folder in the **Solution Explorer** of VC10, that is a ***.cpp** file as usual and a ***.def** one. For the latter, the **Module Definition File** template is to be found amongst the **Code** templates.