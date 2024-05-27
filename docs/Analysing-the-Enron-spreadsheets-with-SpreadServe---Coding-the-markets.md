<!--yml

分类：未分类

日期：2024 年 5 月 12 日 19:29:52

-->

# 使用 SpreadServe 分析 Enron 电子表格 | 编码市场

> 来源：[`etrading.wordpress.com/2017/03/13/analysing-the-enron-spreadsheets-with-spreadserve/#0001-01-01`](https://etrading.wordpress.com/2017/03/13/analysing-the-enron-spreadsheets-with-spreadserve/#0001-01-01)

## 使用 SpreadServe 分析 Enron 电子表格

### 2017 年 3 月 13 日

最近，我一直在使用 Enron 电子表格来测试[SpreadServe](http://spreadserve.com)，因为向高容量、多样化的输入暴露任何代码库都是良好的测试实践。[Felienne](http://www.felienne.com)在[figshare](https://figshare.com/articles/Enron_Spreadsheets_and_Emails/1221767)上提供了这些电子表格，但它们采用了一种稍微晦涩的 zip 格式，所以我[将它们发布到了 github](https://github.com/SpreadServe/ssxls/tree/master/enron)上以便更容易获取。SpreadServe 将每张表中使用的公式信息发布到了 spreadserve.com DB，所以我对 Enron 的公式使用进行了简单的分析。结果在[这里的 github](https://github.com/SpreadServe/ssxls/blob/master/enron_report.md)上。简而言之：共有 15927 张表，只有 8421 张使用了公式。在所有表中使用了 152 种不同的函数，只有 170 张表使用了超出算术以外的数学函数。所以 Enron 电子表格并不像我想象的那样多样化。但它们确实是一个很好的容量测试。下面是一段关于使用 SpreadServe 探索 Enron 电子表格的短视频...

[`www.youtube.com/embed/ob9_b7VzpAQ?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=en&autohide=2&start=13&wmode=transparent`](https://www.youtube.com/embed/ob9_b7VzpAQ?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=en&autohide=2&start=13&wmode=transparent)

视频
