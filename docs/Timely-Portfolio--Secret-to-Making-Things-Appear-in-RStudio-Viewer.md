<!--yml

分类：未分类

日期：2024-05-18 14:50:38

-->

# 及时投资组合：RStudio 查看器的出现秘诀

> 来源：[`timelyportfolio.blogspot.com/2014/11/secret-to-making-things-appear-in.html#0001-01-01`](http://timelyportfolio.blogspot.com/2014/11/secret-to-making-things-appear-in.html#0001-01-01)

我绝不是这方面的权威来源，但我认为我已经发现了 htmltools `html_print`背后的秘密，它选择了 RStudio 查看器的浏览器，而不是像`utils::browseURL`这样的默认浏览器。以下是一个简短的代码片段，希望它能解释正在发生的事情。看起来你只需要一个以`viewhtml*`开头的临时目录。

```
library(htmltools)
library(pipeR)

# htmltools from RStudio very nicely
# makes things appear in the Viewer Window
"<h3>Hello in RStudio Viewer</h3>" %>>%
  HTML %>>%
  html_print

# there is a little secret to doing the same
# without htmltools
"<h3>Hello in RStudio Viewer</h3>" %>>%
  HTML %>>%
  # and the secret is to place in a temp directory
  # with the pattern viewhtml
  (
  ht ~
    tempfile("viewhtml") %>>%
    (~ dir.create(.) ) %>>%
    (~ save_html(ht, file = file.path(.,"index.html")) ) %>>%
    ( getOption("viewer")(file.path(.,"index.html")) )
  )

# to see it in action look at the code change
# in this project
utils::browseURL("https://github.com/bryanhanson/exCon/pull/1/files")

```

我提到它的唯一原因是，我更愿意留在 RStudio 环境中，而不是切换到浏览器上下文。我仍然

**强烈推荐使用 htmltools 的标签**

作为在 RStudio 专家指导下无缝工作和按预期工作的最佳方法。
