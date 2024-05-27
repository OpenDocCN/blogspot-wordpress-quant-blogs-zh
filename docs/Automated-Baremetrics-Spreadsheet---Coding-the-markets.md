<!--yml

类别：未分类

日期：2024-05-12 19:29:37

-->

# 自动化的 Baremetrics 电子表格 | 编码市场

> 来源：[`etrading.wordpress.com/2017/06/05/automated-baremetrics-spreadsheet/#0001-01-01`](https://etrading.wordpress.com/2017/06/05/automated-baremetrics-spreadsheet/#0001-01-01)

## 自动化的 Baremetrics 电子表格

### 2017 年 6 月 5 日

回到四月份，我阅读了[一篇很棒的文章](https://blog.baremetrics.com/saas-financial-model-d2628505bd62) ，作者是 [Jaakko Piipponen](https://blog.baremetrics.com/@jaakkopiipponen) ，关于他建立的 SaaS 财务模型作为 Excel 电子表格。我对电子表格财务模型很感兴趣，所以我很喜欢 Jaakko 对他的模型如何覆盖损益报告、运营费用、工资和收入的介绍。Jaakko 描述了您每月只需花费 30 分钟从 Baremetrics 仪表板下载报告并粘贴到 Excel 中即可保持其更新的过程。这篇文章的标题是“您实际上会更新的 SaaS 财务模型”，因为模型的价值是每月手动操作 30 分钟已经完全合理了。我是第一个主张将 Excel 用于业务敏捷性的人；它是一个极好的工具，使销售、市场营销和财务人员能够自行解决问题，而不需要软件开发团队的瓶颈。但是 Excel 的缺点是像 Jaakko 所说的下载和粘贴这样的手动操作。如果 Baremetrics 数据在电子表格中自动下载和更新会不会很棒呢？然后该模型将始终保持最新状态，并且不需要繁琐且容易出错的下载和粘贴操作。

因此，我通过将 Baremetrics 函数添加到我的 [开源 XLL Excel Addin SSAddin](https://github.com/SpreadServe/SSAddin) 中来构建它。这是一个将 Jaako 的模型简化为模型的收入部分的电子表格...

[`github.com/SpreadServe/SSAddin/blob/master/xls/flight_bare_model2.xls`](https://github.com/SpreadServe/SSAddin/blob/master/xls/flight_bare_model2.xls)

它使用 SSAddin 函数每 10 分钟自动下载收入数据到 MRR Export 表中，通过 [Show Summary API](https://developers.baremetrics.com/reference#show-summary)，因此每 10 分钟 Revenue Model 表将更新为最新的新客户、订阅、取消、升级和降级。您只需要从这里下载 SSAddin 32 或 64 位 .xll 二进制文件...

[`spreadserve.com/s3/downloads.html`](http://spreadserve.com/s3/downloads.html)

然后在 Excel 中安装插件并启动电子表格。不要忘记确保自动计算已打开，并且您已从下载页面获取了 SSAddin.xll.config 的副本并将其放在您的 PC 上与 SSAddin.xll 旁边。您需要编辑 .config 文件以添加您的 Baremetrics 许可密钥。

您可以在这里查看 flight_bare_model2.xls 在线运行并由 spreadserve.com 数据驱动...

[`sscalc0.online/flight_bare_model2.xls/0`](http://sscalc0.online/flight_bare_model2.xls/0)

[`sscalc0.online/flight_bare_model2.xls/MRR%20Export`](http://sscalc0.online/flight_bare_model2.xls/MRR%20Export)

这个在线电子表格将自动化提升到了最高级别。当你在桌面或笔记本电脑上运行用 SSAddin 自动化的电子表格模型时，你仍然需要启动 Excel，加载电子表格，并按 F9 键才能开始自动更新。通过 SpreadServe 托管，你可以将电子表格移至云服务器上。所有手动操作都被消除，每个人在他们的浏览器中都能看到相同的自动更新数字。
