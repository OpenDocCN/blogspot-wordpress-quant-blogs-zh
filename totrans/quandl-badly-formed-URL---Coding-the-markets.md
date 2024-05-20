<!--yml
category: 未分类
date: 2024-05-12 19:31:54
-->

# quandl badly formed URL | Coding the markets

> 来源：[https://etrading.wordpress.com/2015/04/20/quandl-badly-formed-url/#0001-01-01](https://etrading.wordpress.com/2015/04/20/quandl-badly-formed-url/#0001-01-01)

## quandl badly formed URL

### April 20, 2015

I’ve started working on some new code that pulls data from [quandl](http://quandl.com), and I was getting this error…

```
 { "error":"Unknown api route."}
```

I was using the first example from quandl’s own [API page](https://www.quandl.com/tools/api)…

```
https://www.quandl.com/api/v1/WIKI/AAPL.csv
```

and googling didn’t turn up any answers. Fortunately the quandl folk responded on Twitter, and all’s well. The URL should be…

```
https://www.quandl.com/api/v1/datasets/WIKI/AAPL.csv
```

So I’m recording the issue here for any others that get stuck. Looks like “unknown api route”==”badly formed url”.