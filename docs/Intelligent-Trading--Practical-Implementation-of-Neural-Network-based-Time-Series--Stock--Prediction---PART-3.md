<!--yml

分类：未分类

date: 2024-05-18 04:47:47

-->

# 智能交易：基于神经网络的时间序列（股票）预测的实际实现 - 第三部分

> 来源：[`intelligenttradingtech.blogspot.com/2010/02/practical-implementation-of-neural.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2010/02/practical-implementation-of-neural.html#0001-01-01)

好了，现在我们已经看到完美正弦波信号学习得很好，让我们提高难度，看看复杂正弦波学习得如何。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj86nmSv2reFnkTVbYph2-cB-S06g6LDuFCDqJgbvkLZyTbOAKqQav-XR19bIJbyVl_4EXqPS5Ln8rYFeibUgZewiXs5PdsPhy-gHWZ2rYr662RFD_7utdbVDON4andf2OJpJSu6Gc1ZjM/s1600-h/fig1_pt3_complex_rsltplot.jpg)

图 1\. 复杂正弦波的实际 vs. 预测的摘要

哎呀。发生了什么，样本外数据看起来不那么好。但是，让我们看看摘要统计数据。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjgpnC-n_ca5tp_MpfHeW0k4rgBExKQzsd0kGacTdVDaakqLC9OxD7YW5IKFNadrAjoXUnamh57FMoIleiNMaNqQzbqV3F26LQSJJ0_Os0sMxaRiZIzku0Y9u95yvPYOUwF8HHMzWZF9tg/s1600-h/figg_2_weka_rslts.jpg)

图 2\. Weka 对实际 vs. 预测的样本外复杂正弦波摘要

我们看到均方根误差从 0 增加到了约 0.92，尽管相关系数看起来仍然相当不错。发生的情况是，即使信号仍然是完全确定的，但神经网络需要更多的训练数据或更多的工作来正确地逼近新函数。

最后，让我们向信号添加一些随机噪音。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhBV2AecCzgcudvRPJrfRA4hG28hm0_g-8uxs3IG2jnG1OwIpM9B__EhwB6bP40oiPAPwPfkgGHZ5nTm3ul1KEbpmNfHrSwLkFsbVVzX_TNQGIdr-zhaCcbcbZ7GN3_f0K59qjU0PxImK4/s1600-h/fig3_noiseadded.jpg)

图 3\. 添加了噪音的复杂正弦波。

然后让我们试着在随机信号上训练。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgro8u6fhKAa0j5ljGrTmUhI6R5jvh_tUjvdscv5BviHhyphenhyphenpJaoGHJmxcP_JitNjVD_V0QzhL5EjWwi3jHh8S7qjwzJMKf2bMcDnyMIcxp1q7jGivCbThIsBlTi6VrNrot-urlzTVz_F8V8/s1600-h/fig4_act_vs_pred_rslts_nois.jpg)

图 4\. 实际 vs 预测的添加了噪音的复杂正弦波

我们看到预测开始变得非常糟糕。

均方根误差增加到了 0.3，但可能有点误导，因为预测波形的信号幅度大大降低了。更重要的是，相关系数从 0.9 下降到了 0.3。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi9qdLdKBgbmBMbpMuuwgFSigfi2XH6UtQzFyt4TiThTYFYcuWMwBJhqgbO4BS0_uwOVswkjpqXTpamG3AQNMV4jW8U1-h-sL7UkFJZNbExqZKQKXZK8v9P1c7W0xYGuCHxWdAWwknmmu4/s1600-h/fig5_rstls.jpg)

图 5. Weka 结果总结。

尽管 RMSE 看起来并不太糟糕，但相关系数从 0.9 一路下降到 0.3，相对误差从 15%激增至 97%。

结论是，我们训练的信号越噪声或频率越高，结果就越糟糕。让我们从另一个角度尝试理解这个问题。

让我们思考一下为什么第一个简单的复杂预测如此美好。

神经网络究竟做了什么？你可能听说过它是一个通用函数逼近器。这本质上是真的。正如一条直线 y=mx+b 是通用线性函数逼近，神经网络擅长学习任何非线性的未知一般函数。但是，让我们来看看原始正弦与其前一个滞后值的散点图。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhWpsbFamZkQaMNOizYm_p-ANKx7phW62mQm24qfOvxk3YRoMCKkUTEMSN8MlL4ulAsrCebXalW9mrPN3-1ckoKJ5TCHheypRpj5MvOcYZgmdMcQ57TIW60G8DItFt_ggwXTNjnrfgPSSU/s1600-h/fig6_scatter1.jpg)

图 6. 完美正弦与滞后一个值和时间序列图的散点图。

我们注意到，当我们使正弦相对于自身滞后时，我们会看到一个预期的确定性模式。这个模式有时也被称为李萨茹模式。但是，当我们尝试仅从先前的滞后值预测一个值时会发生什么？有两个可能的输出，点 A 和点 B。如果你回想一下很久以前的代数，一个函数是将一组点映射到范围中的一个独一无二的输出，但在这里我们看到有两个。因此，即使模型是完美的，它也无法正确预测下一个值，因为有两个可能的结局；这就像抛硬币一样。所以实际的预测结果将是两个可能的输出状态的平均值。但是，记住我们添加了滞后值作为输入进行训练。那么，当我们做一个完美正弦与先前两个滞后值的散点图时会发生什么？

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhz48EmxjvtCWb0mHyQnyavJ6yoMjiwCgN-AxMpEG8cgzQYUmfbRXhWtPd9R41SfBCyzVo7sCn_VFIBXwYABqisDUDQodmc6MxrZ-QjS9UrtAUIek3TVYgjLeovaA51KZlZ9GE2Ap2AC2I/s1600-h/fig7_3dscatter.jpg)

图 7. 完美正弦波与两个滞后值和时间序列图的 3D 散点图。

我们看到，通过使函数依赖于先前的两个滞后值对，只有一个独一无二的对应输出点！再也没有模糊性，因此存在一个完美的函数能够适应这个条件预测。这就是为什么第一个带有嵌入变量的完美正弦在神经网络回归中具有如此完美的拟合。这是思考神经网络如何学习模式和为什么使用嵌入维度或滞后变量进行训练是有益的另一种方式。

那如果我们用噪声污染这个正弦会发生什么呢？

以下是散点图。

![无标题](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhLiS3iu8czz5myaFpSGIFOxLyeLbcyx1a4BDL1LXJTOJOPnvCqUhIIlFGhSBkeKwGJeva5HPsJ_QVaCizw3rVqSJOOe6zZ_CEh6gFwSDer18TZAy4kPvL1iyU4kxY0GC8-GfVFGRwS0l8/s1600-h/fig8_noisiysinscatter.jpg)

fig8. 带有滞后值的噪声正弦散点图。

看看每个先前的输入预测的所有可能的模糊输出！难怪可怜的神经网络学习起来有困难。它要么给出一些平均输出，要么根据嵌入的维度结构（滞后值），给出与我们期望非常不同的预测。

总之，我希望我给了你一些关于神经网络喜欢什么以及它是如何学得好的思考。

它可能需要一个以上的滞后维度来学得很好，而且它不喜欢噪声输入！这是我发现许多使用神经网络预测的文献中存在的问题，给它带来了坏名声。他们用命中率之类的指标作为目标函数进行总结。然而，这就像试图跟踪硬币抛掷，这并不总是最 useful 的目标。

我希望你也从另一个角度思考这个问题，这可能适用于股票预测。看看以下的信号。

![无标题](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiMaOTw_lw5HW0okr_nE94zHwRdEsy74NnATB5TaZAGEEl26UEEMlTtKab5B_Urxyi0h3NRiE4U2JWBz7bXQDHSNG8eTzv_rFO0_WxMWDTEvFi132slIStGdTIhcNVJ2qVSG80b9cVqbfg/s1600-h/fig9.jpg)

fig 9. 跟踪平滑正弦的动量

看看我们通过跟踪正弦的'平滑'版本在做什么。

我们只是在跟踪动量——上升或下降（可能还有横向），就是这样。另一种思考方式是，我们正在跟踪趋势，但不是每个小小的波动。我们还可以看到，动量中存在强烈的序列或自相关，与高频原始时间序列不同。

通过使用信号的'平滑'版本，我们可以专注于跟踪信号而不是噪声。所以像命中率这样的东西并不那么重要。重要的是我们捕捉到了趋势的大部分实质。另一个好处是我们不会像野马一样被抛来抛去，被搅动得那么厉害。在通信中，我们使用一种叫做相位锁定环的东西来跟踪时间域噪声（抖动）中嵌入的时钟信号，在这里我们专注于跟踪金融'信号'，而不是每个小小的波动。确实会有残余波动，但这些回撤可以通过统计控制图来监控，同时允许神经网络专注于跟踪信号，而不是试图跟踪噪声，这可能是适得其反的。

关于这个问题，还有一个思考方式如下。如果你熟悉计量经济学，那么有很多模型尝试预测所有的剧烈转折和高频成分（AR，ARMA 家族等）。通常它们会告诉你，如果残差仍然存在一些序列相关性，那么你没有很好地建模，需要进行额外的微调。如果你试图完美地拟合一个模型（演绎地），这当然很好，但是它在样本外表现（归纳地）相当糟糕，因为你本质上是在过度拟合模型。近年来从机器学习领域涌现出的一个非常有趣的成功概念，就是集成平均方法的思想。有几种工具，如装袋、提升、堆叠和委员会投票，试图进行平均预测而不是精确预测。预测平均值已经取得了很大的成功，包括众所周知的 NETFLIX 奖，他们使用堆叠学习者。

如果你觉得这听起来很陌生，只需想想这篇文章的目的，那就是试图平滑信号并跟随平均值，而不是预测高频波动。

NEXT. 第四部分。股票预测示例。
