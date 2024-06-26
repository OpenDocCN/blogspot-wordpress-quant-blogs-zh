<!--yml

分类：未分类

日期：2024-05-12 19:56:27

-->

# Falkenblog：另一种资本高效的 AMM

> 来源：[`falkenblog.blogspot.com/2022/11/an-alternative-capital-efficient-amm.html#0001-01-01`](http://falkenblog.blogspot.com/2022/11/an-alternative-capital-efficient-amm.html#0001-01-01)

Uniswap v3 引入了限制范围以解决自动做市商的资本效率问题。一种经济资本的替代方法是给予流动性提供者杠杆。我将这称为杠杆化的 v2 合同或 LAMM（杠杆化自动做市商）。

我制作了一个在 Rinkeby 上运行的原型[链接](https://sam-ruddy.vercel.app/)（你可以在[这里](https://rinkeby.etherscan.io/address/0xc81C35Fdb2aB020cb35Eb256e480c93be7a60bb2#code)看到合同代码）。

在 AMM 中增加杠杆除了资本效率外还有几个好处。例如，鉴于能够向 LPs 提供杠杆，向交易员提供杠杆是直接的。这意味着杠杆交换合同可以允许交易员进行做空和做多杠杆，以前只在永续合约（“永续”）市场中可用。这个永续市场的额外好处是不需要 Oracle，因为价格是由套利设定的，在这种情况下，一个定价不足的代币可以在 LAMM 上购买，然后在另一个交易所以更高的价格卖出。这避免了荒谬的资金费率溢价机制，这只是内部人员为了从用户那里榨取额外收入而进行的阴谋（要了解为什么它无法进行永续价格的套利，请见[此处](https://efalken.substack.com/p/perp-funding-rate-fraud)）。

使用杠杆型 AMM 相比于限制范围有几个其他显著优点。例如，使用杠杆账户可能会导致资不抵债，合同中需要有储备金或保险基金以防止合同资不抵债。在公司财务理论中，股权通常被认为是剩余的部分，是资本结构中承受第一次损失和获得任何额外收入的部分。股权持有者有权利和责任，因此他们会被正确地激励使合同运作良好；股权为重要的持续服务而收入。相比之下，向 Uniswap 增加的费用给予他们的股权持有者仅仅是对品牌的支付，这在开放合同领域似乎显得古雅。

### 预备工作

经典的 AMM 基于两个公式。首先，价格由池中代币的比率表示。例如，有 1500 美元稳定币和 1 ETH，价格将是 1500，这是常识。

第二，对于现有池子，ETH 进、USD 出的交易受到以下规则的约束：两个代币的乘积必须保持在其现有水平，即常数。

尽管这个模型有效，但无限范围是资本低效的。例如，如果您希望有足够的流动性，以便一个价值 10K 美元的订单将定价为 1500 美元的代币的价格移动 0.1%，则需要在池中拥有 4000 万美元的 ETH 和 USDC。对于稳定币来说，这是非常低效的，因为 99.999%的时间，价格被锁定在平价水平。

在 2021 年 5 月，Uniswap 发布了 v3，允许用户提供*受限*或*集中*范围。我在这篇文章[这里](https://efalken.substack.com/publish/post/72611169)中描述了 v3 的数学原理。在 v3 中，您使用上述相同的基础方程，但必须调整各个 LP 的 USD 和 ETH 池数量以反映它们的特定范围，并且还要跟踪所有可能价格的总提供流动性的向量。

通过注意所需的资本量与各种范围提供的相同流动性量之间的关系，可以看出资本效率。下面我们看到了各种范围大小所需的资本量占无限范围（即 v2）的百分比。

**图 1**

**各种大小的对称受限范围的相对资本**

**相同的流动性**

* 例如，一个定价为 100 的代币的 10%差价将在 90 和 111 处有界限（即 100/0.9）

如上所示，一个稳定币对，其中一个 LP 在 99.9 和 100.1 之间提供流动性，可以为相同数量的“流动性”提供 0.05%的资本。这个 v3 池子的资本效率将比 v2 高 2000 倍。

对于风险代币对，例如 ETH/USDC，覆盖上下波动 15%的范围相当于大约一周的波动率。只有当前价格在其范围内的情况下，流动性提供者才能收取费用，该范围被定义为“活跃”范围。如果一个人希望在一周的忽略后 95%确保他们的范围仍然活跃，像 ETH 这样年波动率为 90%的代币需要一个 30%的范围，这仅需要 v2 范围资本的 15%。

尽管市场价格可能突破所有受限范围，但这种情况对用户不构成风险；池子只会变得无关紧要。没有交易，因此流动性提供者不会产生交易费用，但是流动性提供者和交易者都不会有信用风险。如果所有 LP 范围都不活跃的池子就像是有一个可以以 10 万美元购买比特币的场所；没有人会使用它。在 v3 中，完全没有活跃范围的情况很少见，因为其他 LP 会出现来获取费用收入；第一个提供动态范围的流动性提供者将获得 100%的费用收入。

### **备选**

Uniswap 的集中交易范围并不是节省 LP 资金的唯一方法。事实上，作为 v3 风格方法，资本效率在区块链之外是缺失的，这并不是利用资本的最简单方法。尽管非常聪明，但这是路径依赖的产物，旨在通过添加几个参数来保持 v2 的标准功能。杠杆或其相反的保证金是常见的传统金融方法。请记住，杠杆和保证金只是同一枚硬币的两面，最大杠杆为 8 意味着需要 12.5% 的保证金。

考虑 Alice 为范围提供流动性，涵盖当前价格的+/- 10%，并具有与无限制池相同的流动性（以下简称为‘v2’）的情况。下面以 v2 情况作为 v3 的特殊情况，其中范围是无限的（从零到无穷大）进行了介绍。与上述图 1 保持一致，v3 范围所需的资金约为 v2 池所需资金的 5%。

**图 2**

**Alice 的 v3 LP 与具有相同流动性的 v2 LP**

我们可以通过杠杆来复制 v3 的资本节省，这意味着给 LP 一种资产和负债。假设 Bob 在一个杠杆 v2 池中提供了 1.32 ETH 和 1987 USDC，这与 Alice 在她的 v3 池中提供的代币数量相同。在这里，Bob 需要借出 '25.82 - 1.32'（24.49）ETH，还需要 36,742 USD。与 Alice 的额外帐户参数 pLow 和 pHigh 不同，Bob 具有对应于他借来建立 v2 范围的 ETH 和 USDC 的额外帐户参数。对于处于她的 v3 范围中的 Alice，以及处于他的杠杆 v2 范围中的 Bob，他们的帐户参数如下：

**图 3**

Bob 借入 24.49 ETH，以便除了他的初始 ETH 存款外，他在池中有适量的 ETH（USDC 也是如此）。这反映为他帐户中标记为‘vETH’的借方。最初，他的借款不会影响他帐户的市场价值；它创建了一种对称的资产和负债，相互抵消。Bob 的净或‘真实’ETH 为 1.32，与 Alice 的情况相同。

他们的帐户中的 ETH 和 USDC 的净金额相同，支持完全相同数量的流动性。随着价格的变化，这意味着它们的池金额也会发生变化，在两种情况下，这些金额都是代表 v2 池的隐含金额的虚构数字。池金额是杠杆 LP Bob 的资产。只要价格在 Alice 的范围内，Alice 和 Bob 的 LP 帐户价值以及 PnL 也将相同。这意味着它们的**临时损失**（IL）也将相同。

**图 4**

PnL 和 IL 之间的差异是初始投资的 1.32 ETH 的影响。鉴于他们的初始投资为 3975 美元，Alice 和 Bob 在 ETH 价格为 1500 美元时具有相同的帐户价值。这些方法在 Alice 的 v3 价格范围内产生相同的 PnL。

然而，在更广泛的价格范围内，这些方法存在显着差异。这是因为 Alice 的投资组合仅在价格范围之外保持不变。然而，Bob 的杠杆头寸会持续变化，以致当价格大幅上涨或下跌时，他的账户价值变为负值。[这完全忽略了费用收入，以使介绍更简单。]

**图 5**

尽管 Bob 在无限价格范围内的杠杆头寸更加危险，但在从$1000 到$2000 的广泛价格范围内，Alice 和 Bob 之间的差异很小。实际上，正如上面图 5 中指出的那样，当价格在 Alice 的$1350 到$1667 的范围内时，他们的盈亏是*相同的*。

Bob 的负账户价值，即破产，意味着需要一种清算方法来保护杠杆池，因为如果一个方有负账户价值，那么并不是所有账户都能够取回其全部账户价值。没有任何保险基金的破产将导致一场抢购，因为那些在池中拥有资产的人将希望尽早撤出以获得其总账户价值；而有了保险基金，股权所有者将遭受损失。

在上面的示例中，我们给 LP Bob 提供了 20 倍的杠杆，使他的 ETH 和 USDC 池大约是他初始“真实”的 ETH 和 USDC 存款的 20 倍。对 LP 应用的杠杆与将其提供给交易员是非常不同的。*LP* Bob 的账户在价格变动达到-50%和+95%时将破产，而拥有 20 倍杠杆的*交易员*在价格波动 5%时就会失去所有资金。由于以太坊的日常波动率为 5%，协议有足够的时间来预测和纠正潜在的破产风险，使其在实现之前得以解决。

然而，实际上，LAMM 更关心的是 LP 代币的赤字而不是破产。由于 Bob 的初始代币分配与 Alice 的 10%范围相匹配，+10%的价格波动将耗尽他的 ETH，而-10%的波动将耗尽他的 USDC。在下面的图 6 中的$1350 价格点处，Bob 的净 USDC 为零，就像 Alice 一样。

**图 6**

当以太坊价格下跌至$1350 时，Bob 没有更多的 USDC 可以提供，他的账户价值为$3674，仅损失了$301，或 7.5%。因此，在价格移动使 LAMM LP 破产之前，协议需要一种机制，要么激励 Bob 添加代币，要么激励新的 LP 添加代币，以便交换可以恢复。

LPs 在净非正 USDC 的价格，比如本例中的$1350，意味着在此价格以下无法进行交换。与 v3 一样，这对任何人都不构成危险，只是一个失去的机会。与 v3 情况不同的是，新的 LPs 不会像纠正此情况时那样获得所有费用，而是与现有 LPs 按比例分享这些费用收入。这削弱了在 LAMM 中提供必要的额外流动性的激励，除非有额外的机制。

实际上，将会有几个，甚至数百个 LP，每个 LP 都有不同的起始价格点，因此每个 LP 都有不同的净代币数量。一个具有净负面 USDC 的 LP 可能不意味着整体 LP 具有净负面 USDC 余额。立即清算具有负净代币头寸的 LP 并不是必要的，因为合同仍然可能具有两个代币的正净额。这意味着清算的规则不必假定单个 LP 的净代币赤字意味着完全的代币赤字。例如，当 Bob 的净 USDC 下降到-1000 时，他可以被清算，而不是 0。

请记住，在 v3 中，如果价格超过所有 LP 范围，池子也可能用完一个代币；从历史上看，这并不是一个重大问题。由于当池子用完一个代币时，LAMM 对于添加流动性的激励较弱，因此关键是创造激励，使得这种情况与 v3 池子一样罕见。这是一个有几种解决方案的问题。

### **激励 LP 保持正代币头寸的机制**

LP 的清算将是无缝的，因为不需要进行大额交易。LP 的清算只需将当前合同价格给定的“池子”ETH 和 USDC 添加到他的 vETH 和 vUSDC 账户，并将其 LP 流动性归零。LP 将留有一个带有正值但缺少一个代币的账户。合同可以要求 LP 在提取他的代币之前具有非负的 ETH 和 USDC 余额。在下面的示例中，价格已经下降到 1300 美元，导致 Bob 的 USDC 亏损了 686.83 美元。Bob 将被激励向合同存入额外的 686.83 美元，从而使他能够提取他的 3.24 个 ETH（价值 4212 美元）。一旦移除，情况就像一个 v3 池子没有活跃范围时的情况：对任何人都没有风险，只是新 LP 的机会。

**图 7**

一种解决方案允许新的 LP 在同时添加流动性时移除不足的 LP。例如，一个新的 LP 可以在添加流动性时指定一个存在缺陷的 LP。合同将检查以验证 LP 是否处于违约状态，然后在添加新 LP 的同时清算该 LP（这里，默认是由最小净代币余额触发的，而不是通常的市值与所需保证金之间的对比）。这将给新的 LP 更大的动力来纠正问题，因为这将使情况与 v3 相同，新的 LP 将受到 100%手续费收入的诱惑。

或者，可以通过给保管者提供激励费用来强调不足的 LP 的成本，以清算缺少一种代币的 LP。这就像上述条件一样，但是由不同的代理人监管合约中缺少的 LP，并且对这些违约的 LP 应用更显著的成本。一个清算者还必须纠正被清算的 LP 的不足代币余额（这将需要给予清算者与违约 LP 剩余代币相等价值的代币）。

另一种解决方案是基于总 LP 的净 ETH 和 USDC 的资金费率。这将是对永续合约中通常使用的资金费率的一种根本不同的应用，其中永续价格与外部现货价格进行比较。可以使用各种函数，但其核心是，随着合约的净 ETH 或 USDC 接近零，应用于不足的 LP 的成本将呈指数增长，从而给 LP 提供添加不足代币的激励。

**杠杆交易者：永续合约**

杠杆 LP 的池子代币是由他的流动性暗示的，并且反映了他的杠杆，以便他的真实或净 ETH 余额是这两个账户的总和。如果我们将他的 vETH 账户不仅仅视为一种债务，而是作为一个可以是负数或正数的一般交易账户，交易者可以以完全相同的方式获得杠杆。清算和会计机制已经就位。

例如，交易员 Bob 可以向合约存入 750 美元的 USDC，生成以下的合约账户概况。

**图 8**

假设 Bob 随后卖出 1.0 个 ETH。假设没有费用或价格影响，并且保证金要求为 20％（即，最大杠杆为 5 倍），这将生成以下账户数据。

**图 9**

或者，交易员 Alice 可以存入价值 375 美元的 ETH

**图 10**

如果她卖空了 1.375 个 ETH，她的账户看起来与图 9 中的 Bob 的账户完全一样。

或者考虑这样一种情况，一个交易者存入了 1 个 ETH 并且做多了 2 个 ETH，如下图 11 所示。他的账户将如下所示：

**图 11**

只需监控交易者的账户市场价值是否超过其所需保证金，而不管他们是做多还是做空。只要交易者不能提取超过其所需保证金的金额，并且存在一种机制和激励措施，让清算者在违反其所需保证金时清算违约账户，那么合约就是安全的。

杠杆交易将允许合约在有限的情况下运作，直到某个 LP 通过存入 USDC 来纠正池子中的 USDC 赤字。也就是说，当合约没有 USDC 时，交易者无法将 ETH 换成 USDC 进行交换，但那些有抵押品的人可以在合约上出售 ETH，从而为他们的 USD 余额产生信用。清算规则或资金费率方法将鼓励现有的 LP 尽快弥补他们的余额，届时交易者可以将他们的 USD 信用提取为 USDC。

### 没有基于 Oracle 的资金费率

通过同时拥有 Uniswap 和永续功能，合约价格将由套利确定，而不是与一个 oracle 相关联的融资费率。这将消除永续协议中的几个问题。用于标准永续融资费率计算的 oracle 可能会被黑客攻击和审查。更重要的是，用于将永续价格与现货价格联系起来的融资费率机制是一个笑话，因为它与传统掉期市场或期货市场中应用的融资费率有着根本的不同。

#### 融资费率闹剧

在主经纪人掉期账户中，融资费率与价格完全独立；这些账户中的资产在现货市场上交易，就像它们不在掉期账户中一样（你无法分辨哪些交易是从掉期账户进行的）。掉期融资费率变化缓慢，就像一般利率一样，是事先已知的，只适用于隔夜头寸。没有理由应用日内融资费率，因为这是一个毫无意义的延伸，因为其幅度太小，无法有意义地激励行为。

在期货市场中，期货价格与现货价格之间的差异称为基差。到期时它会收敛到零，随着期货价格随着时间向现货价格移动，其变化就像融资费率一样。然而，这种基差远远大于永续市场中通常的 0.03%价格溢价。这种较大的基差可以进行真正的套利，因为它涵盖了交易成本并且可以锁定。相反，在永续市场中，交易时的永续溢价几乎没有意义，因为融资费率是根据头寸持续时间内的平均永续溢价来确定的，而不是在交易发起时的价值。

永续价格由谢林点确定，即最明显的目标是现货价格，融资费率只是为了让交易员感觉舒服，而不仅仅是一个谢林点。事实上，与均衡机制存在模糊关系似乎是永续市场用户在协议中只有一个币种时的必要而充分条件，就像 2016 年的 BitMex 一样。然而，当将以太币交易为 USDC 时，这种机制已经过时：让*真正的*套利来确定价格。

永续溢价融资费率机制是不连贯的，并且在交易员因为获利而兴奋时用来欺诈他们。如果市场刚刚上涨，许多以太币持有者正坐拥巨大收益，因此他们不介意为一个月额外支付 5%（也就是每 8 小时仅为 0.018%）。如果你的永续协议的融资费率是基于其永续价格溢价到现货的，那么你的永续协议管理者要么是无知的，要么是邪恶的。

### 稳定币

一个带有永续和 Uniswap 功能的 ETH-USDC 合约自然会产生一个稳定币。考虑一个存入 0.375 个以太币的用户，其中以太币价格为$2000。她的账户价值和所需保证金如下所示：

**图 12**

假设交易员使用杠杆做多了 0.625 个以太币。她的账户价值将如下所示：

**图 13**

由于她持有价值 2000 美元的 ETH，因此她需要将该价值的 20% 存入她的账户以满足保证金要求。

现在考虑一下 Bob，他在合约中存入了 1 个 ETH。他的初始账户价值如下所示：

**图 14**

他还有 400 美元的必需保证金，但由于他的头寸没有杠杆，所以这从未成为问题。这是因为如果 ETH 的价值下跌，他的保证金要求也会下降，反之亦然。

Bob 可以通过提取新的稳定币 vUSD 来将这个头寸变成类似 MakerDao 的 CDP 头寸。这样的硬币在合约内的价值为 USDC，当存入时向用户的 USD 账户增加，当为负数时从 USD 中减去。然而，这种稳定币将有助于节省合约中的 USDC。通过在提取新的 vUSD 稳定币而不是 USDC 时为用户提供更便宜的费用，用户将被激励提取 vUSD 而不是 USDC。只要合约处于健全状态，USDC 与 vUSD 在合约中的最终可互换性将使 vUSD 的价值与 USDC 相等。提取 1250 美元的 vUSD 将使 Bob 的账户看起来像下面的图 15：

**图 15**

Bob 的账户与 Alice 的完全相同，尽管它们是通过不同的交易到达的。一个生成稳定币的 MakerDao CDP 与抵押 ETH 的杠杆多头头寸是相同的。带有交换和永续功能的 LAMM 使稳定币的生成方式就像甜甜圈制造商制作甜甜圈洞一样，这是一种不可避免的互补产品。正如生产甜甜圈洞而不生产甜甜圈是低效的一样，生产稳定币而没有永续合约也是低效的。

这种方法的好处在于它更有效地创建稳定币，因为与 MakerDao 不同，它不依赖于拍卖或预言机。拍卖可能会被操纵，就像 MakerDao 在 2020 年 3 月以零美元出售了价值 800 万美元的 ETH 一样。在 LAMM 中，违约者的净 ETH 头寸很容易在合约上清算。依赖预言机也是有问题的，因为这些可以被黑客攻击或被审查。

从长远来看，人们可以拥有几个独立的合约，每个合约都有自己的稳定币。例如，一个用于 WBTC-USDC 合约的 vUSD2 和一个用于 UNI-USDC 合约的 vUSD3。这些其他稳定币仅由它们各自的 LAMM 合约支持，是独立的。最终，如果其中一个稳定币变得像 USDC 一样受欢迎，并且像 USDC 一样用于与其他合约或产品进行交易，它就可以像 USDC 一样运作。就像创造法定货币或估值新代币一样，使用最终意味着真正的价值，即使没有“真实”资产支持代币。从区块链中消除类似 USDC 的中心化稳定币对于长期安全至关重要。创建高效的去中心化稳定币机制对于实现这一目标至关重要。

### **总结**

+   杠杆 AMM 可以像受限范围一样节省资本

    +   LAMM 自然延伸到提供永续合约和稳定币。

+   目前的永续市场是可审查的并且是受操纵的。

    +   低延迟平台上的永续合约实际上是集中化的。

    +   类似 BitMex 的资金费率均衡机制是一种笑话；它无法平衡永续市场。

        +   资金费率被操纵以使内部人受益。

        +   查看我[之前的帖子](https://efalken.substack.com/p/perp-funding-rate-fraud)以获取解释。

    +   LAMM 生成由真实套利支持的永续合约。

+   现有的稳定币不可持续。

    +   大多数中心化的方案目前还好，但不是长期的解决方案。

    +   去中心化的稳定币具有监管攻击面。

        +   有控制点的可识别个人

        +   像 Chainlink 这样的预言机是可审查的。

    +   治理代币的收入终局较弱。

        +   当代币增长停止时，有动力接受监管。

    +   LAMM 生成稳定币，没有中心化的攻击面。

AMM 中的集中化流动性是一项伟大的创新，但最终是短暂的，因为它是低效的。如果有办法以更多功能性生成相同的杠杆，那么这些办法将被采用。以太坊有许多被高估的代币，能够在链上做空这些代币而不仅仅是卖出将是不错的。能够在链上做空 BTC 或 ETH，或者在链上做 BTC/ETH 的头寸也是不错的。但只有 Uniswap 池功能是不可行的。

空头交易将使以太坊生态系统受益，因为庞氏币是一种系统性威胁，它们普遍存在，并由愚蠢或邪恶的人利用新的加密货币投资者。这些垃圾币玷污了区块链上的一切声誉。当人们可以做空时，内部人员要维持庞氏币的价值就变得困难得多。

收益农业突显了许多流动性头寸是多么低效，因为如果抵押物可以在其他地方使用，那就意味着它没有被有效利用。如果我们忽略交易和信息成本，使用 LP 代币作为其他平台的抵押物是有效的；在实践中，这些成本是显著的。例如，如果您可以用房子的首付作为汽车贷款的抵押物，那么您的汽车贷款人最好要求您少交现金作为抵押。这是因为贷款人专门从事某些资产，并且不擅长监控一个人可以将抵押品应用到的每个资产的价值，然后在这些其他市场上进行交易。汽车卖家希望您再申请一笔额外的房屋净值贷款，并将现金作为汽车贷款的抵押品，这样汽车卖家就可以避免建立监视并可能查封个人房屋的基础设施。

这篇文章对大多数读者来说已经太长了，所以我不会概述这种方法最好的部分，即它如何促进一种消除暂时损失的机制。也许以后再说。
