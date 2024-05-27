<!--yml

分类：未分类

日期：2024-05-18 14:03:56

-->

# SVM 使用不同长度的 RSI 进行分类 – 量子金融家

> 来源：[`quantumfinancier.wordpress.com/2010/06/10/svm-classification-using-rsi-from-various-lengths/#0001-01-01`](https://quantumfinancier.wordpress.com/2010/06/10/svm-classification-using-rsi-from-various-lengths/#0001-01-01)

首先，我想为最近博客上缺少帖子道歉。我一直忙于工作（现在仍然如此），并且很难抽出时间写完整的帖子。

今天，我想跟进一下[关于 SVM 学习的上一篇文章](https://quantumfinancier.wordpress.com/2010/05/21/application-of-svms/)。在这篇文章中，我做了我文章中提到的所有事情；系统中的唯一输入是与它们各自结果（上涨与下跌）相关的 2 至 30 天的 RSI 值。SVM 算法来自 R 包 kernlab，SVM 本身的参数是 nu = 0.2，C = 10\。这些是随意选择的，绝对没有进行优化，想法只是提供一个例子。此外，我绝不建议这是最佳设置或任何此类事情，我认为这是一个很好的例子，因为之前在博客上已经讨论过了。无论如何，以下是相对于经典 MR+RSI2 50/50 作为代理和持有策略的权益曲线和一些数字。

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/06/svm-rsis1.png)

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/06/svm-rsis-results.png)

只是大体上看图表，我们就能看出 SVM 策略在趋势存在时适应得更好，并且在牛市中表现优于 RSI2，它也相当适应最近的动荡，表现略逊于短期 MR 策略。我计划分享一些代码，但不想让博客充斥着一行行的代码，所以一旦我想出最好的方法（我正在考虑一个可下载的文件或其他类似的方式），我将进行分享。最后，如果读者对 SVM 有所尝试，我像往常一样欢迎建议和评论！

QF
