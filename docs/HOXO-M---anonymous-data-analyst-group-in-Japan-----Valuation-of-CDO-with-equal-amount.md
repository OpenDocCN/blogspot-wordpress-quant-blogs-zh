<!--yml

分类： 未分类

日期：2024-05-18 06:49:10

-->

# HOXO-M - 匿名数据分析小组 - ：等量 CDO 估值

> 来源：[`mockquant.blogspot.com/2011/01/valuation-of-cdo-with-equal-amount.html#0001-01-01`](http://mockquant.blogspot.com/2011/01/valuation-of-cdo-with-equal-amount.html#0001-01-01)

日本银行(BOJ)发表研究论文

定期发布。他们最近发表了一篇有关 CDO 估值的非常有趣的论文。他们引入了用于定价 CDO 的 copula，并讨论了使用不同 copula 进行定价时不同的 CDO 利差。

我想重现他们的结果（尤其是，P23-Table7）

计算条件如下

+   债务数量（NUM.REFDEBT）:=100

+   成熟期（MATURITY）:=5 年

+   恢复率（RECOVERY.RATE）:=40%（固定值）

+   违约概率 (DEFAULT.PROBABILITY):=5％（在 5 年内）

+   正态 Copula 的参数 ρ:=0.15

+   克莱顿 copula 的参数 α:=0.21

他们为了简化计算，近似了他们的估值公式（方程式（27））

（他们假设 CDO 的利差是按折现债券支付的。）

我用他们的方法模拟了 CDO 的价值。

结果如下

| copula/tranche | Equity | mezzanine | senior | super senior |
| --- | --- | --- | --- | --- |
| 正态 | 1,145.42 | 62.49 | 0.52 | 0.000 |
| t(20) | 1,055.28 | 86.07 | 2.18 | 0.004 |
| t(6) | 896.74 | 126.44 | 8.56 | 0.044 |
| t(3) | 733.31 | 165.90 | 23.56 | 0.191 |
| 克莱顿 | 857.64 | 135.73 | 12.83 | 0.084 |

这个表格复制了他们的结果(P23-Table7)。

而且，在 senior 或 super senior 中，你可以理解使用正态 copula 评估的 CDO 利差要低于其他类型。这意味着在金融危机中，正态 copula 是不适当的。

我展示我的编程代码（使用 R 语言）。

如果你复制并运行我的源代码，你可以轻松复制我的结果。

在你运行之前，请先安装"copula"包。

<fieldset>

```

```

[库](http://inside-r.org/r-doc/base/library)(copula)

#CDO 利差计算函数

SpreadOfCDO <- function(copula, default.probability, maturity,

恢复率，附着，分离，路径数，参考债务数）

{

随机 copula <- rcopula(copula,num.path)

num.default <- rowSums(random.copula < default.probability)

亏损参考债务 <- (1-恢复率)/num.refdebt*num.default

亏损类别 <- (pmax(亏损参考债务 - 附着,0)-pmax(亏损参考债务 - 分离,0))/(分离-附着)

预期损失类别 <- sum(亏损类别)/num.path

利差 <- -1/成熟度*log(1-预期损失类别)

return(spread)

}

################  主要  ##################

#参数

NUM.PATH <- 10³

NUM.REFDEBT <- 100

DEFAULT.PROBABILITY <- 0.05

MATURITY <- 5

RECOVERY.RATE <- 0.4

#我想要比较的 copula。

COPULA <- list(normalCopula(0.15, dim = NUM.REFDEBT),

tCopula(0.15, dim = NUM.REFDEBT, df = 20),

tCopula(0.15, dim = NUM.REFDEBT, df = 6),

tCopula(0.15, dim = NUM.REFDEBT, df = 3),

claytonCopula(0.21, dim = NUM.REFDEBT)

)

#用于简化编程的定义

SpreadOfCDOWithFixedParameter <- function(copula,attachment, detachment){

SpreadOfCDO(copula, DEFAULT.PROBABILITY, MATURITY,

    RECOVERY.RATE, attachment, detachment, NUM.PATH, NUM.REFDEBT)

}

result <- list()

#tranche:equity

result[[1]] <- sapply(COPULA,SpreadOfCDOWithFixedParameter,0.0,0.06)

#tranche:mezzanine

result[[2]] <- sapply(COPULA,SpreadOfCDOWithFixedParameter,0.06,0.18)

#tranche:senior

result[[3]] <- sapply(COPULA,SpreadOfCDOWithFixedParameter,0.18,0.36)

#tranche:super senior

result[[4]] <- sapply(COPULA,SpreadOfCDOWithFixedParameter,0.36,1)

#convert to matrix, and chenge unit to "bp"

result <- 10⁴*do.call("cbind", result)

colnames(result) <- c("equity","mezzanine","senior","super senior")

rownames(result) <- c("normal","t(20)","t(6)","t(3)","clayton")

result

```

```

[由内部-R.org 上漂亮的 R 创建](http://www.inside-r.org/pretty-r "由内部-R.org 上漂亮的 R 创建")</fieldset>
