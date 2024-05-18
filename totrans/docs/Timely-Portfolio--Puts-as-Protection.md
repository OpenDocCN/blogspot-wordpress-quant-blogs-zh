<!--yml
category: 未分类
date: 2024-05-18 14:49:29
-->

# Timely Portfolio: Puts as Protection

> 来源：[http://timelyportfolio.blogspot.com/2017/03/puts-as-protection.html#0001-01-01](http://timelyportfolio.blogspot.com/2017/03/puts-as-protection.html#0001-01-01)

Many asset management firms are happily enjoying record revenue and profits driven not by inorganic growth or skillful portfolio management but by a seemingly endless increase in US equity prices. These firms are effectively commodity producers entirely dependent on the price of an index over which the firm has no control. The options market presents an easy, cheap, and liquid form of protection in the form of puts with which the firm could hedge its revenues, its clients, or both. However, many of these firms in blissful disregard for the brutality of asymmetric arithmetic choose to ignore this opportunity for protection.

Here is some very quick and ugly code with which anyone can evaluate various put options for the hedge and their potential outcomes. I hope someone, somewhere might benefit from the idea

### Load Our Helpful Packages

```
library(quantmod)
library(purrr)
library(dplyr)
library(pipeR)
library(tibble)
```

### Use quantmod To Gather Data

```
getSymbols("SPY")
```

```
## [1] "SPY"
```

```
spy_opts <- getOptionChain("SPY", Exp = "2017-12-15")
```

### Construct Simple Hedged Portfolio

```
outcomes <- spy_opts$puts %>%
  tbl_df() %>%
  filter(Strike >= 230, Strike <= 260, Ask > 0) %>%
  mutate(
    spy_pos = floor(100*tail(SPY,1)[[4]]-100*Ask),
    option_pos = ceiling(100*Ask)
  ) %>%
  select(Strike, spy_pos, option_pos)

portfolio <- map(
  seq_len(nrow(outcomes)),
  ~.x %>>%
    {outcomes[.,]} %>>%
    (strike~{
      map(
        seq(-50,50,5),
        ~tibble(
          outcome = .x,
          value = strike$spy_pos * (1+.x/100) + 
                  max(c(strike$Strike - tail(SPY)[[4]] * (1+.x/100),0)) * 100
        )
      ) %>>%
        bind_rows()
    })
)

strike_port <- tibble(
  strike = outcomes$Strike,
  outcomes = map(portfolio, ~.x)
)
```

### Plot Outcomes in $

```
plot(
  value ~ outcome,
  data = strike_port[1,]$outcomes[[1]],
  ylim = c(0,40000),
  type = "l"
)
walk(
  seq_len(nrow(strike_port)),
  ~lines(value ~ outcome, data = strike_port[.x,]$outcomes[[1]])
)
```

![](img/d76689678962c8186ccad09f75853d1a.png)

### Make Outcomes Interactive in Plotly

```
library(plotly)

pltly <- reduce(
  1:nrow(strike_port),
  function(left, right) {
    left %>%
      add_lines(
        x = strike_port[right,]$outcomes[[1]]$outcome,
        y = strike_port[right,]$outcomes[[1]]$value/(100*tail(SPY,1)[[4]]) - 1,
        inherit = FALSE,
        name = strike_port[right,]$strike
      )
  }, 
  .init = plot_ly()
)
```

[Live Plotly Example](https://bl.ocks.org/timelyportfolio/raw/153eb2a6f42a74196985771fd4192b0b/)