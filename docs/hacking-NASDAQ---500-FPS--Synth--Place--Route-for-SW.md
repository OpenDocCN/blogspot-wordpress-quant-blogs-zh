<!--yml

分类：未分类

日期：2024 年 5 月 12 日 23:45:42

-->

# 以**500 FPS**的速度黑入纳斯达克：用于软件的合成、布局、路由

> 来源：[`hackingnasdaq.blogspot.com/2014/06/synth-place-route-for-sw.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2014/06/synth-place-route-for-sw.html#0001-01-01)

在 FPGA 设计中满足时序在最好的情况下可能是痛苦的。痛苦来自于“编译”之间的长等待时间，单独来看这并不算什么问题。糟糕在于（至少对我来说），在运行时你什么都做不了（除了在博客上吐槽！）。

从理论上讲，你可以在代码运行时进行修改，并使用不同的代码/配置启动多个运行，但实际上，我发现这样的多任务通常会导致在所有编译完成后并不知道你到底改变了什么。

作为一个软件人员，很难想象我在说什么。时序？路由？映射？布局？到底在说什么？一个更具体的“编译”逻辑的完整版本看起来像左边的图片。这是一个传输链，它比预算多了 1 纳秒，这意味着它是一个 = b + c; 针对整数中的特定位。这里特别的问题是它花费的时间比简单的加法长 1 纳秒，并且具有其他一些让工具出问题的东西。

它让我思考现代 EDA 工具如何向软件人员解释？

一个答案是：想象一下你的系统内存不再是确定性的。这意味着如果你写入地址 0x1000[0] = 1;就不能保证读取 0x1000[0] == 1。要获得 0x1000[0] == 1 的确定性行为的唯一规则是，如果读写指令靠近内存数据位置。这意味着 CPU 在内存中的指令位置必须接近内存位置 0x1000，才能实现确定性行为。

如果这听起来不像狂热的数独爱好者的版本，那么你可以开始想象编译器会是什么样子。第一部分是根据 verilog/vhdl 输入文件生成正确的操作码序列。之后，这是一个优化问题，找到最佳的操作码/内存位置组合，以在有限的时间内获得正确的读/写内存行为-一个 NP 难问题。

最后，如果你相信所有这些，那么制作一个可以编译但无法正常工作的程序是很容易的-这就是时序闭合的痛苦。

...至少在某种伪手势数独类比中。
