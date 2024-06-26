<!--yml

分类：未分类

日期：2024-05-18 14:00:30

-->

# 一劳永逸——量化金融家

> 来源：[`quantumfinancier.wordpress.com/2011/04/24/one-size-does-not-fit-all/#0001-01-01`](https://quantumfinancier.wordpress.com/2011/04/24/one-size-does-not-fit-all/#0001-01-01)

在我们对交易圣杯的永恒追求中，经常会诱惑我们试图找到一个“终极”信号（指标）并将其应用到尽可能多的工具上。这种单一的解决方案在很大程度上是失败的，想想一个工具箱里只有锤子的木匠（或者她是；量化金融（QF）倡导性别平等）。尽管使信号适应性是绝对有所改进的，然而，我认为我们有时会错过重点。

与其将一个信号*ad absurdum*优化到改善回测，不如从大局出发。一个信号本身只包含这么多信息。虽然有很多表现很好的指标（博客圈在这方面是一个丰富的生态系统）；当与其他包含不同信息的信号结合时，它们的力量会更加放大。秘密在于信号聚合。换句话说，我们如何形成并使用一个信号集合，隔离不同的信息片段来构建一个有利可图的策略（注意我用的是策略这个词而不是系统，除了精心挑选词汇之外，两者的区别是至关重要的）。这是一个我最近一直在深入研究的话题，我认为博客圈是一个分享我一些发现的绝佳论坛。作为一个开始，以下是一些我将在接下来的系列文章中涉及的观点。

1. 集成方法背后的基本直觉是什么，它们为什么能帮助构建交易策略？

2. 我们如何隔离和量化特定的信息片段，然后观察它们对我们交易的工具产生的影响。

3. 我们如何评估信号当前的相关性。

4. 最后，我们如何汇总所有有用的信息并从零开始构建策略。

将通过一个简化示例来解释机制，以便读者可以跟随，但直觉将与博客上首次实时跟踪的第一个 QF 策略背后的直觉相同。我暂时还没有一个花哨的名字，但它在正式发布时会有的。

量化金融（QF）
