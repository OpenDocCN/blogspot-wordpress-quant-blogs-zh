<!--yml
category: 未分类
date: 2024-05-12 20:39:59
-->

# Falkenblog: How to Spot Overfitting

> 来源：[http://falkenblog.blogspot.com/2011/11/how-to-spot-overfitting.html#0001-01-01](http://falkenblog.blogspot.com/2011/11/how-to-spot-overfitting.html#0001-01-01)

FRBSF Economic Letter: Probability of a Recession vs. Actual Recession Dates

[![](img/1045985cc4ac17e954264b315862ac7d.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEidnz7wIKw7fYK7JnQK05T8ql_7DIr-QFF_FTdJe6DSG2zUVoDl35fJz8CcSdoxgA-96s_PA3a17gWi6CQi2kmiJLGzt0KppJsFnzkhhkAK_9J8Z6Ma5O-ec38Iep7I7LXhyphenhyphenDC63A/s1600/fedfcst.png)

You can teach statistics, but unfortunately, you can't teach people not to overfit data. The problem is that it is too tempting to look at some data, keep applying different inputs and functional forms, until you fit the data. In some sense, that's what a good model does, so the objective, maximizing the R2, is encouraged.

But there's no point fooling yourself, it just wastes time, and only the researcher really knows if they overfit the problem, because outsiders don't know how the ultimate functional form was chosen (iterating over a large set of inputs?). Macro forecasting is especially difficult, and anyone familiar with its history would do well to be modest (see

[here](http://www.richmondfed.org/publications/research/economic_quarterly/2003/summer/pdf/stockwatsonsummer03.pdf)

). The above graph

[from some San Francisco Fed researchers](http://www.frbsf.org/publications/economics/letter/2011/el2011-35.html)

is clearly overfit because the base recession rate is about 16% since 1945, so the average forecast should be around 16%, not jumping from 0 to 100%. A forecast should cluster around the unconditional expectation, not the extremes. Only with hindsight do these kind of forecasts make sense.