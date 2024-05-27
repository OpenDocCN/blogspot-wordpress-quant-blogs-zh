<!--yml

类别：未分类

日期：2024-05-13 00:09:32

-->

# 以 500 FPS 黑客 NASDAQ：一个符号

> 来源：[`hackingnasdaq.blogspot.com/2009/12/symbol.html#0001-01-01`](http://hackingnasdaq.blogspot.com/2009/12/symbol.html#0001-01-01)

下一步是查看单个符号的流量。这里是 MSFT 的 1 秒，10ms，1ms 图表。其中肯定有一些信号，但信噪比正在急剧下降。处理方面，最大的订单数量/秒可能是 1000 笔，意味着每条订单要花费 1000us 的时间......那是相当多的时间。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiu7tnZ22LItXjneAEZFC9Fjy87oue0uL-cklxxS7ThKTj3WWRba_1bD0JQWLkg2vvIZZuJzRdcaFkid_l35x0VO-1mhNvcPwby3RKFbrv1Z8fVj0-zwX2mE7V8c2Q6q-a4De6lfN_rAg/s1600-h/msft_stack.png)

1 横向像素 = 1 秒

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEivsfmgWkTzPo6ju-7O4saepD9V8bMuGyj7oAfx4BWVyFRgJfCfaW8ZrGQ0NdX-kGWxBBJwuHBmA2GAdrxeGFuLgGyO2ha6TbFq1circFFIueoPosGfIwx65tFka69U1M10u48AOa1Vgw/s1600-h/msft_add.png)

1 横向像素 == 1 秒

将其分成 10ms 的间隔，会变得越来越混乱，几乎没有任何模式。也许仅有的明显的是尖峰是平均值的 10 倍，我猜测这是高频交易员们涌入市场的指令。或者可以是大宗交易活动被随机切割成了突发指令，因此出现了大尖峰。不管怎样，需要对价格水平+成交量进行拆分，以弄清楚这些交易尖峰到底发生了什么。

1 横向像素 == 10ms

1 横向 == 10ms

深挖到 1ms 水平和发出的订单数量，几乎找不到什么信号，基本上都是噪音。

1 横向像素 = 1ms

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi1aXs2sV7X6TnSxhUC0Nz7o1g_dOQ1Y-f6x0DMZyi1C_U5FkaSWsnC33IBOseZ9RVzauH7dco8Sxxc2Nfx8b9GKLdpFWO7Yx8JJ3NlNEBJX8StLnxffunBjv-dy_1TRlgmtLFsNOX4Q/s1600-h/msft_add1ms.png)

1 横向像素 = 1ms
