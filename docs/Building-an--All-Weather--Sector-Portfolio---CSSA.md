<!--yml

类别: 未分类

日期: 2024-05-12 18:01:33

-->

# 建立一个“全天候”行业投资组合 | CSSA

> 来源：[`cssanalytics.wordpress.com/2013/02/11/building-an-all-weather-sector-portfolio/#0001-01-01`](https://cssanalytics.wordpress.com/2013/02/11/building-an-all-weather-sector-portfolio/#0001-01-01)

[“全天候”投资组合](https://cssanalytics.wordpress.com/2012/11/07/the-all-weather-portfolio-derivation/ "The “All-Weather” Portfolio Derivation") 的核心概念是平衡：通过分配使得投资组合在不同的经济环境下表现均衡。原始投资组合通过广泛的资产类别平衡投资组合风险和绩效，以保持对经济增长和通货膨胀变化的中立。这一基本概念可以延伸到创建一个“全天候”股票行业投资组合。观察行业轮换的一个传统方式是使用经济“商业周期”来确定哪些行业最有利。在这个观点下，经济经历四个不同阶段，按顺序逐步发展，并在多年周期内重复：1) 早期 2) 中期 3) 晚期和 4) 衰退。在这种情况下，经济增长在最早的阶段最高，在商业周期进展的过程中增速逐渐下降。通货膨胀在最早的阶段较低，并随着时间的推移逐渐上升，直至在衰退之前的晚期阶段出现“过热”，然后通胀压力减缓。Fidelity 进行了一项[研究](https://www.fidelity.com/viewpoints/how-to-use-business-cycle)，跨越 50 多年来确定在每个阶段表现最佳的行业。下面是一张图表（*来源:* Fidelity Asset Allocation Research），描述了商业周期和预期的相对行业绩效按阶段划分：

![商业周期](https://cssanalytics.files.wordpress.com/2013/02/business-cycle.png)

![按商业周期阶段划分的绩效](https://cssanalytics.files.wordpress.com/2013/02/performance-by-business-cycle-phase.png)

[研究结果](https://www.fidelity.com/viewpoints/how-to-use-business-cycle)表明，各个行业绩效存在非常稳健和显著的差异。***应用这种方法的问题在于，对于经济处于哪个阶段以及当前商业周期将持续多长时间存在相当大的不确定性（它们的持续时间可能从 6 个月到数年不等）*。** 因此，创建一个对商业周期有效中性的行业投资组合是合乎逻辑的。这可以通过生成在周期的每个阶段表现最佳的四个不同投资组合，然后根据阶段长度和绩效差异进行加权来实现。得到的投资组合应该会在时间上表现得非常好，并且比更为简单的分配方法具有更大的一致性。

要创建“全天候”行业组合，我使用了一个简单的评分系统来捕捉行业和阶段表现的相对差异。选择使用排名/评分模型而不是实际数据，可以避免使用过去的行业回报和历史阶段周期长度所带来的噪音，这在原始幅度上更难以推断。理论上，相对有利性和周期长度应该更加稳定。阶段长度和相对表现均排名（从高到低）。通过将长度排名乘以相对表现排名，产生累积权重。这决定了四个组合（早期、中期、晚期和衰退）的相对权重。在每个组合内，根据相对有利性，为每个行业分配一个分数。对于给定阶段，历史上表现最佳的行业得到 3 分，显著表现的行业得到 2 分，表现中性（匹配市场）的行业得到 1 分，历史上表现低于市场的行业得到 0 分。我编制了一个[全天候行业工作表](https://cssanalytics.files.wordpress.com/2013/02/all-weather-sector-worksheet.xlsx)来更详细地展示计算的细节。以下是“全天候”行业组合的最终复合和分配细节：

![全天候行业](https://cssanalytics.files.wordpress.com/2013/02/all-weather-sector.png)
