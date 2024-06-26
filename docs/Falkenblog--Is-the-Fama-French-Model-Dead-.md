<!--yml

category：未分类

日期：2024-05-12 19:58:58

-->

# 弗雷肯博客：法玛-弗伦奇模型已死？

> 来源：[`falkenblog.blogspot.com/2020/01/is-fama-french-model-dead.html#0001-01-01`](http://falkenblog.blogspot.com/2020/01/is-fama-french-model-dead.html#0001-01-01)

当我在 90 年代初在西北大学读研究生时，热门的金融话题都与寻找和估计风险因素有关：通过潜在因素的套利定价理论（

[Connor 和 Koraczyk](http://mural.maynoothuniversity.ie/8439/1/1-s2.0-0304405X86900279-main.pdf)

1986），卡尔曼滤波状态空间模型（如，

[Stock 和 Watson](https://www.nber.org/papers/w2772.pdf)

1989），以及

[MoM（矩估计法）](http://larspeterhansen.org/lph_research/proofs-for-large-sample-properties-of-generalized-method-of-moments-estimators/)的证明

估计者（Lars Hansen 1982）。这些吸引了中心极限定理证明，这是学术梦想，因为数学证明决定性地证明了客观的元知识，

*如何*

知道重要的东西。学习这样的方法需要智慧和努力，承诺了即时的准入壁垒，而且肯定不是来自那些聚会更好但不懂统计学，更不用说测度理论的粗鲁的商学院学生。

大约在同一时间，尤金·法玛和肯·弗伦奇正在简单地将低股息率和高股息率股票的回报进行排序，并观察这些投资组合的基本统计数据（请看

[这里](https://pdfs.semanticscholar.org/4622/4481150e76d784ca057f2cf647a64b0c9585.pdf)

)。尽管法玛因其关于定义有效市场的理论工作以及他的后来确认资本资产定价模型（即 CAPM）的重要 1973 年的论文而备受尊敬，但他似乎就像是那些充斥 1970 年代的古老经济学家中的一个。确实, 如果你读那些老论文，你会惊讶地发现它们是多么简单--你可以在一读懂它们--这使得许多必然的假阳性显而易见（从后来看）。

但后来在 1992 年，法玛和弗伦奇发表了他们的

[票房炸弹三因子模型](http://home.cerge-ei.cz/petrz/gdn/Fama_French_92_tables.pdf)

证明，如果你首先按尺寸，然后按 beta 值对股票排序，样本中没有 beta 值与股票之间的相关性。先前的发现是

*被遗漏的变量*

，尺寸。也就是说，一个人可能看着人类，发现头发长度与身高呈负相关：头发越长，人越矮。但是如果你注意到女性比男性头发更长，并对此进行控制，相关性就消失了；头发与身高无关。

大小和价值在 70 年代后期被发现，往往出现在会计杂志上。法马和弗伦奇的分析很简单，但结果太强大以至于不能够忽视，尤其是因为法马并不是一些会计菜鸟，而是一个能够理解风险和预期回报的人。法马和弗伦奇假设大小和价值溢价意味着它们代表了影响投资者的风险，但学者们无法测量，正如我们能够看到暗物质的效应，但无法看到暗物质本身。

然而，许多研究人员误入歧途，大小和价值的发现方式也是相同，简单地找到一个强烈的模式，就认为它是真实的，而不是一个顺序统计学（见

[在这里](https://pubs.aeaweb.org/doi/pdfplus/10.1257/jep.3.1.189)

DeBondt 和 Thaler 在 1989 年左右列出的异常情况）。虽然 F-F 说它们是风险代理变量，似乎

*特定的目的*

.经济理论暗示了风险溢价

*必不可少*

视角要素的经济学模型，效用函数暗示了风险溢价

*当且仅当*

关系（这意味着 B ⇒ A 和 A ⇒ B）。[我的看法：这里的错误在于将其应用于个体财富，它对冰淇淋和鞋子效果很好] 再加上 20 年，经济学家发现 CAPM 模型已经得到证明（“同行评审事实”，他们今天会这样说），然后你就会有一种强烈的偏见，这种偏见不会在一些简单的分析后被丢弃。您可以通过他们是如何通过瞬时条件引入他们的发现来识别过去--许多人仍在从事他们的工作--（见

[Harvey and Siddique](http://pages.stern.nyu.edu/~dbackus/GE_asset_pricing/disasters/HarveySiddique%20skewness%20JF%2000.pdf)

， 1999)，或识别负载、因子回报和风险价格的因子模型，λ（见

[Ang et al 2006](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.319.1161&rep=rep1&type=pdf)

)。

然而，大小和价值投资变得受欢迎。Dimensional Fund Advisers 创建了一个非常成功而有影响力的量化交易平台，大小和价值成为基金标志或风险因素，具体取决于具体应用。在黑暗时期，比如大小因子在 80 年代末和 90 年代中期出现问题，或者价值股在科技泡沫时期遭受重创，但它们总是反弹：它们是有风险的！而隐变量模型、卡尔曼滤波器和 GMM 的严格方法在金融领域却没有产生实际成效。

简单模型长期获胜，但短期总是被混淆者所主导。苏格拉底和耶稣分别批评了诡辩家和法利赛人，因为这些官方知识分子是假正经的吹毛求疵者，错失了大局。基督教辩护士是中世纪最重要的学者，尽管现在

*辩护者*

“精英主义者”是对教条主义者的贬义称呼，关键在于复杂的推理一直被用来掩盖教条思维。精英们利用他们的知识优势来争辩，而不是寻找真理。那些复杂、难以理解的辩论，得到了大多数其他知识分子的支持，是不可能被反驳的。如果人们认为这一切都是浪费时间，就没人会花大量时间去理解这些论点，所以所有能够和他们争辩的人都是信徒（例如，我最初想成为一个宏观经济学家，但很快就意识到这是毫无意义的，所以今天我无法对主流的宏观模型进行深入的批评）。

简单的模型更容易发现真理，因为它们更容易被他人复制和检验，这是真理和重要性的最好证据，因为有效的事物随着时间的推移往往被复制。它们还暴露了愚蠢的推理和过度拟合，因为读者可以理解它们。复杂性并不能克服过拟合，它只是更好地隐藏了它。GMM 估计量很少因拟合过度而受到批评，因为很难说清楚，当没有人因为最古老的统计罪而被抓到时，你可以肯定它是猖獗的（例如，当 UFC 有类固醇问题时，没有人被抓到）。

更重要的是，真正深刻的金融思想并不多。我的第一反应是，我考虑了波动性与时间的平方根成正比、布莱克-斯科尔斯模型，或者利率远期与期货中的凸性调整等。然而，这些内容都可以在一次交流中传达给懂基本统计学的人。对于上面那些花哨的方法来说是不可能的。

虽然法玛-弗伦奇模型因其简单性而蓬勃发展，但我们现在正处于另一个黑暗时期。具体来说，在 2015 年由法玛-弗伦奇引入的 5 因子模型已经报告了以下各因子的月平均收益（不包括无争议的市场风险溢酬）：

然而，自出版以来，结果是这样的（注：它们应该是积极的）：

与以往的黑暗时期不同，现在除了法玛和弗伦奇的 5 外，我们还有大量其他因子。过拟合是一个长期存在的问题。与亚马逊和 Netflix 使用的“大数据”不同，因子数据规模要小得多，增长速度非常缓慢，与此同时，成千上万的全职研究人员正在寻找同样的数据新模式。他们都极其积极地寻找新的、更好的因子，我们都知道当你长时间折磨数据时会发生什么。3 因子法玛-弗伦奇模型的简单性并不是一个平衡状态，因为这促使许多人忽略一些因子并创造自己的因子（甚至法玛和弗伦奇也加入进来，增加了另外 2 个因子）。现在，与以往那些复杂方法一样，因子推动者们的推理是一样倾向性的和不诚实的，我们只是已经习惯了它。

这对在对冲基金应用的权益因子尤为重要，至少有 20 种，并包括正交估计的风格因子，还有没有人认为有回报溢价的行业因素。各种权威机构都普遍采用权威性论据，唯独科学家们采用这种策略是因为他们有多个微妙的假设，并通过引用多个有很好引用率的同行评议的文章来证明这些假设，而这些文章本身又是一样的做法，使得它不可能被驳斥，因为没人有那么多时间。我从未见过那些因子如何帮助管理风险的充分论据，但我了解它们在解释为什么上个月收益下降时是非常有用的。做作和地方性行话使得普通（即愚蠢的）风险管理人员、高级执行官、基金顾问等更容易感到有价值：他们知道一些外行不懂的东西，而那些外行又无法证明它不是空话。

没有任何金融研究人员能就权威因子的规范集合或最佳代理方法达成一致意见。虽然没有人提出卡尔曼滤波器，但每个人都对他们的价值因子有一些微妙的扭曲，如何定时因子，或者他们自己的创造。目前的失败导致很多人重新审视他们的因子，担心过去他们过度拟合模型，或者现在通过改变它们来做到这一点。在因子出现回弹之前退出的风险与坚持持有即将成为历史上的价格、应计利润和通货膨胀贝塔的风险是对称的。
