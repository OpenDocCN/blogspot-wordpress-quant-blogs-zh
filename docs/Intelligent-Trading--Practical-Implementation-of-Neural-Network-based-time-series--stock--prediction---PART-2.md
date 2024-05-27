<!--yml

分类：未分类

日期：2024-05-18 04:47:58

-->

# 智能交易：基于神经网络的时间序列（股票）预测的实用实现 - 第二部分

> 来源：[`intelligenttradingtech.blogspot.com/2010/01/practical-implementation-of-neural.html#0001-01-01`](http://intelligenttradingtech.blogspot.com/2010/01/practical-implementation-of-neural.html#0001-01-01)

作为系列文章的后续，我想花点时间介绍一下 Weka，这是我们用来实现神经网络的机器学习工具。它是一个出色的开源 JAVA 工具，由新西兰的 Waikato 大学开发。编程经验不多的用户可以使用 GUI 外壳，使得运行回归或分类场景变得轻而易举。更高级的 JAVA 程序员可以选择使用命令行或定制自己的类。此外，还有许多支持选项，包括一个出色的 Nabble 论坛，你可以订阅它——

[Weka 论坛](http://old.nabble.com/WEKA-f435.html)

我发现问题回答得非常迅速，网站上有很多活动，所以你不必等待很长时间就能得到回复。此外，Ian Witten 和 Eibe Frank 出版了一些很好的书籍，引导你通过最小数学理论的实践数据挖掘：

[数据挖掘：实用机器学习工具和技术 Java 实现](http://www.amazon.com/Data-Mining-Practical-Techniques-Management/dp/0120884070/ref=sr_1_1?ie=UTF8&s=books&qid=1264903087&sr=8-1)

我拥有第一版，并发现它是一个非常有用的参考书。

免费工具（Weka）中包含了各种内置的学习模块，比如线性回归、神经网络（亦称多层感知器）、决策树、支持向量机，甚至还有遗传算法。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiZNqm-WKrMONM33pPAU3w5mRbpOiWFVK87iZbUk09snDORrMaYu7Qpcgh5BxI0m-SF8yfuO8skZBRisWEPRKd1x5dTenZF3AO33cJI8kPMM-ggWotljRFK_i9MxOHH7Yt5PHdgROi6z9Q/s1600-h/weka_gui1.jpg)

图 1. 使用 Weka GUI

在图 1 中，我们看到 Weka GUI 选择器已打开，并选择了探索器选项。Weka 常用的本地格式是.ARFF 格式，幸运的是，它还可以读取.CSV 文件，这些文件可以通过 Excel 的保存选项轻松创建。我们将首先训练的 Excel 文件是 sim_training_set_perfect_sin.csv。一旦加载，你将在 Weka 探索器壳中看到所有相关变量。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhpfEeU7bgRZ4opAxbAGkBtvZqoKjVHX8_gA4Ufwz811irkZtognHnNpV6KL0y-oiNKGSkvXe02uYKGZ8YlgJln9J-vsH-dnqPcmTFB58t3l3hlv5RnleBt0SYv5ROQ9pRdDt_kfyqPC4E/s1600-h/fig2_pt2back.jpg)

图 2. Weka 的加载 Excel csv 训练源文件

我们注意到有些新变量已经被引入，在第一部分中并没有。

为了理解原因，让我们展示在此使用的 CSV 文件。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgt7EMZXcsBv3SpPF52IH76q5HJALLe1wkp75wgQyNAUywZd9nxnBqKJqAometVgId3fIJHB96Ya36BlvtaBqDUHHjIEZ1XaNVYsFl_n0KqYK5poB_EnvldShQPyeVMOi9ucjmw9Z-8FzA/s1600-h/fig2_training_sin-pt2.jpg)

图 3. 训练集变量。

我们所看到的是，原始的完美正弦波信号在名为 signal 的列中保持不变。附加的信号 s-1、s-2、s-3、s-4 通常被称为延迟或嵌入（维度）变量。它们仅仅是信号的滞后值，用于训练神经网络。确定滞后值的数量没有确切的方法，尽管存在许多不同的方法。现在，我们将简单地接受四个信号的滞后值是有用的。最后一列，称为偏置，是神经网络共有的。偏置节点允许神经网络通过训练将常数信号输入移动到网络中。例如，想象我们的信号平均值为 2.0 但是我们正在学习它。神经网络需要一些输入来跟踪那个常数值，否则它将会有很大的偏移误差，妨碍收敛。偏置节点完成了该操作。熟悉工程理论的人会 recognize this node as a DC bias.

好吧，所以在 GUI 界面中我们注意到的另一件事是，在右下角选择了类：信号(数字)。这是因为我们是预测一个数字类，而不是一个名义类（这对于分类方案来说是典型的默认值）。

