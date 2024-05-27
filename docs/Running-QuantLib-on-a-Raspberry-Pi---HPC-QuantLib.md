<!--yml

分类：未分类

日期：2024-05-17 23:41:16

-->

# 在树莓派上运行 QuantLib – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2012/08/11/running-quantlib-on-a-raspberry-pi/#0001-01-01`](https://hpcquantlib.wordpress.com/2012/08/11/running-quantlib-on-a-raspberry-pi/#0001-01-01)

**QuantLib 1.2** 在一台[树莓派](http://www.raspberrypi.org/)上运行，这是一款基于 700MHz ARM 处理器，售价为 35 美元的信用卡大小的计算机。在树莓派上编译 QL 非常简单：

1.  安装 boost 单元测试：`sudo apt-get install libboost-test-dev`

1.  `./configure –disable-static`

1.  `make`

如果你的发行版基于 boost 1.49，那么你会看到很多警告，比如“警告：*swp*{b}使用*已被弃用*对于这个架构”。这些警告可以忽略，或者按照[这里](https://svn.boost.org/trac/boost/ticket/7141)的简短说明来消除它们。QuantLib 基准测试的运行速度为 28.3MFlops，这与 Pentium II@300MHz 的性能相当。
