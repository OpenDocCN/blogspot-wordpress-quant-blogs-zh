<!--yml

类别：未分类

日期：2024 年 05 月 18 日 下午 3:28:52

-->

# 观察数据中的因果关系 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2014/12/26/causality-in-observational-data/#0001-01-01`](https://tr8dr.wordpress.com/2014/12/26/causality-in-observational-data/#0001-01-01)

2014 年 12 月 26 日 上午 10:37

过去曾经创建[集群](https://tr8dr.wordpress.com/2010/01/22/cointegration-clusters/ "协整集群")以帮助识别资产之间的关系。结果图对于识别用于均值回归组合的资产非常有用。该方法的难点始终在于准确衡量资产对之间的关系强度。我曾经研究过 Granger 因果关系，但它相当受限，因为预计资产关系将遵循 VECM 类似的模型，并最终选择在一些技术中进行加权以作为近似。

确定更一般关系的因果关系需要非常不同的方法，其中 Y ← f(X) + ε。即 f(x) 可能是 X 上的（未知的）非线性函数。我遇到了一篇有趣的论文：“使用观察数据区分因果关系：方法和基准”（[链接](http://arxiv.org/pdf/1412.3773v1.pdf)），它建立在查看 p(Y|X) 与 p(X|Y) 的“复杂性”的不对称性的工作基础上，如果 Y ← X（X 引起 Y），则 p(Y|X) 的复杂性倾向于低于 p(X|Y)。

文章提供了两种方法的结果：加性噪声方法（ANM）和信息几何因果推断（IGCI），其中 ANM 在各种情况下通常比 IGCI 更好。

ANM 的 Python 伪代码算法（摘自该论文）：

```
def causality(xy: DataFrame, complexity: FunctionType, complexity_threshold: float):
    n = nrows(xy)
    xy = normalize (xy)
    training = sample(xy, n/2)
    testing = sample(xy, n/2)

    ## regress Y <- X and X <- Y on training set
    thetaY = GaussianProcess.regress (training.y, training.x)
    thetaX = GaussianProcess.regress (training.x, training.y)

    ## predict Y' <- X' and X' <- Y' & compute residuals on testing set
    eY = testing.y - GaussianProcess.predict (testing.x, thetaY)
    eX = testing.x - GaussianProcess.predict (testing.y, thetaX)

    ## determine complexity of each proposition on variable and residuals
    Cxy = complexity (testing.x, eY)
    Cyx = complexity (testing.y, eX)

    ## determine whether Y <- X, X -> Y, or indeterminate
    if (Cyx - Cxy) > complexity_threshold:
        return X_causes_Y
    elif: (Cxy - Cyx) > complexity_threshold:
        return Y_causes_X
    else:
        return None

```

文章建议使用 Hilbert-Schmidt 独立准则（HSIC）的评分作为复杂性测试。我将编写上述代码，并查看其在广泛资产组合上的表现。 文章确实测试了 CEP 基准，其中包含一些已知的金融关系。

### 附录

现在正忙于另一项调查，但将以适当的实施方式重新访问这个问题。
