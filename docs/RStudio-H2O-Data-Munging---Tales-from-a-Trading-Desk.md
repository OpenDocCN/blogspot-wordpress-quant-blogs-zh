<!--yml

分类：未分类

日期：2024 年 05 月 18 日 05:34:54

-->

# RStudio H2O 数据处理 | 交易台的故事

> 来源：[`mdavey.wordpress.com/2016/04/04/rstudio-h2o-data-munging/#0001-01-01`](https://mdavey.wordpress.com/2016/04/04/rstudio-h2o-data-munging/#0001-01-01)

以下可能对 [RStudio](https://www.rstudio.com/) 的 H2O 专家来说已经非常熟悉，但对于不熟悉 [H2O](http://www.h2o.ai/) 的任何人来说，这可能会有所帮助。

一些开始的上下文：我有各种数据集，并希望开始尝试各种 H2O 算法，理想情况下通过预测从数据中获得见解，以及数据是如何聚类的。初始数据集并不大，但我怀疑会阻碍诸如深度学习之类的算法。

当通过 `h2o.uploadFile` 加载带标题的 CSV 文件时，请确保每个列标题是唯一的🙂 显而易见，但有时并不是🙂

```
data.hex &lt;- h2o.uploadFile(path = "/Users/Matt/Downloads/sampledata.csv",header = TRUE, sep = ",", destination_frame = "data.hex")

```

列名和摘要有时很有用：

```
colnames(data.hex)
summary(data.hex)

```

RStudio [技巧](https://twitter.com/rstudiotips) 可能很有用。

柱状图可以通过以下方式轻松显示一列：

```
h2o.hist(data.hex$"&lt;column name&gt;")

```

使用 `help` 获取 H2O 算法的帮助页面：

```
help(h2o.kmeans)

```

[交叉验证](http://stats.stackexchange.com/) 是一个问题和答案网站，专门为对统计学、机器学习、数据分析、数据挖掘和数据可视化感兴趣的人士设计 - 我发现有几次对问题的答案很有用。

R H2O [教程](http://h2o-release.s3.amazonaws.com/h2o/rel-lambert/5/docs-website/Ruser/rtutorial.html) 很有帮助，但缺少更多关于理解算法输出的细节。例如，拿 `prostate.csv` 的示例代码来说。一旦将广义线性模型应用于数据集，对输出的更多信息以及 `summary()` 输出将有助于初学者。我怀疑这是某本书或其他阅读材料解决这个知识缺口的地方。

为 3.8.06 H2O 重新编写前列腺代码，得到以下结果：

```
prostate.hex &lt;- h2o.importFile(path= "https://raw.github.com/0xdata/h2o/master/smalldata/logreg/prostate.csv")
data.split &lt;- h2o.splitFrame(data = prostate.hex, ratios = 0.8)
prostate.train &lt;- data.split[[1]]
prostate.test &lt;- data.split[[2]]
prostate.glm &lt;- h2o.glm(y = "CAPSULE", x = c("AGE","RACE","PSA","DCAPS"), training_frame = prostate.train, validation_frame = prostate.test,family = "binomial", nfolds = 10, alpha = 0.5)
prostate.fit &lt;- h2o.predict(object = prostate.glm, newdata = prostate.hex)
summary(prostate.fit)

```

提供了以下 `summary()` 的输出格式：

```
predict p0 p1
Min. :0.0000 Min. :0.001468 Min. :0.1590
1st Qu.:0.0000 1st Qu.:0.538552 1st Qu.:0.2911
Median :1.0000 Median :0.663140 Median :0.3369
Mean :0.5737 Mean :0.588795 Mean :0.4112
3rd Qu.:1.0000 3rd Qu.:0.708884 3rd Qu.:0.4614
Max. :1.0000 Max. :0.840978 Max. :0.9985

```

根据这个 [帖子](http://www.r-bloggers.com/things-to-try-after-user-part-1-deep-learning-with-h2o/)，提供了“具有所有可能结果的概率的预测标签（或回归问题的数值输出）”

作者：mdavey，2016 年 4 月 4 日。

发布在 [数据](https://mdavey.wordpress.com/category/data/)、[未分类](https://mdavey.wordpress.com/category/uncategorized/) 中
