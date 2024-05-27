<!--yml

类别：未分类

日期：2024-05-18 06:47:41

-->

# HOXO-M - 日本匿名数据分析小组 - : githubinstall - New R Package for Easy to Install R Packages on GitHub

> 来源：[`mockquant.blogspot.com/2016/06/githubinstall-new-r-package-for-easy-to.html#0001-01-01`](http://mockquant.blogspot.com/2016/06/githubinstall-new-r-package-for-easy-to.html#0001-01-01)

## 1\. 概述

越来越多的 R 软件包是由世界各地的各种人创建的。 其部分原因是 **devtools** 软件包，它使得开发 R 软件包变得容易 [[1]](https://www.rstudio.com/products/rpackages/devtools/)。 **devtools** 软件包不仅简化了开发 R 软件包的流程，还提供了另一种分发 R 软件包的方法。

开发人员发布 R 软件包时，通常会使用 CRAN [[2]](https://cran.r-project.org)。 您可以使用`install.package()`安装可以在 CRAN 上获得的软件包。 例如，您可以按照以下方式安装**dplyr**软件包：

```
install.packages("dplyr")
```

**devtools** 软件包提供了`install_github()`，可以从 GitHub 安装软件包。

```
library(devtools)
install_github("hadley/dplyr")
```

因此，开发人员可以在 GitHub 上开发 R 软件包，并进行分发。 此外，还有一些开发人员，他们并没有打算提交到 CRAN。 例如，Twitter, Inc. 在 GitHub 上提供了**AnomalyDetection**软件包，但它将不会在 CRAN 上提供 [[3]](https://blog.twitter.com/2015/introducing-practical-and-robust-anomaly-detection-in-a-time-series)。 您可以使用**devtools**轻松安装这样的软件包。

```
library(devtools)
install_github("twitter/AnomalyDetection")
```

`install.packages()` 和 `install_github()` 在所需参数上有所不同。 `install.packages()` 需要软件包名称，而`install_github()` 需要仓库名称。 这意味着当您想要在 GitHub 上安装一个软件包时，您必须正确记住其仓库名称。

麻烦的是 GitHub 的用户名经常很难记住。 开发人员考虑软件包名称，以便用户可以直观地理解其功能。 但是，他们常常粗心地决定用户名。 例如，**ggfortify** 是 GitHub 上一个很棒的软件包，但是谁创建了它？用户名是什么？答案是 *sinhrks* [[4]](https://github.com/sinhrks/ggfortify)。 似乎很难记住它。

**githubinstall** 软件包提供了一种方式，可以仅凭借软件包名称就像`install.packages()`一样在 GitHub 上安装软件包。

```
library(githubinstall)
githubinstall("AnomalyDetection")
```

```
Suggetion:
 - twitter/AnomalyDetection
Do you install the package? 

1: Yes (Install)
2: No (Cancel)
```

`githubinstall()` 会根据软件包名称建议 GitHub 仓库，并询问您是否要执行安装。

此外，您可能会成功安装软件包，即使只是凭借模糊的字符串搜索也能自动纠正其拼写，因为我们的软件包会自动纠正其拼写，从而对模糊的字符串搜索进行模糊查询。

```
githubinstall("AnomaryDetection")
githubinstall("AnomalyDetect")
githubinstall("anomaly-detection")
```

## 2\. 安装

您可以从 CRAN 安装**githubinstall**软件包。

```
install.packages("githubinstall")
```

**githubinstall** 软件包的源代码可以在 GitHub 上找到

## 3\. 详情

**githubinstall** 软件包提供了几个有用的函数。

+   `githubinstall()` 或 `gh_install_packages()`

+   `gh_suggest()`

+   `gh_suggest_username()`

+   `gh_list_packages()`

+   `gh_search_packages()`

+   `gh_show_source()`

+   `gh_update_package_list()`

这些函数具有公共前缀`gh`。 `githubinstall()`是`gh_install_packages()`的别名。

要使用这些函数，首先应按以下方式加载包。

### 3.1\. 从 GitHub 安装包

`githubinstall()`只需输入包名称即可安装 GitHub 上的包。

```
githubinstall("AnomalyDetection")
```

```
Suggestion:
 - twitter/AnomalyDetection
Do you install the package? 

1: Yes (Install)
2: No (Cancel)

Selection: 
```

该函数建议 GitHub 存储库。 如果键入‘1’并按‘enter’，则将开始安装该包。 建议是通过查找 GitHub 上的 R 包列表来进行的。 该列表由[Gepuro Task Views](http://rpkg.gepuro.net)提供。

如果发现多个候选项，则可以选择其中之一。

```
Select one repository or, hit 0 to cancel. 

1: amurali2/cats      cats
2: danielwilhelm/cats No description or website provided.
3: hilaryparker/cats  An R package for cat-related functions #rcatladies
4: lolibear/cats      No description or website provided.
5: rafalszota/cats    No description or website provided.
6: tahir275/cats      ff

Selection: 
```

`githubinstall()`是`gh_install_packages()`的别名。

```
gh_install_packages("AnomalyDetection")
```

### 3.2\. 提出存储库建议

`githubinstall()`提示您安装建议的包。 但您可能只想知道建议的内容。

`gh_suggest()`以向量形式返回建议的存储库名称。

```
gh_suggest("AnomalyDetection")
```

```
## [1] "twitter/AnomalyDetection"
```

```
## [1] "amurali2/cats"       "danielwilhelm/cats"  "davidluizrusso/cats"
## [4] "hilaryparker/cats"   "lolibear/cats"       "rafalszota/cats"    
## [7] "tahir275/cats"
```

此外，如果您想从模糊记忆中了解用户名，`gh_suggest_username()`很有用。

```
gh_suggest_username("hadly")
```

```
## [1] "hadley"
```

```
gh_suggest_username("yuhui")
```

```
## [1] "yihui"
```

### 3.3\. 列出包

`gh_list_packages()`以`data.frame`的形式返回 GitHub 上的 R 包存储库列表。

例如，如果要获取*hadley*创建的存储库，运行以下命令。

```
hadleyverse <-  gh_list_packages(username = "hadley")
head(hadleyverse)
```

```
##   username package_name                                              title
## 1   hadley   assertthat                     User friendly assertions for R
## 2   hadley    babynames An R package contain all baby names data from the 
## 3   hadley    bigrquery          An interface to Google's bigquery from R.
## 4   hadley     bookdown                                              Watch
## 5   hadley   clusterfly An R package for visualising high-dimensional clus
## 6   hadley      decumar                           An alternative to sweave
```

通过使用结果，您可以安装 hadley 创建的所有包。

```
repos <-  with(hadleyverse, paste(username, package_name, sep="/"))
githubinstall(repos) # I have not tried it
```

### 3.4\. 按关键字搜索包

`gh_search_packages()`返回包含给定关键字的标题的 GitHub 上的 R 包存储库列表。

例如，如果要搜索与*lasso*相关的包，运行以下命令。

```
gh_search_packages("lasso")
```

```
##           username     package_name                                  title
## 1  ChingChuan-Chen             milr  multiple-instance logistic regressi..
## 2       YaohuiZeng         biglasso  Big Lasso: Extending Lasso Model Fi..
## 3      huayingfang          CCLasso  CCLasso: Correlation Inference for ..
## 4         mlampros FeatureSelection  Feature Selection in R using glmnet..
## 5             pnnl        glmnetLRC  Lasso and Elastic-Net Logistic Regr..
## 6       statsmaths         genlasso  Path algorithm for generalized lass..
## 7       vincent-dk         logitsgl  Fit Logistic Regression with Multi-..
## 8       vincent-dk             lsgl  Linear Multiple Output Using Sparse..
## 9       vincent-dk             msgl  High Dimensional Multiclass Classif..
## 10      vstanislas             GGEE  R Package for the Group Lasso Gene-..
## 11          zdk123       BatchStARS  R package for Stability Approach to..
## 12          zdk123           pulsar  R package for Stability Approach to..
```

### 3.5\. 显示 GitHub 上函数的源代码

`gh_show_source()`查找 GitHub 上给定函数的源代码，并尝试在 Web 浏览器中打开该位置。

```
gh_show_source("mutate", "dplyr")
```

如果已加载包含该函数的包，可以直接输入函数。

```
library(dplyr)
gh_show_source(mutate)
```

此功能可能在 Safari 上无法正常工作。

### 3.6\. 更新 R 包列表

**githubinstall**包使用[Gepuro Task Views](http://rpkg.gepuro.net)获取 GitHub 上 R 包的列表。 Gepuro Task Views 每天都会爬取 GitHub 并更新信息。 该包每次加载时都会从 Gepuro Task Views 下载 R 包的列表。 因此，您可以在新的 R 会话中始终使用最新的包列表。

但是，您可能长时间使用 R 会话。 这种情况下，`gh_update_package_list()`很有用。

`gh_update_package_list()`显式更新下载的 R 包列表。
