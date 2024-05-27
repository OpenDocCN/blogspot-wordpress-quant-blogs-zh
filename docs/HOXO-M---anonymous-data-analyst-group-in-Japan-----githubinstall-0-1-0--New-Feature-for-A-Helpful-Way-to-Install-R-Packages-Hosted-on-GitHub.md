<!--yml

类别：未分类

日期：2024-05-18 06:47:37

-->

# HOXO-M - 日本的匿名数据分析师团队 - ：githubinstall 0.1.0：安装在 GitHub 上托管的 R 包的新功能

> 来源：[`mockquant.blogspot.com/2016/08/githubinstall-010-new-feature-for.html#0001-01-01`](http://mockquant.blogspot.com/2016/08/githubinstall-010-new-feature-for.html#0001-01-01)

我们已经更新了我们的**githubinstall**软件包。现在它在[CRAN](https://cran.rstudio.com/web/packages/githubinstall/) 上了。

### 基础知识

使用该软件包，您可以在 GitHub 上安装 R 包而不需要用户名。

```
library(githubinstall)
githubinstall("AnomalyDetection")
# It is same as devtools::install_github("twitter/AnomalyDetection")
```

我们在[之前的条目](http://mockquant.blogspot.jp/2016/06/githubinstall-new-r-package-for-easy-to.html) 中介绍了该软件包。

您可以按照以下方式安装或更新软件包。

```
install.packages("githubinstall")
```

### 新功能

我们在新版本的软件包中添加了一个新功能。

现在，您可以通过指定 Git 引用（分支、标签、提交和拉取请求）来安装软件包。

开发者们在 GitHub 上管理 R 包的政策上存在分歧。如果一个软件包将在“develop”分支开发，您可能希望从该分支安装软件包。

`gh_install_packages()` 有 `ref` 参数以指定 Git 引用。例如，您可以按照以下方式从 ["develop" 分支](https://github.com/swish-climate-impact-assessment/awaptools/tree/develop) 安装**awaptools**：

```
githubinstall("awaptools", ref = "develop")
```

有时您可能遇到安装软件包失败的情况，因为其存储库 HEAD 已经损坏。在这种情况下，您可以指定一个标签或提交到 `ref`。在几乎所有情况下，标签是添加到未损坏提交中的。例如，您可以从 [“v0.0.3” 标签](https://github.com/hoxo-m/densratio/releases/tag/v0.0.3) 安装**densratio** 如下： 

```
githubinstall("densratio", ref = "v0.0.3")
```

即使您找不到这样的标签，也可以从未损坏的任何提交中安装软件包。例如，您可以按照以下方式从 [“e8233e6” 提交](https://github.com/hoxo-m/densratio/commit/e8233e651dbef2b34a8c9c2e4432594a13ea8de7) 安装**densratio**：

```
githubinstall("densratio", ref = "e8233e6")
```

最后，您可以作为拉取请求找到修复错误的补丁。在这种情况下，您可以使用 `github_pull()` 指定拉取请求到 `ref`。例如，您可以按照以下方式从 [拉取请求＃2058](https://github.com/hadley/dplyr/pull/2058) 安装**dplyr**：

```
githubinstall("dplyr", ref = github_pull("2058"))
```

### 修复的 Bug

我们已经修复了一些在 [Issues](https://github.com/hoxo-m/githubinstall/issues) 上报告的错误。这些已在 [NEWS](https://github.com/hoxo-m/githubinstall/releases/tag/v0.1.0) 上有详细说明。

如果您发现了一些错误或需要新功能，我们将不胜感激。
