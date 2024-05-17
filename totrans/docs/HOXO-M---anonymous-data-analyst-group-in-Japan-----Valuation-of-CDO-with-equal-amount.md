<!--yml
category: 未分类
date: 2024-05-18 06:49:10
-->

# HOXO-M - anonymous data analyst group in Japan - : Valuation of CDO with equal amount

> 来源：[http://mockquant.blogspot.com/2011/01/valuation-of-cdo-with-equal-amount.html#0001-01-01](http://mockquant.blogspot.com/2011/01/valuation-of-cdo-with-equal-amount.html#0001-01-01)

Bank of Japan(BOJ) publish research paper 

regularly. And, they issued very interesting paper about valuation of CDO recently. They introduced copula for pricing of CDO,and discussed how different CDO spreads were with using different copula for pricing.

I would like to reproduce their result (especially,P23-Table7)

The condition of calculation is following that

*   number of debt（NUM.REFDEBT）:=100
*   maturity(MATURITY):=5 year
*   recovery rate(RECOVERY.RATE):=40%（constant value）
*   probability of default (DEFAULT.PROBABILITY):=5％（in 5 years）
*   parameter of nomal copula ρ:=0.15
*   parameter of clayton copula α:=0.21

They apporoximated their valuation formula for easy calculation(equation (27))

(They assumed that CDO spread were paid as discounted bond at the begging.)

I simulated valuation of CDO with their method.

The result is following that

| copula/tranche | Equity | mezzanine | senior | super senior |
| normal | 1,145.42 | 62.49 | 0.52 | 0.000 |
| t(20) | 1,055.28 | 86.07 | 2.18 | 0.004 |
| t(6) | 896.74 | 126.44 | 8.56 | 0.044 |
| t(3) | 733.31 | 165.90 | 23.56 | 0.191 |
| clayton | 857.64 | 135.73 | 12.83 | 0.084 |

This table reproduce their result(P23-Table7).

And, In senior or super senior,you can understand that the CDO spread which is evaluated by normal copula is lower than the others. It means that normal copula is inadequate in financial crisis.

I show you my programming code（by R language).
If you copy and run my source code, you can duplicate my result easily.
Before you run, please install "copula"package.

<fieldset>

```

```
[library](http://inside-r.org/r-doc/base/library)(copula)
#function for CDO spread calculation 
SpreadOfCDO <- function(copula, default.probability, maturity,
  recovery.rate, attachment, detachment, num.path, num.refdebt)
{
  random.copula <- rcopula(copula,num.path)
  num.default <- rowSums(random.copula < default.probability)
  loss.refdebt <- (1-recovery.rate)/num.refdebt*num.default
  loss.tranche <- (pmax(loss.refdebt - attachment,0)-pmax(loss.refdebt - detachment,0))/(detachment-attachment)
  expectation.loss.tranche <- sum(loss.tranche)/num.path
  spread <- -1/maturity*log(1-expectation.loss.tranche)
  return(spread)
}
################  main  ##################
#parameter
NUM.PATH <- 10^3
NUM.REFDEBT <- 100
DEFAULT.PROBABILITY <- 0.05
MATURITY <- 5
RECOVERY.RATE <- 0.4
#copulas which I want to compare.
COPULA <- list(normalCopula(0.15, dim = NUM.REFDEBT),
  tCopula(0.15, dim = NUM.REFDEBT, df = 20),
  tCopula(0.15, dim = NUM.REFDEBT, df = 6),
  tCopula(0.15, dim = NUM.REFDEBT, df = 3),
  claytonCopula(0.21, dim = NUM.REFDEBT)
)
#define for easy programming
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
result <- 10^4*do.call("cbind", result) 
colnames(result) <- c("equity","mezzanine","senior","super senior")
rownames(result) <- c("normal","t(20)","t(6)","t(3)","clayton")
result
```

```

[Created by Pretty R at inside-R.org](http://www.inside-r.org/pretty-r "Created by Pretty R at inside-R.org")</fieldset>