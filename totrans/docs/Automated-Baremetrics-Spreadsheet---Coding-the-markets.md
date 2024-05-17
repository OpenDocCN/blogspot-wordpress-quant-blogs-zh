<!--yml
category: 未分类
date: 2024-05-12 19:29:37
-->

# Automated Baremetrics Spreadsheet | Coding the markets

> 来源：[https://etrading.wordpress.com/2017/06/05/automated-baremetrics-spreadsheet/#0001-01-01](https://etrading.wordpress.com/2017/06/05/automated-baremetrics-spreadsheet/#0001-01-01)

## Automated Baremetrics Spreadsheet

### June 5, 2017

Back in April I read a [great post](https://blog.baremetrics.com/saas-financial-model-d2628505bd62) by [Jaakko Piipponen](https://blog.baremetrics.com/@jaakkopiipponen) on the SaaS financial model he’d built as an Excel spreadsheet. I’m interested in spreadsheet financial models, so I enjoyed Jaakko’s run down on how his model covers PnL report, operating expenses, payroll and revenue. Jaakko describes how you only need to spend 30 mins a month downloading reports from the Baremetrics dashboard and pasting it into Excel to keep it up to date. The post is titled an “SaaS financial model you’ll actually update”, because the value of the model is such that 30 mins of manual handle turning a month is more than justified. Now I’m the first to advocate Excel for business agility; it’s a great tool that enables sales, marketing and finance people to solve problems for themselves without the bottleneck of a software development team. But the downside of Excel is manual operation like the download and paste Jaakko spells out. Wouldn’t it be great if the Baremetrics data in the spreadsheet downloaded and updated automatically? Then the model would always be up to date, and no tedious and error prone download’n’paste operations are necessary.

So I built it by adding Baremetrics functions to my [open source XLL Excel Addin SSAddin](https://github.com/SpreadServe/SSAddin). Here’s a spreadsheet that strips Jaako’s model down to just the revenue parts of the model…

[https://github.com/SpreadServe/SSAddin/blob/master/xls/flight_bare_model2.xls](https://github.com/SpreadServe/SSAddin/blob/master/xls/flight_bare_model2.xls)

It uses SSAddin functions to automatically download the revenue numbers every 10 minutes into the MRR Export sheet via the [Show Summary API](https://developers.baremetrics.com/reference#show-summary) so the Revenue Model sheet will update every 10 minutes with the latest new customers, subscriptions, cancellations, upgrades and downgrades. All you need to do is download SSAddin 32 or 64 bit .xll binaries from here…

[http://spreadserve.com/s3/downloads.html](http://spreadserve.com/s3/downloads.html)

Then install the addin in Excel and fire up the spreadsheet. Don’t forget to ensure that auto calc is on, and that you’ve got a copy of SSAddin.xll.config from the download page and put it next to SSAddin.xll on your PC. You’ll need to edit the .config to add your Baremetrics license key.

You can see flight_bare_model2.xls running online and driven by spreadserve.com data here…

[http://sscalc0.online/flight_bare_model2.xls/0](http://sscalc0.online/flight_bare_model2.xls/0)

[http://sscalc0.online/flight_bare_model2.xls/MRR%20Export](http://sscalc0.online/flight_bare_model2.xls/MRR%20Export)

This online spreadsheet takes automation to the ultimate level. When you run a spreadsheet model automated with SSAddin on your desktop or laptop you still have to start Excel, load the spreadsheet and hit F9 before auto updates can start. With SpreadServe hosting, you can move the spreadsheet onto a cloud server. All manual operations are eliminated, and everyone sees the same auto updating numbers in their browsers.