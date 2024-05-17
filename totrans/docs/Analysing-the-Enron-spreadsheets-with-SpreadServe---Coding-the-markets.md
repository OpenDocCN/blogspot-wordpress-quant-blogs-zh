<!--yml
category: 未分类
date: 2024-05-12 19:29:52
-->

# Analysing the Enron spreadsheets with SpreadServe | Coding the markets

> 来源：[https://etrading.wordpress.com/2017/03/13/analysing-the-enron-spreadsheets-with-spreadserve/#0001-01-01](https://etrading.wordpress.com/2017/03/13/analysing-the-enron-spreadsheets-with-spreadserve/#0001-01-01)

## Analysing the Enron spreadsheets with SpreadServe

### March 13, 2017

Recently I’ve been using the Enron spreadsheets to test [SpreadServe](http://spreadserve.com), simply because it’s good testing practice to expose any codebase to a high volume of diverse inputs. [Felienne](http://www.felienne.com) made them available on [figshare](https://figshare.com/articles/Enron_Spreadsheets_and_Emails/1221767), but they’re in a slightly obscure zip format, so I [posted them on github](https://github.com/SpreadServe/ssxls/tree/master/enron) to make them more accessible. SpreadServe posts information about the formulae used in each sheet into the spreadserve.com DB, so I did a simple analysis of Enron formula use. The results are on [github here](https://github.com/SpreadServe/ssxls/blob/master/enron_report.md). To summarise: there are 15927 sheets, and only 8421 use formulae. 152 different functions are used across all sheets, and only 170 sheets use maths funcs that go beyond arithmetic. So the Enron spreadsheets weren’t as diverse as I’d hoped. They made for a good volume test though. Here’s a short video about exploring the Enron spreadsheets with SpreadServe…

 [https://www.youtube.com/embed/ob9_b7VzpAQ?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=en&autohide=2&start=13&wmode=transparent](https://www.youtube.com/embed/ob9_b7VzpAQ?version=3&rel=1&showsearch=0&showinfo=1&iv_load_policy=1&fs=1&hl=en&autohide=2&start=13&wmode=transparent)

VIDEO