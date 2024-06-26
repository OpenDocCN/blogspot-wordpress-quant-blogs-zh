<!--yml

类别：未分类

日期：2024-05-12 21:49:58

-->

# Falkenblog：物理学家“解决”了双信封悖论

> 来源：[`falkenblog.blogspot.com/2009/09/physicists-solve-two-envelopes-paradox.html#0001-01-01`](http://falkenblog.blogspot.com/2009/09/physicists-solve-two-envelopes-paradox.html#0001-01-01)

我正在了解一个

[新解决方案](http://www.physorg.com/news169811689.html)

在一些科学/物理网站上讨论双信封问题：

> 澳大利亚的研究人员走出一步，解决了一个看似简单但尚未解决的悖论，称为“双信封”问题。他们制定了一种新策略，可以让玩家在增加报酬方面战胜游戏。该策略可能在优化投资收益和其他领域应用...研究人员解释称，该策略源自物理学、工程学和经济学领域出现的最新两态转换现象的进展.

嗯。每个人在一个两人零和交换中都可以获得更好的结果吗？请告诉我。我认为这个悖论来自于没有看到真正的状态空间。想到这些人认为通过“物理、工程和经济学新兴领域”的进展来从石头中挤血，真是有趣。断言他们的解决方案就像断言混合策略是占主导地位的

[蒙提霍尔问题](http://en.wikipedia.org/wiki/Monty_Hall_problem)

我认为他们通过特定的假设模拟得到结果。

先验

获胜分布.

问题很简单：

> 在两个信封悖论中，玩家必须在两个信封之间进行选择，一个信封中的金额是另一个的两倍。玩家可以打开他们选择的信封，然后他们有转换信封的选项。另一个信封当然有第一个信封的两倍或半倍的金额，但玩家不知道是哪一个.

看来，假设信封中有金额 $X，转换可以获得 0.5*2*X+0.5*0.5*X=1.25*X，比你拥有的$X 多 0.25 倍。但如果它们都应用这样的逻辑，那怎么可能是理性的，他们在零和博弈中有着同样的期望，正回报（一个人的得失是另一个人的损失）？

有

[许多已知解决方案](http://en.wikipedia.org/wiki/Two_envelopes_problem)

针对这个问题，有一些解法是不一致的，但我认为最简单的解法如下。

你可能认为你的信封里有 $X，并且可以交换成 $2X 或 $0.5*X，给你一个收益 New Envelope 减去 Current Envelope 的价值，或者 0.5*($2X+$0.5X)-$X，或者 +$0.25X。然而，你必须考虑，对称地，你可能是‘另一个人’，所以你的信封里是$2X 或 $0.5X。在这种情况下，你的预期收益相反，交换给你一个新的信封里有 $X，放弃了随机的 0.5*($2X+$0.5X)，产生了一个预期损失 $X-0.5*($2X+$0.5X)，或 -$0.25X。由于你以相等的概率处于第一或第二种情况，期望值为零，0.5*(+$0.25X-$0.25*X)。

看起来的悖论源于思考

你

拥有信封中的金额 $X （无论是翻倍还是减半），忽略你可能初始拥有的$2X 或$0.5X 的机会。如果一个玩家拥有$X，你有 50% 的概率成为那个人，25% 的概率拥有 0.5*X，和 25% 的概率拥有 2X。当你打开你的信封，看到$10，你不能假设 X=$10。在看到你的信封中的 $10 的条件下，它可能是 X=$20 或 $5。从概率的角度对所有情况进行权衡，交换并不会增加价值。
