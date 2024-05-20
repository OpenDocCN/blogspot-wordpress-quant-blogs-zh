<!--yml
category: 未分类
date: 2024-05-18 14:50:38
-->

# Timely Portfolio: Secret to Making Things Appear in RStudio Viewer

> 来源：[http://timelyportfolio.blogspot.com/2014/11/secret-to-making-things-appear-in.html#0001-01-01](http://timelyportfolio.blogspot.com/2014/11/secret-to-making-things-appear-in.html#0001-01-01)

I am by no means an authoritative source on this, but I think I found out the secret behind htmltools `html_print` that chooses the RStudio Viewer browser rather than your default browser like `utils::browseURL`. Here is a quick code snippet that hopefully explains what is happening. It appears you just need a temp directory with the pattern starting with `viewhtml*`.

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

The only reason I mention it is that I much prefer to stay in the RStudio environment instead of switching contexts to a browser.  I still

**firmly recommend using tags from htmltools**

as the best method to make all this work seamlessly and as intended by the experts at RStudio.