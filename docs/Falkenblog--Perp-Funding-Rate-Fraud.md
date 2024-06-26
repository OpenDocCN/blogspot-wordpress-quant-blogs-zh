<!--yml

类别：未分类

日期：2024 年 5 月 12 日 19:56:40

-->

# Falkenblog：永续融资利率欺诈

> 来源：[`falkenblog.blogspot.com/2022/11/perp-funding-rate-fraud.html#0001-01-01`](http://falkenblog.blogspot.com/2022/11/perp-funding-rate-fraud.html#0001-01-01)

据说，永续合约资金费率使期货/合约市场得以在不交割的情况下以现货价格达到均衡，因此市场是一个永续互换，简称为“永续”。这一机制表面上类似于期货市场中的基差，但在理论和实践上却有根本的区别。事实上，人们对这种存在缺陷但似乎可信的反馈控制系统故事能够满意，这意味着必须牵涉某些必要的细节才能看出其为何行不通。基本的不一致在于资金费率最佳的预测者不是当前永续/现货价格比率，而是资金费率的移动平均。然而，如果事实确非如此，那么为何永续/现货比率被宣称定义正在使市场达到均衡的资金费率？

就实际情况而言，永续合约溢价并不能在永续市场上达到供需均衡；现货价足以满足这一功能。永续市场追踪现货市场的主要原因可以解释为[谢林点](https://zh.wikipedia.org/wiki/%E8%B0%A2%E6%9E%97%E7%82%B9)或[相关均衡](http://www.millenniumpost.in/sundaypost/beacon/the-ace-game-theorists-453467)。永续合约溢价并不能决定资金费率，而是由内部市场制定者针对每个交易所作出的资金费率决策确定的。交易所一般以各种程度控制这些内部人员。鉴于 DeFi 永续合约交易所目前已有数百亿美元的未清结余，中心化交易所上的未清结余更是数倍于此，即使您典型的永续交易者似乎对此持无动于衷的态度，这一喜剧的经济意义也是巨大的。

七年前，不可能做空或杠杆持有比特币的多头头寸。所有人只能交换一种代币以获取无杠杆的多头头寸。当时还没有稳定币或包装比特币，因此该任务是寻找一种在没有美元的情况下交易比特币的方法。2016 年，中心化交易所 BitMex 创建了第一种受欢迎的永续合约，这样就能在只使用比特币进行交易的情况下进行杠杆头寸。

永续合约没有到期日和结算，它通过资金费率机制将其价格锚定到现货价格。当永续合约的价格超过现货价格时，标准的解释是这意味着多头需求多于空头需求。为了使市场平衡，多头交易者向空头交易者支付与价格溢价成比例的费用。加密货币资金费率阻止了两个市场的价格持续分歧。BitMex 的资金费率每 8 小时应用于当时处于活动状态的每个持仓。8 小时窗口现在已成为报价的约定，尽管当今的资金费率应用有时是按小时或连续进行的。

永续合约溢价定义为永续合约价格与现货价格的百分比差值。现货价格可以来自 Coinbase 等外部市场，也可以来自自己交易所的现货市场：

永续合约溢价 = 永续合约价格/现货价格 - 1

资金费率就像期货每天到期一次。例如，如果你卖出的比特币永续合约的价格一直比基础指数高出 0.03%，那么在当天或隔天，你将收到总资金费率支付的 0.03%。如果比特币在一系列交易所的当前市价为$20,000，资金费率机制将帮助确保永续交换合约的价格随时间也围绕着相同的$20,000 水平定价。

在 3 万英尺的高空，这一切看起来都是合理的。我没有看到任何人质疑它的逻辑。即使是金融领域的著名教授[坎贝尔·哈维](https://www.youtube.com/watch?v=BZSARSWrnaA)， 他对传统期货数据和理论非常熟悉，也接受了这一逻辑。永续合约将比特币衍生品推向了引人瞩目的地位，并激发了新的交易所提供永续合约。这通常是必要的，因为当时存在许多限制（没有其他区块链的稳定币或封装币）。随着时间的推移，交易者对这种产品变得更加舒适，并相信它的永续合约溢价/资金费率机制是有效的。

一百年前，槽货商店是人们交易主要交易所上市股票的常见方式。商店会接受赌注，并给予最高 100 比 1 的杠杆，交易股票、谷物、石油等。并没有股票或商品的转让交割，因此客户实际上是在和槽货商店经营者赌博。通常情况下，股票价格并不真实，但即使是真实的，更资本化的槽货商店管理员也可以操纵价格以耗尽客户的保证金。尽管有些人以为他们是在与'真实'的证券价格交易，但另一些人知道它并不一定与交易所的价格相关，但他们觉得足够接近。这些实际上是在经历了 50 年后于 1922 年被禁止，突显了即使明显不可持续的坏商业行为也能持续很长时间。

目前的永续加密货币期货市场与非法期货交易所有很多共同之处：操纵、缺乏真正的交割、100-1 杠杆、对交易乐此不疲的冷漠赌徒们。不幸的是，监管机构的高压态度给愿意并且有能力的加密货币投资者提供了很少和不太具吸引力的选择。你可以在芝加哥商品交易所做空，但最低名义金额为$100k (5 比特币)，并且做空头部位的保证金为 150%。在时间上，投资期货交易的入门费用很高，需要将资金从股票经纪人处转移到一个处理期货的机构，并且会有很多关于你的资金来源的问题。如果有一个简单的加密数字货币 ETF，数百万投资者将能够以更安全的方式做多，并避免不良的永续市场，ETF 还能给人们做空的机会。这使大多数加密货币投资者通过区块链可以访问的交易所（例如，[dydx](https://dyds.exchange/)）或者更明确地通过 VPN 和虚假身份在海外的中心化交易所来进入未受监管的交易所。监管机构的零容忍态度严重损害了零售加密货币投资者，因为它严重限制了加密货币投资者的受监管的机会。

我不指望监管机构会接纳加密货币。它将被强制性地推向他们，就像政府官僚发现禁止加密技术对技术上是徒劳的，或者 UBER 暴露了低效的出租车垄断，并且使其恢复到旧体系变得在政治上不受欢迎。然而，在加密货币 dapps 等未来的加速发展的关键是暴露不良做法，以便消费者可以做出知情的决定。竞争是历史上最好的监管机构，它包括积极的建设性批评，而不是天真的批评，担心自己的垄断权力的无知官僚们的批评，以及由加密媒体资助的比特连接的最新版本的容易轻信的报道。

**资金费率理论**

为了理解这个问题，你必须首先理解期货/掉期市场中的资金费率是如何运作的。在期货市场中，基差的作用就像掉期市场中的资金费率，它定义为期货价格和现货价格之间的差异。图 1 显示水平时间轴从当前期货价格移动到交付/到期日期，如果黑线代表当前现货价格。

**图 1**

“基差”是期货和现货价格之间的差异。它可以是正数或负数。“基差”的摊销可以被视为每日资金费率；在*顺差*中，多头向空头付款，而在*逆差*中，空头向多头付款。资金费率隐含于基差随时间的摊销中，在到期时，现货价格等于期货价格，因此在那时，“基差”肯定为零。

利率亏损没有任何关于掉期市场的依据；而是，每日应用融资利率，与期货市场的基础完全相同。它们使用事先已知的融资利率每日结算。这里，基差从隐性变为显性。

长期利率亏损（t+1）= 名义本金（t）* [p（t+1）/ p（t）- 1 - 融资利率]

不幸的是，关于基差率和融资利率的文献在定义基差或融资利率时并不一致。你可以在一本书中看到基差 = 期货 – 现货，在另一本书中看到基差 = 现货 – 期货。我将坚持加密货币的约定，定义融资利率如下：

正利率：多头付给空头（期货正向）

负利率：空头付给多头（期货反向）

套利确保资产的各种成本和收益反映在期货基差或掉期融资利率中。它们都是基于以下推理。

假设你有$1，并且想比较两种投资。首先，购买国债券。这将产生一个简单利率回报

$1*(1+R(us))

其次，您拥有资产 A。许多因素影响其净收益，但这可以由*Ret(A)*表示。要获得此回报，您首先必须将美元换算成资产 A；用$1，您可以获得 1/A 价格的 A 单位。您将在一定时期结束时将其重新转换成 F(A)美元。期货市场允许您在今天设定 f(t+1)的期货价格

$1/现货价格（t）*（1 + R(A)）*期货价格（t+1）

在这里，我们以美元/A 货币对的期货（F）和现货（S）价格的条件定义。我们期望这两个等式相等，否则不会是均衡状态。通过一些重新排列，我们得到

F(t+1) / S(t) = {1 + R(us)} / {1 + R(A)}

如果我们将此按照永续期权溢价的方式表达，那么将是

F(t+1) / S(t) - 1 = {R(us) - R(A)} / {1 + R(A)}

永续期权的溢价是由相对于资产 A 的净回报推动的。这些因素定义如下：

+   利率

做多一个现货头寸 100 美元会有机会成本，因此需要放弃无风险资产（如国债）的回报。如果没有此调整，一个人可以通过掉期做多某种资产，并赚取购买现货所需现金的无风险利率。黄金没有以下列出的其他属性，因此其期货价格仅由美国利率决定，始终处于正向（期货价格>现货价格）。然而，对于货币，两种货币都有利率，因此净利率仅有一半时间是正向的。目前，美国利率已经接近零，过去十年的效果是解释永续融资利率的二次效应（最多年化 2%）。

标准存储成本就像利息率一样，从*R(A)*中减去。它们包括保险和仓储成本，就像石油一样，也包括像农产品那样的腐败。长期现货头寸支付它们，因此长期互换头寸也必须支付，以长期期货价格随时间下降的形式，即正的资金费率。这些对加密货币无关。

对于支付股利的股票，在未来的价格会根据这一股利进行调整。例如，如果一只 100 美元的股票在即将到期的期货交割前有 10 美元的股利，预期到期时它将价值为 90 美元，因此从现价中减去股利就可生成远期价格。这对于没有股利的加密货币无关。

+   期权价值（又称便利产出率，存储理论）

大宗商品的库存底线为零，也有最大值。对于像小麦或石油这样有持续正消费流的资产，库存底线会导致绝望的用户抬高价格。这种短缺的期权价值导致现货价格高于期货价格，这就是为什么石油价格的逆向现象是普遍规律的原因。然而，有时石油罐会被填满，比如在 2009 年 4 月全球衰退的深处或 2020 年 4 月疫情关闭期间，当当月期货价格变负时。这对加密货币无关。

+   风险溢价又称套期保值压力

如果套期保值者净空头或净多头，他们必须支付投机者承担另一方，以转移自己的风险。凯恩斯曾声称这是一般的情况，他称之为“正常逆向化”。他的例子是，当农民在期货市场上出售他们预期的小麦产量时，通过增值向长期期货价格支付溢价，随着到期日的临近而支付。还有一些情况，套期保值者天生就是空头，比如飞机制造商通过购买期货锁定其铝材成本，短头通过期货价格下跌至现货价格而得到支付（顺价平）。对于加密货币来说，自然的多头故事最符合，因为矿工生成一系列加密货币，可能希望通过现在锁定价格来避险。这意味着负的资金费率。我想不出一个自然的空头故事，一个必须定期购买加密货币的群体。

这一理论是解释加密货币融资利率为何是正的标准论点（见币安[这里](https://www.binance.com/en/blog/futures/a-beginners-guide-to-funding-rates-421499824684900382)）。这不在传统融资利率解释的文献里。对资产需求的冲击应反映在当前价格而不是未来价格；说任何市场永远是‘多头多余空头’是错的。[Samuelson (1965)](https://investmenttheory.org/uploads/3/4/8/2/34825752/paulsamuelson-proof.pdf)证明，如果你知道明天需求会高，这会反映在今天的价格而不是未来或预期现货价格。这种推理是随机漫步假设的基础，尽管它受到批评，但对于任何资产价格的时间序列，它是一个极好的一阶近似。但是，人们必须承认加密货币的特殊情况：拥有或杠杆加密货币受到了前所未有的监管限制。因此，在像 2017 年末和 2021 年初这样的牛市中，被监管部门限制的额外需求推高了永续合约价格，多头愿意支付资金费用以获得他们在其他地方得不到的访问。

加密货币的融资利率通常是正的，表明合约溢价。存储成本、股息和期权价值对加密货币无关紧要。风险溢价只会意味着负的资金利率，因为天然持有对冲头寸的仅有人群为那些做多的人，比如矿工或需要加密货币运作的 dapp。美国的利率会有几个百分点，但很难假设稳定币会有这样的利率，因为你不能直接用稳定币购买美国国债。这留下了情绪理论，这是一种牵强的解释，但可能是合理的。

#### **融资利率数据**

平均而言，永续合约融资利率是正的：多头支付空头。大多数永续合约交易所将默认融资利率设定为每 8 小时 0.01%，年化后为 10.95%。下图 2 比较了 BitMex 和币安的比特币永续合约利率与芝加哥商品交易所期货隐含融资利率。平均而言，币安的融资利率比 BitMex 或芝加哥商品交易所高出 10%。我用第二张期货价格减去头寸价格乘以 12 来得到芝加哥商品交易所的年化融资利率，但这可能是个不准确的数字，因为第二个月很不流动，可能因交易不频繁而有偏差。

**图 2**

平均年化比特币融资利率

9/2019-6/2022

币安上更高的资金费率反映了更一般的资金费率，并且是由资金费率在某些月份飙升到 50%至 100%（年化）的场景推动的。资金费率的飙升与牛市之间存在明显的相关性，这就是为什么大多数评论者认为永续合约的资金费率是市场情绪的指标。随着时间的推移，我们可以看到，像许多永续交易所一样，币安在大牛市期间收取异常高的资金费率，并很少提供对称的负资金费率（BitMex 在这方面是例外）。

**图 3**

虽然不同交易所的资金费率高度相关，但差异可能很大。这些市场显然受到通过各种监管限制的套利的限制的影响，这突显了情绪理论的潜在可信度。

**图 4**

#### 同期对比与滞后回报效应

将币安的日资金费率回归分析与当天的回报以及上一个月的 ETH 或 BTC 回报相比显示，两者回报与资金费率呈正相关：高回报意味着更高的资金费率。然而，先前一个月的价格回报比当日回报更显著地解释了日 ETH 和 BTC 资金费率。

**图 5**

日资金费率的回归分析

币安，2019 年 8 月-2022 年 6 月

###### 因变量为 ETH 和 BTC 的日资金费率。数据每 8 小时生成一次，因此日资金费率是这些观测值的总和。回报是使用来自 Gemini 的分钟降采样数据计算的。日回报和上一个月的回报没有重叠。ETH 资金费率使用 ETH 回报，BTC 资金费率使用 BTC 回报。

在传统金融市场中，关于过去价格变动和基础的首要特征是，价格上涨与负的融资利率相关联，价格下跌与正的融资利率相关联。一般的解释是，价格激增是由于库存问题，即干旱，因此持续的消费需求需要今天异常高的价格，而这并不是预期将继续下去。由于缺乏油储存等原因造成的重大价格下降也有可能是暂时的，因此期货价格将高于现货价格。

将“过去价格飙升”与“当前价格飙升”混为一谈，并认为情绪资金利率相关性对于一个理性市场是有意义的。事实上，过去回报比当前回报要强得多，这与该论点相矛盾。加密货币资金费率与先前回报之间的正相关性是一个异常。

#### 永续套利金并非牛市的紧急指标

如果我们看看 BitMex 的 ETH 永续合约，"操纵内部做市商"理论就很清晰了。这个永续合约具有奇怪的特性，即包含了 ETH-BTC 的协方差，也就是说 BitMex 以 BTC 计价支付，但合约以美元定价。这篇帖子在[这里](https://efalken.substack.com/p/bitmexs-ethusd-funding-rate-anomaly)有更完整的解释，但要点是 ETH 永续合约的回报是

ret(ETH) * (1 + ret(BTC)) = ret(ETH) + ret(ETH) * ret(BTC)

术语 E[ret(ETH)×ret(BTC)]也被称为 ETH 和 BTC 的协方差。因此 BitMex 永续合约的回报是 ETH 的回报加上它的协方差。很少有人提到这一点，突显出，就像在旧的投机坑股店时代一样，大多数客户如此渴望赌博，以至于他们不关心。当我谷歌搜索"[BitMEX eth 资金费率过高](https://www.google.com/search?q=BitMEX+eth+funding+rate+too+high&rlz=1C1RXQR_enUS934US934&oq=BitMEX+eth+funding+rate+too+high&aqs=chrome..69i57j69i59.537j0j4&sourceid=chrome&ie=UTF-8)"的解释时，我会得到 2019 年左右的我的博客文章；其他文章只是指出了费率水平。顾客们心满意足地无动于衷。

尽管如此，显然，一些 BitMex 内部人已经弄清楚了这一点。从 2018 年 8 月到 2022 年 6 月的 ETHUSD 回报数据中，你会看到协方差项几乎完美地被解释了。在没有资金的情况下，他们的 ETH 合约总回报数据为 149%，而该期间的年化 ETH 回报为 83%。两者的差异 66%，与协方差和资金费率(63%)相匹配。

**图 6**

**BitMex ETHUSD 永续合约每日资金费率和回报数据的年化数据**

**2018-2022**

这一切都是合理的。BitMex 已经[声明](https://archive.ph/ONG7E)其做市商部门的目标是实现盈亏平衡。考虑到他们从手续费中赚取的大量资金以及监管机构惩罚他们的强烈愿望，这是一个明智的策略。ETH 永续合约的数据表明，他们的 ETHUSD 资金费率确实是中性的，即经过协方差计算后，为零。他们做得很好！

有趣的是，很少有人看到资金费率和协方差之间的直接关系。由于比特币和以太坊之间的相关性是正的，它意味着持多头仓位存在凸性。就像凸性在任何地方一样，这是你可以对冲来最小化风险的东西，但它是对持空头凸性的不可避免的成本。Arthur Hayes 在一篇[博客文章](https://blog.bitmex.com/is-the-ethusd-swap-fairly-priced/)中写到 ETHUSD 永续合约是否被合理定价，并没有提到这个明确的公式。

**图 7**

[彭博欧元美元/掉期页面](https://archive.ph/ONG7E)

在传统市场上，一旦了解，凸性调整就是明确的。例如，上图 7 显示了一张彭博页面，显示了比较欧元美元期货和欧元美元互换需要的详细[凸性调整](https://www.cmegroup.com/education/courses/introduction-to-eurodollars/understanding-convexity-bias.html)。在了解这种关系之前，一些大型投资银行通过做多期货做空互换实际套利获利。然而，大约在 1995 年左右，许多着名的学术文章强调了这种套利，并指出了准确的凸性调整。欧元美元期货和掉期交易员在用于比较这两个市场的定价模型中已经将这种凸性调整内置，套利通过此调整使价格平衡。交易者不会隐式地调整凸性；他们会精确地通过上述模型来应用它。

像许多 CEO 一样，哈耶斯似乎对公司实现目标的各种技术策略（平坦的市场做市利润）毫不知情。ETHUSD 市场做市商使用明确的调整，但由于对此信息的需求很小，最好不要提及，因为比大多数人拥有更好的模型给了人一种有用的选择。

#### **永久理论**

当提及永续合约时，通常参考这两篇学术文章。第一篇是[Gehr (1988)](https://www.gwern.net/docs/economics/1988-gehr.pdf)，它描述了黄金在香港中国金银交易所（CGSE）上的交易。需要记住的是，这是在当时交易不可能全天候进行，并且没有互联网，因此在交易时间之外，收盘价格波动很小。CGSE 是独特的，因为它的期货市场是无日期、永久的（它至今仍在[运作](https://industrialhistoryhk.org/the-chinese-gold-silver-exchange-society-hong-kong-established-1910-new/)，我对它今天的协议不太确定）。该市场实际上是每日结算，然后进行 30 分钟的拍卖过程来确定资金费率。那些持有多头黄金的人将比较支付长头寸的存储和利息成本与资金费率；持有空头黄金期货的人如果认为资金费率太低就会交割。这个资金费率被增加到即期价格上，以创造后续一天的 PNL 的基础。

在 CGSE 期货市场上，价格和现金流的影响如下。如果市场价格收盘为 100.00，并且所确定的资金费率为第二天的 0.01%，则第二天的 PNL 的基础为 100.01。如果价格每天保持在 100.00 不变，那么多头将损失 0.01，因为每日的 PNL 将在多头头寸上为 100.00-100.01，其中 100.00 为即期收盘价，100.01 为前一天的期货收盘价。交易价格永远不会是 100.01；它只会用于交易者保证金调整的日常计算中，从多头转移到空头。

诺贝尔奖得主罗伯特 [希勒（1993）](https://www.nber.org/system/files/working_papers/t0131/t0131.pdf) 提出了一种用于像单户家庭这样的东西的永续期货合同。与股票指数或商品不同，基础资产很难转化为期货商品，因为很难定义一个住宅单位。一百套房子？10 万平方英尺的房子？质量差异很大，导致了 [柠檬问题](https://en.wikipedia.org/wiki/The_Market_for_Lemons)。希勒提出用租金指数来为房屋价格指数创造一个租金回报代理。人们会应用统计方法来估计房地产的平均租金回报，扣除折旧。然后这个租金回报将由空头支付给多头。

s(t+1) = f(t+1) - f(t) + d(t+1) – r×f(t)

这里 *s* 是交易账户的日度保证金变动； *f* 是永久期货价格，*r* 是精确的法定货币利率调整，而 *d* 则是市场外部确定的。尽管这很有趣，但 *d* 产生可靠的租金指数的困难很可能是为什么这从未被实施过的原因。就像经济中的利润一样，通过宏观经济指标估计租金收入是非常困难的，人们不喜欢交易建立在 R2 较低模型上的资产。尽管如此，市场只是用一个不包含每日资金费用 *d* 的现货价格进行交易。

永续溢价 *类似于* 交易后加上的 CGSE 资金利率费用在市场的现货价格。直接资金利率是希勒模型中的 *d(t+1)* 项一样的定期支付。然而，希勒和格尔的永续模型是替代品，而非互补品；资金利率要么定期加到现货价格中，要么定期收费。此外，格尔的简短、从未交易的永续溢价 *是由* 明确的资金利率拍卖确定，而不是反过来。因此，从 30k 英尺来看，永续溢价与资金利率之间的联系似乎与格尔的模型一致，但完全颠倒了；永续资金利率机制似乎与希勒的模型一致，通过明确的资金利率收费，但完全以不同的方式确定（与市场外部因素有关）。

#### **资产价格的普朗克尺度**

在加密永续合约中，模态每日资金费率和永续合约溢价为 0.03%，年化为高达 11%。考虑到过去几年利率几乎为零，这是一个显著的资金费率。然而，0.03% 低于任何“真实价值”的估计或交易成本的精度。对于最流动的美国股票，其平均交易成本至少为 0.1%（参见 [这里](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3229719)）。鉴于明确的费用起点约为 0.1%，加密价格不太可能具有更低的交易成本。Gemini 的交易数据显示，从一次交易到下一次的价格标准偏差为 0.15%。一种单向交易费用为 0.2%，这意味着价格必须偏离其“真实”价格至少 0.2% 才能进行套利交易，这使得永续期货市场价格具有 0.2% 的不确定性区间。然而，尽管存在所有这些不确定性，我们预期市场将以比这些限制精度更高几个数量级的精度确定资金费率。

#### **锁定资金费率**

加密永续合约类似于标准可交割期货基差，因为价格始终反映了基差和现货价格。然而，由于永续合约溢价是连续应用的，其大小与任何交易决策无关。考虑永续合约交易员看到永续合约价格为溢价 0.0685%，意味着卖空者有 25% 的高资金费率。问题不仅在于这种溢价低于资产价格普朗克长度，还在于她交易时的永续合约溢价并不确定她将获得的资金费率。相反，这个溢价是她持有头寸的时间的平均值。鉴于下一个跳跃会使永续合约价格上涨 0.1%，当前永续合约溢价 0.06% 具有较低的前瞻价值。暗示着极端大资金费率的永续合约溢价不足以激励开立头寸，因为当前永续合约溢价的信息内容很低（特别是与过去资金费率的简单移动平均相比）。

套利在可交割期货市场中要简单得多。期货交易员在交易时锁定了一个累积资金费率。从期货基差隐含的资金费率是一个累积率，经过多天生成一个高于交易成本的目标回报。每月或每季度的交割意味着年化资金费率为 11%，这将显示为与现货价格相比高达 1% 或 3% 的溢价，而不是 0.03% 的溢价。在具有相同的每日资金费率的情况下，在期货市场上可能存在真正的套利，即在没有不确定性的情况下获利，但在永续期货市场上是不可能的。

#### **传统金融交换资金费率**

许多对冲基金为其国际股权头寸使用掉期账户。这方面有几个监管原因，但最终结果是，投资银行充当股票的托管人，对对冲基金的股票收取资金费率，并在投资组合基础上应用保证金待遇。值得注意的是，对冲基金指挥他们的交易，就像他们管理自己的交易一样。资金利率是独立于交易确定的。

在美国，做空股票需要先行“定位”，因为裸卖空已不再允许。对于需求量较大的空头股，卖空者将得到他们可以卖空的股数*和*特有空头回扣。一旦知道了这些，交易者就像任何其他卖空交易一样，在市场上进行卖空。与 CGSE 一样，交易现货价格和资金利率是在不同的市场上确定的，而不是像期货一样同时确定。

#### **相信他们**

受监管的市场必须呈现其市场交易和订单的经过审计的记录。例如，[MIDAS](https://www.sec.gov/marketstructure/midas-system)每天从所有国家股票交易所收集大约 10 亿条记录，时间戳精确到微秒。他们正在寻找市场操纵或在特定时间未根据一揽子买卖价格给客户最佳交易的情况。加密货币交易所不受此类审计监管，这使得他们在重要场景中拥有相当大的自由裁量权。

永续合约交易所以加权平均的永续溢价在不同频率下公布资金利率。他们用来对标自己构建的地方指数的现货价格必须是实时的，而不是下采样的历史数据，因此他们的“指数”价格无法以很高的精度知道。永续价格可以以各种方式计算，例如使用前一结束价或“影响价格”，该价格查看交易时的限价委托簿，看看对买卖双方价值为$10k 名义价值的中间价的平均价。将永续价格和现货价格（也就是“标记”价格和“指数”价格）联系起来获得溢价将取决于几条未提及的规则。考虑到每个交易刻度都会上下波动 0.15%，根据这些自由度获得的任何永续溢价都将至少具有 0.05%的标准误差，从而使他们能够在 36%的波动范围内发布任何资金利率（0.05% —> 18%年化，-0.05% —> -18%年化）。

#### **内幕人员**

做市商在所有交易所中主导价格设定。他们可以决定以当前现货指数的 0.03%或 0.13%为目标。作为做市商，这将决定通过使用上述各种自由参数进行汇总生成期望的资金费率的一般模式。这些专业人士要么在中央限价委托簿（CLOBs）中发布买卖价差，要么作为自动做市商的套利者。

通常，他们明确为交易所工作，就像 BitMex 公平的 ETHUSD 市场做市商一样，或者在一个不太明确的合作伙伴关系中这样做。交易所需要流动性，通常通过给予某些特定群体对其订单簿的特权访问或零售交易者无法获得的高速访问而获得这种流动性。总的来说，我们应该期望加密永续市场做市商净持平但空仓永续，因为在永续市场外持多仓要比持空仓容易得多。例如，如果 Binance 的市场做市商净持多仓，他们将不得不信任 FTX 等另一个交易所来赋能他们的空仓，监管机构将成为维持这样一个头寸的瓶颈。相比之下，如果 Binance 市场做市商净持空仓，他们只需在区块链上拥有加密货币并进行对冲。最终结果将是，除了通过买卖价差和手续费获得标准市场做市商的盈利能力外，他们还可以从他们的无风险加密头寸内的自然空仓永续头寸中获得额外的 10%融资费率。很荒谬，客户接受这作为默认融资费率的现状。

[一个引人注目的例子](https://insights.deribit.com/market-research/the-quest-for-perp-amms/)是由 perp.fi 的“虚拟”AMM 提供的，内部人为交易者提供流动性（今年春季关闭）。随着 ETH 价格上涨，交易者通过不变产品 AMM 的逻辑是净持多仓。然而，融资费率为负数，意味着持多仓的人收到了融资费率。这与 2021 年所有其他永续交易所相矛盾。这是因为那些持多仓的人，与 perp.fi 内部人不相关，决定成为 perp.fi 交易所的市场做市商，而 perp.fi 没有能力或计划制止他们。显然，市场做市商决定了永续溢价，因此决定了融资费率。这就是市场做市商的工作。永续/现货价格比不反映‘多头需求’，而是市场做市商的融资偏好。

#### **结论**

这种奇怪的情况源于需要为人们提供一种以杠杆长和空交易加密货币的方式。永续溢价模型无法按照宣传的方式运行，更重要的是，它无法运行。它鼓励了充斥着 DeFi 的粗心思考，并催生了建立在庞氏经济学上的不可持续的商业模式。例如，[一个网站](https://phemex.com/user-guides/funding-rate)解释了永续价格高于现货价格的原因：“逻辑上，这意味着有更多的交易者持多头仓位。”没有人应该把钱投入到由持有这样逻辑的人经营的 dapp 中，因为它必然延伸到他们的代币经济学中。

解释正回报/资金费率相关性的理论是典型的非平衡故事，听起来不错，但没有任何意义。就像解释有“更多的买家比卖家”，即长期需求显示在期货价格溢价中听起来合理，但在逻辑上是不连贯的。标准套利和期望法则表明，当前情绪反映在现货价格中，而不是远期利率。这就是为什么资金费率通常独立于资产价格，为什么对汽车购买的需求并不会对汽车融资利率产生实质性影响。此外，先前一个月的回报，而不是同时的回报，最能预测资金费率。

过去的回报与供给冲击期间的基础呈正相关，其中库存接近零或耗尽。然而，在加密货币之外，我们看到高价格对应负资金费率，低价格对应正资金费率。这与我们在加密货币中看到的完全相反。

所谓的永续期权（perp）资金机制据说是一种自发的市场过程，无指导性，但隐藏了永续交易所控制做市商，他们在可能的时候操纵资金费率。当价格暴涨时，用户并不在意百分之百的年化资金费率，这相当于仅有百分之零点一的日费用。这就像在拉斯维加斯大赢家经常给荷官大费的情况一样：人们不尊重[赌场的资金。](https://www8.gsb.columbia.edu/sites/decisionsciences/files/files/thaler_and_johnson.pdf)2021 年 2 月永续期权资金费率相对于 CME 的额外 50%以上增长反映了内部人员尽力获取利益。 

永续期权的客户和加密货币爱好者喜欢相信加密项目像市场经济一样去中心化：高效、自发和不可审查。更可能的故事是永续期权的做市商们一般都持空头，并收取高达 11%的资金费率，这些都进入了做市商的盈亏表。考虑到监管问题，BitMex 或 FTX 的内部人员很容易通过持有永续合约的空头仓位和区块链的多头仓位来实现净平仓位。如果他们在永续合约上持有净多头仓位，他们就必须在其他地方持有空头仓位，这将是有问题的。

解决方案是摆脱永续期权，回归有交割的期货。当 BitMex 首次提出永续期权时，还没有稳定币或包装比特币等，但现在已经有了。有了一个交割，你就不需要明确的资金费率，因为基础很好地适应了存储成本和法定利率。
