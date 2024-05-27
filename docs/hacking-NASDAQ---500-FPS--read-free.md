<!--yml

类别：未分类

date: 2024-05-13 00:05:20

-->

# 在纳斯达克进行 500 FPS 的黑客活动：读取免费

> 来源：[`hackingnasdaq.blogspot.com/2010/02/read-free.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2010/02/read-free.html#0001-01-01)

如果我们对 Rx 端进行性能分析，基本上就是寄存器读取的成本+一些冷 DDR 获取+一些杂乱的工作，因此下一个逻辑步骤就是放弃所有寄存器读取。这相当简单，因为 MAC 将 dma 描述符状态和内容直接写入 DDR，因此...让我们只是轮询 Rx 描述符状态，而不是读取 Rx 头寄存器。

128 字节 TCP 往返时间没有寄存器读取

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhUFOVl2tACzkD5I_Z1A6JHXPkkxA8zKRBRrpsOqi8xuDNTTxx-ZPGxXaUcszvqIb86QGBXE0Mxe2y7Ic_a6A5_fL_rraRnr35Ufm582zewNXBGTaKE1N8LEroU8hWNJ6CKZj6Ruh-uKQ/s1600-h/round_tcp_metal.png)

128B TCP 往返寄存器读取

128B TCP 往返精神-> linux 金属（带有寄存器读取）

如您所见，我们现在比 linux 堆栈快 4-5,000ns，这是令人尊敬的！不过，必须谨慎使用这种无寄存器的方法，因为我不确定这里的内存顺序规则是什么，例如，如果 PCIe/SB 写入是有序提交还是可以乱序调度。如果您读取了 Rx 描述符状态，载荷数据很可能还没有到达 DDR。不过，如果你的数十亿美元经过这里，你*真的*想要确定。

最后，大部分加速来自 B 机器的长寄存器读取时间，因此 B 机器的 128B TCP 数据包的全 NIC 到 NIC 时间是...

B 机器，NIC（CPU Rx）-> NIC（CPU Tx）延迟

...大约 410ns，即使有软件校验和。从这个角度来看，我糟糕的 FIX Fast（Arcabook compact）软件解码器在热的情况下大约每个包运行大约 140ns。因此，我们显然可以加速 TCP 环回代码，但是当硬件延迟成为瓶颈时有什么意义呢？

很明显，线对线时间是几微秒...例如，MAC 要花费 1,000 多纳秒才能写入 DDR，而相反，CPU 的写入要到达 MAC...但这强调了在这个层次上问题都是硬件/拓扑，因为硬件延迟比软件大一个量级...不好玩...所以是时候回到我的工作去了。
