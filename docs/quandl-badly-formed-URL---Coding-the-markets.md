<!--yml

类别：未分类

日期：2024-05-12 19:31:54

-->

# quandl 格式错误的 URL | 编码市场

> 来源：[`etrading.wordpress.com/2015/04/20/quandl-badly-formed-url/#0001-01-01`](https://etrading.wordpress.com/2015/04/20/quandl-badly-formed-url/#0001-01-01)

## quandl 格式错误的 URL

### 2015 年 4 月 20 日

我已经开始编写一些新代码，从 [quandl](http://quandl.com) 获取数据，并且我遇到了这个错误…

```
 { "error":"Unknown api route."}
```

我正在使用 quandl 自己的[API 页面](https://www.quandl.com/tools/api)中的第一个示例…

```
https://www.quandl.com/api/v1/WIKI/AAPL.csv
```

我尝试在谷歌上搜索，但没有找到任何答案。幸运的是，quandl 团队在 Twitter 上做出了回应，一切都好了。URL 应该是…

```
https://www.quandl.com/api/v1/datasets/WIKI/AAPL.csv
```

所以我在这里记录下这个问题，以便其他遇到相同问题的人参考。看起来“未知 API 路由”等于“格式错误的 URL”。
