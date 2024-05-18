<!--yml
category: 未分类
date: 2024-05-18 15:43:12
-->

# Trading with Python: How to setup Python development environment

> 来源：[http://tradingwithpython.blogspot.com/2011/11/how-to-setup-python-development.html#0001-01-01](http://tradingwithpython.blogspot.com/2011/11/how-to-setup-python-development.html#0001-01-01)

If you would like to start playing with the code from this blog and write your own, you need to setup a development environment first. I've already put a summary of tools and software packages on the 

[tools page](http://tradingwithpython.blogspot.com/p/setting-up-development-environment.html)

 and to make it even easier, here are the steps you'll need to follow to get up and running:

1\. Install 

[PythonXY](http://code.google.com/p/pythonxy/wiki/Downloads)

. : this includes Python 2.7 and tools Spyder, Ipython etc.

2\. Install 

[Tortoise SVN](http://tortoisesvn.net/downloads.html)

. This is a utility that you need to pull the source code from Google Code

3\. Install

[Pandas](http://pypi.python.org/packages/2.7/p/pandas/pandas-0.5.0.win32-py2.7.exe#md5=c2badf1d82d48a57abcff72228d28cd9)

 (time series library)

This is all you need for now.

To get the code, use 'Svn Checkout' windows explorer context menu that is available after installing Tortoise SVN. Checkout like this (change Checkout directory to the location you want, but it should end with

*tradingWithPython*

):

If all goes well, the most recent version of the files will be downloaded. I'll be writing more code and improving current one, you'll be able to stay in sync with my code by using 'svn update' context menu.

The final step is to launch Spyder (through pythonXY launcher or start menu) and add the directory just above the '

*tradingWithPython'*

(in my example C:\Users\jev\Desktop') dir to python path . Do this with 'tools'->'PYTHONPATH manager'.

Ok, all done, now you can run the examples from \cookbok dir.