<!--yml

类别: 未分类

date: 2024-05-12 18:18:23

-->

# 使用 ETF Rewind 的“情绪差距”创建标普 500 的市场间集成模型 | CSSA

> 来源：[`cssanalytics.wordpress.com/2010/09/19/creating-an-ensemble-intermarket-spy-model-with-etf-rewinds-sentiment-spreads/#0001-01-01`](https://cssanalytics.wordpress.com/2010/09/19/creating-an-ensemble-intermarket-spy-model-with-etf-rewinds-sentiment-spreads/#0001-01-01)

与亨利·比（Henry Bee）合作的大卫·瓦拉迪（David Varadi）

“集成”是从计算智能领域借来的术语，用于描述利用多个输入或变量组合来创建预测或复合信号的过程。通常，一个好的集成将优于任何单个组件，或者至少在样本外更加稳定和健壮。这种集成方法是将技术指标或基本变量（或两者）结合起来的最强大和最合适的方式。然而，由于这种关系的不稳定性和短暂性，这种方法对于市场间分析来说甚至更为重要。我决定探索市场间分析是一项有价值的练习，因为大多数人都专注于技术分析和季节性。然而，我需要一组广泛而又紧凑的市场间变量来进行工作。在浏览了许多我关键的信息来源后，其中一个最有趣的市场间指标引起了我的注意，因为它可能是有价值的，那就是关于**ETF Rewind**的指标- 这是我使用的一个每晚更新的产品，里面有丰富的信息，也包含了几个有价值的工具。 [`etfrewind.blogspot.com/`](http://etfrewind.blogspot.com/)。

![](https://cssanalytics.files.wordpress.com/2010/09/7pairs1.png)

指标称为“情绪差距”，表示 8 对不同市场之间 1 天收益差异的总和。它还很好地捕捉了广泛的市场间关系（或变量），因此是进一步分析的紧凑集合。只列出了 7 个差距，不包括第 8 个差距 - VXX-VXZ - 因为历史数据不足。根据 Jeff Pietsch（ETF Rewind 的创建者）的说法，该指标在日内交易中最有价值，作为捕捉市场对风险资产情绪的指标。正差距或正差异收益意味着市场愿意承担风险，因此可能上涨。通过推断，越多的差距是正的，或者差距的总和越大，市场上涨的可能性越大，反之亦然。然而，这些差距也恰好代表了创建一个预测标准普尔 500 指数的市场间模型的良好整体基础输入。首先让我们看看这些差距作为综合指标的表现 - 在这个例子中，我们包括了历史数据最长的 5 个差距（列出的前 5 个）用来准确预测 SPY，就像情绪差距指标一样。如果差距总和为正，我们会长期交易 SPY，如果总和为负，则会短期交易。

![](https://cssanalytics.files.wordpress.com/2010/09/5rawspreads_withoutoptimization.png)![](https://cssanalytics.files.wordpress.com/2010/09/5rawspreads_withoutoptimization_table.png)

如您所见，基础传播模型的表现优于标普 500（SPY），风险调整后的回报率更高。尽管它们的预期用途不是用于预测第二天的表现（最适合日内交易），但该指标仍然做得相当不错。该指标的问题之一是它是静态的，不随市场条件变化而变化。由于跨市场关系的变化速度远远快于技术关系，因此合理的做法是纳入一些可以适应不同制度的东西。此外，简单的聚合过程本身容易出错：1）某些传播比其他传播更具波动性，因此即使这是不受欢迎的，它们也会有更多的贡献权重 2）某些传播在确定标普方向时不可避免地更重要 3）传播在某些时期的相互关系方面会有所不同，因此使用某些传播信号内存在冗余。自然的问题是，是否使用具有动态分配和自适应过程的模型组件可以改善这一结果。这是凯利优化模型的一个良好任务，其中每个传播作为一个交易系统来交易 SPY，最终暴露就像情绪传播模型一样进行聚合或求和。新模型代表了一个简单的集合模型，并且每天更新，并在样本外测试以证明其随时间的适应能力。

![](https://cssanalytics.files.wordpress.com/2010/09/binary_longshort_252cagrpearsonspearman_5pairs.png)

![](https://cssanalytics.files.wordpress.com/2010/09/binary_longshort_252cagrpearsonspearman_5pairs_table.png)

从图中可以看出，该模型比未经优化的版本表现要好得多。使用非参数相关的斯皮尔曼模型优于使用线性相关的皮尔逊模型。总体而言，结果相当不错。事实上，回报率和风险调整后的回报率与博客圈测试的许多技术指标相媲美。需要指出的重要一点是，一个即插即用的组合跨市场模型，例如所提出的模型与 DV2 或 RSI2 等指标没有相关性。因此，在考虑多个因素的较大复合模型中，它可以添加价值。虽然我会把这个话题留到另一个时间，让我们看一下一个更短的样本，其中包含更多的情绪传播，以查看是否通过包含更多信息来改善性能。事实证明确实是这样的：

![](https://cssanalytics.files.wordpress.com/2010/09/binary_longshort_252cagrspearman_5vs7pairs.png)

![](https://cssanalytics.files.wordpress.com/2010/09/binary_longshort_252cagrspearman_5vs7pairs_table.png)

这表明，使用额外的两对 - 质量差距和日元 - 欧元关系 - 不仅增加了收益，还增加了风险调整后的收益。 最近的表现也有所改善。 很明显，包含更多不相关的差价将大大改善模型以及随着时间的推移的稳健性。 除了只看 252 天的回溯之外，添加不同的时间框架也会增强结果。 还可以使用更复杂的方法，如提升或装袋，但这是一种非常直观且计算密集度较低的方法，可以说更加健壮。