接下来，我们选择分类标签以选择我们的学习方案，在此案例中将是多层感知器。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiMV1Zq9uPUxGfVIK2E96dFxs2JhhFvxjYWSi7Yr34H7II7D0-H3TnV8l1ypsL6QDiw7DGugZmEpNFqVn8epuP4pKOhrnOvATPB8wNMONjyWRruSWco3qS0Zp_fDUXA1YAT3npct067BZs/s1600-h/fig5_MLP_options_pt2.jpg)

我们将 nominalToBinaryFilter 和 normalize 属性设置为 False，因为我们不希望修改输入数据以变为二进制，并且我们没有使用名义属性。然而，我们

如果我们想要将`normalizeNumericClass`设置为 True，就像之前提到的那样，它将强制将规范化方案设置为 Weka 的内部限制范围，因此我们就不必自己设置了。此外，我们将训练 1000 个 epochs。

![图片](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj8SQWMNUa9ET41uCP4V03aZZWPfzgJRhP82NwIxHAP-4T2UqvYc4Q08a_CVhA5yutodVey587fU-VuhFx6r3sCrVBtYrjQiYBACb69NgqTO2tOzcqHoeNNbiSYoRK6HcYZrtLQ9aIW3oM/s1600-h/fig6_pt2_MLP_options.jpg)

图 6。MLP 训练模型的首选项。

我们将通过对 66%的数据进行训练来构建模型。我们希望存储和输出预测结果，以便我们可以直观地看到它们的样

![图片](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiwxxresRDCU3sHYERfBwT-WxA-wrO2NXxnnYcVFE-RAIHctwXjuIBwvL3x-kNSjRC5ARHftXGBfM6I3XP8HEkJ5SY7cLh7LleGuYaPsU08KKJ-TVN8ZBGo9kHrJ0RjUlFE4Gv4F02gdwE/s1600-h/fig7_pt2_MLP_simple_sin.jpg)

图 7。带有统计摘要的结果控制台。

如果我们向上滚动，我们可以看到模型收敛的实际权重，这些权重将用于预测样本外数据。

我们可以看到，最后 34%的结果（271 个样本数据点）有一个很好的打印输出，以及预测值和误差，以及控制台底部有一个有用的统计摘要。我们经常使用均方根误差作为神经网络回归的性能度量。在这种情况下，数字 0.0005 相当不错。但让我们使用一个小技巧来视觉检查一下有多好。我们实际上可以从控制台抓取数据（通过使用鼠标左键选择并拖动），然后将这些数据复制回 Excel。因此，我们可以在 Excel 中绘制实际与预测的样本外结果。

![图片](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg9FF-MGVDLWuDBDaTr0vAvksQ7gL1MIdK0h-g7qOK4OvxuQZZ_GjTssfxzbvf7TTJxjV4Pxu6QmML6gw88nJAa7LsZdEYwm3pz1xl7Dk9W09k3MWAtrKKR7-j_Z6GLAtJAWKoHQrxABrM/s1600-h/fig8_pt2_MLP_excelimport.jpg)

图 8。将预测结果导入回 Excel。

注意，我们将数据从 Weka 控制台剪切并粘贴回 Excel，但必须选择文本以将数据分隔成列。

![图片](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgFQrjZnlPmgpJxBAz4ZPFi60Nf-xS_TmX8y9uhB3BPsIm_z1TrwBPq2qsIBytKZ08mXDNdMWgI4sPe4AdicNNXcB7KtRz3ShOeRZ-ooEAAjO3aGIuXc36BYy-m7mUjzDgBtttenjoRuek/s1600-h/fig9_pt2_MLP_txttocolumns.jpg)

图 9。选择要分隔为列的区域。

瞧！现在我们可以绘制预测值与实际值的图表了。看它们排列得多好。在样本外集合上的误差非常小，注意有些是 0，其他的是.001，肉眼几乎无法察觉，不放大那个点很难看出。

实际上，它找到了一个完美的时间序列模型（稍后我们会解释为什么会这样），误差可以归因于数值精度。

![图 10](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiUrZEtp4jaBC9LR7IoY07YnJJb_J1SCAcB2iZOsKVVvN7K6PWJutnsgbQ_qxJ962XqdTz4mUkt4GBhMmOXkNhxDolbcbnEfuruyxBKsF1QIr_JSXZq2fTh1-yWtHPuZcvLk4I0lbrbmpA/s1600-h/fig10_pt2_results.jpg)

图 10。预测值与实际数据的结果图。

我们现在刚刚使用 Weka 和 Excel 构建了一个基本的神经网络，用于简单的正弦波时间序列。预测的样本外结果非常好。

然而，正如我们将看到的，我们使用的数据信号，即简单的正弦波，是一个非常容易学习的信号，因为它完全重复且平稳。我们会发现，随着信号变得越来越复杂，预测结果就不那么好了。

第二部分就到这里，欢迎留言。
