<!--yml
category: 未分类
date: 2024-05-18 08:08:53
-->

# Installing QuantLib for VC11 (Windows) | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2012/11/13/installing-quantlib-for-vc11-windows/#0001-01-01](https://quantcorner.wordpress.com/2012/11/13/installing-quantlib-for-vc11-windows/#0001-01-01)

Below are instructions for installing and using **QuantLib 1.2** for **VC11** on a computer running under **Windows** (32-bit). We will only install  the core library of **QuantLib**, that is only 1 of the 15 projects contained in the solution file. Thus, we will just need **Boost** header-only. There will no need to install the **Boost** library.

**(I) Requirements**

**a)** You must have the **VC11** environment available on your computer, that is Visual Studio 11 Beta, Visual Studio 2012, Visual C++ 2012 Express, … .

**b)** The **Boost** library can be downloaded [here](http://www.boost.org/users/download/ "Boost"). Currently, the latest version available is **Boost 1.52.0**.

**c)** The **QuantLib** library. The solution file of **QuantLib 1.2.1** for **VC11** can be downloaded from a [previous post](https://quantcorner.wordpress.com/2012/10/28/quantlib-1-2-with-vc11/ "QuantLib for VC11").

**(II) Building QuantLib**

We will build the solution from within **Visual Studio** in Debug mode, here. Just follow the same upcoming installation steps to build **QuantLib** in any other mode (e.g. in Release mode). From now onwards, we assume everything is okay with the requirements in **(I)**.

**a)** From within your GUI or directly by double clicking on the file, open the solution file named QuantLib_vc11.sln ( *… \QuantLib-1.2.1\ QuantLib_vc11.sln*). This will open the 15 projects contained in the solution (see the picture, below).

[![](img/b3443eacd5b40d4a504f1221e4661ff3.png "vc11 1")](https://quantcorner.wordpress.com/wp-content/uploads/2012/11/vc11-1.jpg)

**b)** Make sure the ‘QuantLib’ project is selected that is it is enlighten in the ‘Solution Explorer’ panel. Then, right-click and select ‘Properties’ in the context menu.

**c)** Add the path to the folder *… \boost_1_52* to *Configuration Properties*/*VC++ Directories/Include Directories*. Then, add the path to the folder *… \boost_1_52\libs* to Configuration Properties/*VC++ Directories/Libraries Directories* (see in bold on the picture, below). Obviously, you click on ‘Apply’ for your changes to be taken into account.

[![](img/e08a0d84d4b0e705d1a13a3fb4f6236b.png "vc11 2")](https://quantcorner.wordpress.com/wp-content/uploads/2012/11/vc11-2.jpg)

**d)** Now, in the ‘QuantLib Properties Pages’ panel, set the *Configuration Properties/*C/C++/***Precompiled Headers/Precompiled Header* item to ‘Not Using Precompiled Headers’.

[![](img/d81f26b28f8eac765250a7e9f3ea6b10.png "vc11 3")](https://quantcorner.wordpress.com/wp-content/uploads/2012/11/vc11-3.jpg)

**f)** In the ‘Solution Explorer’ panel, right-click on ‘Solution_vc11’ (15 projects)’ and select ‘Properties’. In *Configuration Properties/Configuration* unselect all the project from ‘Build’ except the ‘QuantLib’ project.

[![](img/bfc20357a3c6f10e3b3394dbe9ffe19e.png "vc11 4")](https://quantcorner.wordpress.com/wp-content/uploads/2012/11/vc11-4.jpg)

**g)** Now, right-click again on ‘Solution_vc11’ (15 projects)’ in the ‘Solution Explorer’ panel and click on ‘Build Solution’. Alternatively, on can strike the F7 key. The build process should start.

There might be warning messages during the compilation, but this is no real problem.

**(III) QuantLib Usage**

**a)** Each time the C++ program you write relies on the **QuantLib** library, you will have to make the *… \boost_1_52* and *… \boost_1_52\libs* folders visible to your project as shown at the step **(II,c)**, above.

**b)** Then, add the path to the folder *… /QuantLib-1.2.1* to Configuration Properties/*C/C++/General/Additional Include Directories*.

[![](img/155ace2fa84acfd008b626c967309eb7.png "vc11 5")](https://quantcorner.wordpress.com/wp-content/uploads/2012/11/vc11-5.jpg)

**c)** Eventually, add the path to the folder *… /QuantLib-1.2.1/lib* to Configuration Properties/*Librarian/General.*

[![](img/10b77b14c33ccc2be43a251a4bfbce00.png "vc11 6")](https://quantcorner.wordpress.com/wp-content/uploads/2012/11/vc11-61.jpg)

Alternatively, one can make the steps **(III, a)** an **(III, b)** less tiredsome, specifying once for all the directories required for the use of **QuantLib**, e.g. by specifying a [per-user directory list](http://msdn.microsoft.com/en-us/library/vstudio/ee855621.aspx "Per-user directory list"), or any other method you like*****.

****** Thank you to **Polter**  for his comments in the Wilmott forums.*