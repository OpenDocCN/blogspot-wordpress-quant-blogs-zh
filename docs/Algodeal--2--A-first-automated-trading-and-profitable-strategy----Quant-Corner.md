<!--yml

类别：未分类

日期：2024-05-18 08:10:10

-->

# Algodeal (2) A first automated trading and profitable strategy! | Quant Corner

> 来源：[`quantcorner.wordpress.com/2011/06/13/algodeal-2-a-first-automated-trading-and-profitable-strategy/#0001-01-01`](https://quantcorner.wordpress.com/2011/06/13/algodeal-2-a-first-automated-trading-and-profitable-strategy/#0001-01-01)

## 介绍

今天，我们使用由 **Algodeal** 团队开发的 **Java** 中的 **Market Runner** 开发环境编写了第一个自动化交易策略。然后，我们将其发送到 **Algodeal** 服务器上，也就是说，我们将运行我们的策略，以查看其在伪实际条件下的表现如何。

事先，我们做了我们的功课，也就是说，我们进行了市场调研，试图了解股票/指数/期货价格的行为。然后，我们确定了一个交易框架，入场和退出规则。

根据一个人在金融领域的交易经验、金融知识、计量经济学、技术分析、神经网络、支持向量机等方面的知识，可以提出各种各样的自动化交易思想。这是科学和经验（和运气？）的混合。

对于这个第一段代码，这个研究步骤仅限于观察常见的技术分析指标，并了解底层知识。

就**Java**编码而言，我们将参考 **Algodeal** 团队提供的代码示例。我们的代码结构来源于可用的教程。

## 底层和交易规则

我们选择了一个名为*底层*的**农产品期货**。

我们利用了**RSI**（相对强弱指标）技术指标，结合交易日底层价格的下跌（以百分比表示）。

我们确定了**RSI**和价格下跌的某些水平。更确切地说，我们为每个指标确定了两个不同的水平。

我们策略的（伪）伪代码如下：

_____________________

如果 x > RSI > y 并且 a > drop > b

然后购买 1 单位

如果 y > RSI > z 并且 drop > b

然后购买 1 单位

如果持仓为多头则

等待 3 个条形图然后平仓

_____________________

在这里，x < y < z，而 a < b。

人们可以看到这真的很基础，有些*异端*，*a priori*风险很大，因为没有安全保障。请注意，这种策略将需要现金，因为它是*先买后卖*类型。但是，现在还可以！

## Java 代码中的策略

我们遵循在 beta.algodeal.com 上展示的一般代码结构。

我们的代码从基本的指令开始：

```
@Instruments(futures = {Underlying})
@MarketData(start = "yyyy/mm/dd", end = "yyyy/mm/dd")
```

正如在 **Algodeal** 代码示例中所示，我们扩展了 AbstractStrategy 类：

```
public class StrategyName extends AbstractStrategy {}
```

然后，我们定义了所有的变量：

```
double drop;
double smallerDrop = val1;
double higherDrop = val2;   

RSI rsi;
int smallerRSI = val3;
int higherRSI = val4;
int hold = 0;
int barHolding = val5;
```

这样做将很容易通过反复试验改变值以希望获得更好的得分。

然后，我们声明了我们的变量 rsi 并在图上绘制如下：

```
rsi = newIndicator().rsi().withLength(14).on(Bar.TO_LOW).draw(RED, DrawMode.INDEPENDENT).get();
```

*请参考 MarketRunner API 文档了解参数的详细信息*。

最后，我们来到策略的核心。我们所有的条件、循环等都包含在一个 **onClose()** 回调中。

整个代码片段看起来像：

```
package PackageName;

import static com.algodeal.marketData.instruments.Futures.*;
import static java.awt.Color.*;
import com.algodeal.marketData.prices.Bar;
import com.algodeal.marketrunner.indicators.*;
import com.algodeal.marketrunner.recorders.records.IndicatorConfigRecord.DrawMode;
import com.algodeal.marketrunner.strategies.AbstractStrategy;
import com.algodeal.marketrunner.strategies.Instruments;
import com.algodeal.marketrunner.strategies.MarketData;

@Instruments(futures = {Underlying})
@MarketData(start = "yyyy/mm/dd", end = "yyyy/mm/dd")

public class StrategyName extends AbstractStrategy {

    double drop;
    double smallerDrop = val1;
    double higherDrop = val2;   

    RSI rsi;
    int smallerRSI = val3;
    int higherRSI = val4;

    int hold = 0;
    int barHolding = val5;

    @Override
    public void onStrategyStart() {
        rsi = newIndicator().rsi().withLength(14).on(Bar.TO_LOW).draw(RED, DrawMode.INDEPENDENT).get();
    }

    @Override
    public void onClose (Bar bar){

        drop = Math.log(getBars().ago(0).getOpen() - getBars().ago(0).getClose());

        if (rsi.getValue() < smallerRSI) {
            if (drop >= smallerDrop){
                if (drop < higherDrop) {
                    buy(1, "Buy!");
                    }
                }
            }

        if (rsi.getValue() >= smallerRSI ) {
            if (rsi.getValue() <= higherRSI){
                if (drop >= higherDrop) {
                    buy(1, "Buy!");
                    }
                }
            }

        if (getPosition().isLong()){
            if (hold < barHolding){
                hold++;
            }else{
                closePosition("Close out!");
            }
        }
    }
}
```

## 运行策略

*最后但并非最不重要*，我们通过向**Algodeal**服务器网格发送我们的代码来在“真实”条件下运行我们的策略。在很短的时间内，我们就会收到一系列我们交易策略的表现指标。

我们策略的整体表现：

![](https://quantcorner.wordpress.com/wp-content/uploads/2011/06/equitychartsoybean.png)

![](https://quantcorner.wordpress.com/wp-content/uploads/2011/06/barchartsoybean1.png)

好吧，这离完美还有很远，这种策略有很多注意事项，因为它过于简化了。但是，你能相信吗？这是有利可图的！这应该能说服一个人，值得花时间做市场调研，定义自动交易策略，并使用**Algodeal**进行编码。

有一次，一位作者写道，*知识无处不在，等待被表达*。现在，把这种说法推断为*财富无处不在，等待被编码* 是很诱人的 🙂。
