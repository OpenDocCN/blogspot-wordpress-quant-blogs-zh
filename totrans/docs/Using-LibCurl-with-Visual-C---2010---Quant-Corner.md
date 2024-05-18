<!--yml
category: 未分类
date: 2024-05-18 08:08:26
-->

# Using LibCurl with Visual C++ 2010 | Quant Corner

> 来源：[https://quantcorner.wordpress.com/2012/04/08/using-libcurl-with-visual-c-2010/#0001-01-01](https://quantcorner.wordpress.com/2012/04/08/using-libcurl-with-visual-c-2010/#0001-01-01)

I was stuck for some time with **LibCurl** and **Visual C++ 2010** (**VC10**). The document [**Using libcurl in Visual Studio**](http://curl.haxx.se/libcurl/c/visual_studio.pdf "Using libcurl in Visual Studio") available at the **[Curl](http://curl.haxx.se/libcurl/ "Curl")** project’s website doesn’t help that much (notice it dates back from 2002). I searched on the internet for hints, but hadn’t find the ‘right’ solution. At the same time ** good for my ego **, I realized I hadn’t been the only one in trouble. 😉

Below is how I got **LibCurl** working with **VC10** (on a 32-bit machine).

First, download the latest version of **LibCurl** for **VC10,** [here](http://curl.haxx.se/latest.cgi?curl=win32-ssl-devel-msvc "here").

Now, create a new C++ project.

(In what follows, I assume that solutions are built in **Debug mode**, but it’s easy to derive the steps below  for the **Release mode.**)

First  go to **Properties > Configuration Properties > VC++ Directories > Include directories**. Here, add the **curl** directory to be found in the **include directory** of the unzipped **Libcurl** file (C:\ … \libcurl-7.19.3-win32-ssl-msvc\include\curl).

Now go to **VC++ Directories > Library directories**. Add the **Debug** directory containing **curllib_static.lib**, **curllib.dll** and **curllib.lib** (C:\Users\Édouard\Documents\Visual Studio 2010\LibCurl\lib\Debug).

Still in **Configuration Properties**, go to **Linker > Input > Additional Dependencies**. Here, you have to add the **curllib.lib file** (C:\  … \lib\Debug\curllib.lib). Type in up to name of the lib file.

The next step consists on adding **curllib.dll**, **libeay32.dll**, **openldap.dll**, and **ssleay32.dll** in the **Debug directory** of your project. There all are to be found in the root  directory of **Libcurl**. You also have to add **libsasl.dll** in this directory. Just google for it.

(Shouldn’t this have been the first step?) Now, open the **curl.h** file. Replace the line **#include «curl/curlbuild.h»** with **#include «curlbuild.h»** .

You’re done.