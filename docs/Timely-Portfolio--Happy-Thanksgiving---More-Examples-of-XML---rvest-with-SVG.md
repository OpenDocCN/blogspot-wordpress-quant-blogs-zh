<!--yml

category: 未分类

date: 2024-05-18 14:50:30

-->

# 及时投资组合：感恩节快乐 | XML + rvest 与 SVG 的更多示例

> 来源：[`timelyportfolio.blogspot.com/2014/11/happy-thanksgiving-more-examples-of-xml.html#0001-01-01`](http://timelyportfolio.blogspot.com/2014/11/happy-thanksgiving-more-examples-of-xml.html#0001-01-01)

I did not intend for this little experiment to become a post, but I think the code builds nicely on the XML + rvest combination (also see yesterday’s [post](http://timelyportfolio.blogspot.com/2014/11/slightly-advanced-rvest-with-help-from_26.html)) for working with XML/HTML/SVG documents in R.

一切始于我在 iPhone 上的[Sketchbook 应用](https://itunes.apple.com/us/app/autodesk-sketchbook/id883738213?mt=8)上画画，我画了一只非常糟糕的火鸡。即使火鸡画得不好，我认为结合[vivus.js](http://maxwellito.github.io/vivus/)会很有趣。然而，Sketchbook 不支持导出 SVG，所以我导出为 PDF，并导入到[Inkscape](http://inkscape.org)中。最后的结果仍然是一个非常杂乱的 SVG 文件，因此我认为这将是我用`[rvest](http://blog.rstudio.org/2014/11/24/rvest-easy-web-scraping-with-r/)` + `[XML](http://www.amazon.com/gp/product/1461478995/ref=as_li_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=1461478995&linkCode=as2&tag=timelyp-20&linkId=FZJTULMKOUP5KIXE)`新技能的一个很好的测试/应用。代码打开 SVG，获取所有的`path`节点，将这些组装成带有 id = "turkey"的`svg`标签，然后添加一个脚本来使用`addDependency`为 vivus.js。

祝所有美国读者感恩节快乐。
