<!--yml
category: 未分类
date: 2024-05-18 08:09:38
-->

# Using Quantlib on a Windows (32bit) machine | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2011/01/24/usin-quantlib-on-a-windows-32-bit-machine/#0001-01-01](https://quantcorner.wordpress.com/2011/01/24/usin-quantlib-on-a-windows-32-bit-machine/#0001-01-01)

In this post, we show the required steps before using  **Quantlib** on a **Windows 32** computer. We install this powerful library for quantitative matters with **MS Visual Studio 2010**. And, that must work for MS **Visual Studio Express 2010** as well. We build upon the “Install” section of the **Quantlib**library official website, i.e [http://quantlib.org/install/vc9.shtml](http://quantlib.org/install/vc9.shtml). As this web address itself indicates, this is an installation documentation for the previous version of MS Visual Studio (that is the  MS **Visual Studio 2008**version). Our job is getting and installing the latest Quantlib files.

The **Quantlib** library requires the **Boost** library to be available on your machine. We thus will install the latter, too. Finally, we will install a user-friendly software, namely **TortoiseSVN**, to get the latest versions of the files of both libraries.

**Let’s start**:

– Download the **Boost**library installer, freely available at [http://www.boostpro.com/download](http://www.boostpro.com/download) . At the time of writing the latest available version is BoostPro 1.44.0 Installer.

– Follow the “Boost installation” paragraphs at [http://quantlib.org/install/vc9.shtml](http://quantlib.org/install/vc9.shtml) . Except, that you will install the **Visual C++ 10.0** (**Visual Studio 2010**) binary.

– Download the **Quantlib**library from [http://sourceforge.net/projects/quantlib/files/QuantLib](http://sourceforge.net/projects/quantlib/files/QuantLib) . Select the latest version of the library, and start the download.

– Download **TortoiseSVN** from [http://tortoisesvn.net/downloads.html](http://tortoisesvn.net/downloads.html) . It is a subversion client program for **Windows**. It is easy to use and this software will allow you to get the latest file versions of Boost and **Quantlib**. It is well documented, too ([http://tortoisesvn.net/docs/release/TortoiseSVN_en](http://tortoisesvn.net/docs/release/TortoiseSVN_en) ).

– Get the latest **Boost**file versions from the subversion repository using **TortoiseSVN**at [http://svn.boost.org/svn/boost/trunk](http://svn.boost.org/svn/boost/trunk) .

– In much the same way, update your **Quantlib**file versions, from [http://quantlib.svn.sourceforge.net/svnroot/quantlib/trunk](http://quantlib.svn.sourceforge.net/svnroot/quantlib/trunk) .

– Find out the **QuantLib_vc10.sln** file in the **C:\ … \Quantlib\QuantLib** directory on your disk. Double-click on it. Visual studio will simultaneously open the 14 projects.

– Now, make the **Boost**headers and libraries available to **Quantlib**. Right-click on the **QuantLib**project in the solution explorer, then add your **C:\ … \boost_1_44** directory into the “Include files” directory of **Visual Studio**(We assume you didn’t rename any file). Next, add **C:\ … \boost_1_44\lib** into the “Library files” directory.

– You are ready to build the **Quantlib**library. In the solution explorer window of **Visual Studio**, right-click on “Solution ‘Quantlib_vc10’ (14 projects), and choose “Build the solution” to build all the 14 projects.

***–  You’re done!  –***

You can build the solution whatever in build or release mode. It doesn’t really matter. The important thing is that you will have to build your future projects in the same mode as **Quantlib** had been built. Being so, *why wouldn’t you build* ***Quantlib****in both modes on your computer ?*