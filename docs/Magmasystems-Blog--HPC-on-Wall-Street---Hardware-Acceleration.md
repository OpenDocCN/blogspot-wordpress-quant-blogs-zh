<!--yml

类别：未分类

日期：2024-05-18 05:12:08

-->

# Magmasystems 博客：华尔街的 HPC - 硬件加速

> 来源：[`magmasystems.blogspot.com/2007/02/hpc-on-wall-street-hardware.html#0001-01-01`](http://magmasystems.blogspot.com/2007/02/hpc-on-wall-street-hardware.html#0001-01-01)

犹他大学的 Sam Brown 刚刚发表了

[一些幻灯片](http://www.chpc.utah.edu/hybrid_computing/talks/sam_brown_talk.ppt)

在他最初尝试硬件加速时。他对比了 Cell 处理器的使用，

FPGAs

，和

多

多核处理器。他试图加速 2 路波动方程建模，这不是一个金融应用程序，但作者学到的经验可以适用于那些正在（或探索）

HPC

在华尔街。

最大的努力是在展开循环和

并行化

你的代码。使用

POSIX PThread API

和

多

多核

cpus

是最容易的事情。使用 4 个线程（2 个双核，每个 2.2

Ghz Opterons

，4 GB RAM），他在一组基准测试中提高了 11 倍的性能，在大应用程序上提高了 2 倍的性能。

该

FPGA

系统使用了

Altera Stratix

II

FPGA

。他大约提高了 14 倍的

改进

在初步的一组基准测试中，但开发工作要困难得多。它花了 12 个小时才把设计放到

FPGA

芯片。

Cell 系统是索尼

Playstation

3（！！！）和带有 2 个 Cell 处理器的 IBM Cell 刀片，每个处理器有 8

SPEs

每个（一个 Cell 处理器有 8

SPEs

，作为协处理器。）Cell 的结果普遍令人失望，作者怀疑自己是否正确编写了 Cell 的程序。关于 Cell 我听说的一件事是，它非常难以编程。或许像

PeakStream

可以帮助你完成这项工作。

（为了即时满足，幻灯片 28、29 和 30 是高潮部分）

硬件加速能为你做什么？更快地对衍生品进行定价。更快地生成风险值，特别是对于奇异品。更好的隔夜压力测试。

问题在于获取

技能集

到

并行化

算法，处理开发环境（尤其是调试），学习 C 的新变体，并从业务中获得支持。

©2007 Marc Adler - 版权所有
