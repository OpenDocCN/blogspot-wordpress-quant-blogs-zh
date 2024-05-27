<!--yml

分类：未分类

日期：2024-05-18 15:00:21

-->

# 及时投资组合：来自 vega 和 clickme 的 d3 生命线

> 来源：[`timelyportfolio.blogspot.com/2013/04/d3-lifeline-from-vega-and-clickme.html#0001-01-01`](http://timelyportfolio.blogspot.com/2013/04/d3-lifeline-from-vega-and-clickme.html#0001-01-01)

这周对[d3.js](http://d3js.org)和[R](http://r-project.org)来说是一个激动人心的时刻，随着

1.  数据可视化巨头[Trifacta](http://trifacta.com/about)发布了[**vega**](https://github.com/trifacta/vega)

1.  推出了[**clickme**](https://github.com/nachocab/clickme)并且已经进行了重大的重写以适应**vega**

1.  一个非常有前途的 d3 模板[DexCharts](https://github.com/PatMartin/DexCharts)在[多篇文章](http://dexvis.wordpress.com)中描述。

我很高兴有时间玩这三个，实际上我已经用它们处理过合法的工作了。我只懂基础，但我还是想分享如何将一个**clickme** ractive 和一个**vega**模板结合起来，以生成**vega**中包含的[生命线示例](http://trifacta.github.com/vega/editor/)。我喜欢生命线示例，因为它有最复杂的数据源和最多的 d3 元素。幸运的是，这两个项目都有很好的文档，特别是对于早期版本。我强烈建议阅读两个维基百科，以快速提高学习曲线。我会在[**clickme**“**clickme**和**vega**”维基页](https://github.com/nachocab/clickme/wiki/clickme-and-vega)中填补一些空白。

### **vega**框架

**vega**框架是 JSON 对象，用于简化交互式 d3 可视化的构建。在[维基百科](https://github.com/trifacta/vega/wiki/Documentation)中，作者将**vega**比作**ggplot2**，但说

> 然而，为了快速制定规格，这些系统在用户不知情的情况下做出了许多决定，并且对可以创建的图表类型施加了限制。**vega**旨在成为更底层的技术，以实现对可视化设计的精细控制。

**ggplot2**和**lattice**用户应该立即熟悉诸如“轴”，“刻度”，“数据”和“标记”之类的词汇。

### **clickme** ractives

**clickme** ractives 是一个文件夹结构，包含至少一个 R markdown 模板（template.rmd）和一个 R 翻译器（translator.r），以便在最终的 HTML5 渲染中使用 R 数据和计算。尽管**clickme**是在不知道**vega**的情况下开发的，但作者立即看到了将两者结合的可能性，并重写了**clickme**以实现轻松集成。这两个的协同作用体现在能够使用相同的 template.rmd 和 translator.r 创建 7 个**vega**示例。现在**vega**模板位于**clickme** ractive 的数据目录的 spec 子目录中。

### **clickme**填充**vega**

如果我们查看原始的[lifelines **vega**规格](https://github.com/trifacta/vega/blob/master/examples/vega/lifelines.json)，我们会看到一些我们可能希望 R 提供信息的地方，比如：

```
...
  "width": 400,
  "height": 100,
  "padding": {"top": 60, "left": 5, "bottom": 30, "right": 30},
  "data": [
    {
      "name": "people",
      "values": [
        {"label":"Washington", "born":-7506057600000, "died":-5365324800000, 
         "enter":-5701424400000, "leave":-5453884800000},
...
      "name": "events",
      "format": {"type":"json", "parse":{"when":"date"}},
      "values": [
        {"name":"Decl. of Independence", "when":"July 4, 1776"}, 
```

我猜测一些 R 用户可能对这个 JSON 的数据部分有点困惑，所以让我们将其转换为列表，这是我希望稍微更熟悉一点的东西。

```
data = list(
    list(name="people",
       values=list(
                      list(label="Washington", born=-7506057600000, died=-5365324800000, enter=-5701424400000, leave=-5453884800000),
                      list(label="Adams", born=-7389766800000, died=-4528285200000, enter=-5453884800000, leave=-5327740800000),
                      list(label="Jefferson", born=-7154586000000, died=-4528285200000, enter=-5327740800000, leave=-5075280000000),
                      list(label="Madison", born=-6904544400000, died=-4213184400000, enter=-5075280000000, leave=-4822819200000),
                      list(label="Monroe", born=-6679904400000, died=-4370518800000, enter=-4822819200000, leave=-4570358400000)
                  )
        ),
    list(
      name= "events",
      format= list(type="json", parse=list(when="date")),
      values= list(
                list(name="Decl. of Independence", when="July 4, 1776"),
                list(name="U.S. Constitution",     when="3/4/1789"),
                list(name="Louisiana Purchase",    when="April 30, 1803"),
                list(name="Monroe Doctrine",       when="Dec 2, 1823")
              )

    )
) 
```

然后在我们的 ractive 的 translator.R 部分，我们可以使用[rjson 包](http://cran.r-project.org/web/packages/rjson/index.html)将列表转换为 JSON 等价物。大多数 d3 和**vega**的数据通常可以直接来自 data.frames。**clickme**作者实际上还写了**df2json**以更好地处理 data.frames 到 JSON 的转换，**clickme**包中有许多使用 data.frames 的 ractive 示例。

```
 get_data_as_json <- function(opts) {
  ...
    } else {
      library(rjson)
      json_data <- toJSON(opts$data) ##opts$data comes from the data parameter of the clickme function   
    }
      json_data
  } 
```

现在我们只需要用我们的数据填充**vega**规格。我们可以用以下内容替换数据部分：

```
"data": {{ get_data_as_json(opts) }} 
```

当我们运行**clickme_vega**函数时，**clickme**将使用**knitr**中的[**knit_expand**函数](https://github.com/yihui/knitr/blob/master/man/knit_expand.Rd)来扩展/运行在**clickme_vega**中作为参数提供的数据上的 get_data_as_json 函数，并使用我们的翻译 JSON 数据表示进行替换，就像邮件合并一样。在我们的 ractive 中，我们还将指定高度、宽度、边距、标题等。我们只需一行就能生成我们的 HTML 页面。

```
clickme_vega(data,"lifelines",params=list(height=100,width=400,padding=list(top=60, left=5, bottom= 30, right=30)))
```

### R 到 clickme 到 vega 到 d3 可视化的工作流程

假设我们已经有了一个预定义的**clickme** ractive 和**vega**规格，从 R 到漂亮 d3 可视化的流程变得荒谬地简单：

1.  就像我们创建 R 图表时一样，我们获取数据、清洗数据、运行计算

1.  在 R 中，我们运行 clickme_vega(data=our_data_from_step1, ractive=nameofourractive)

1.  展示并使用我们惊人的、美丽的、互动式的可视化（某些情况下可能需要一个简单的 http 服务器）。

如果我们没有一个预定义的**clickme** ractive，那么我们可以很容易地从[令人难以置信的 d3 示例仓库](http://biovisualize.github.com/d3visualization/)或可能的未来**vega**仓库中借鉴/窃取，并遵循[**clickme**维基](https://github.com/nachocab/clickme/wiki/Creating-the-%22par_coord%22-ractive)中的说明将其转换为 ractive。

### 实时示例

如果嵌入式显示不出来，请访问[`bl.ocks.org/timelyportfolio/5316682`](http://bl.ocks.org/timelyportfolio/5316682)。

### 复制我

下面是运行这个特定示例的所有代码。ractive 和**vega**规格在这个[Git 仓库](https://github.com/timelyportfolio/clickme_vega_lifelines/)中。

```
#if not already installed, uncomment the two lines below
#library(devtools)
#install_github("clickme", "nachocab")

require(clickme)
#set location where you put your multiline ractive
set_root_path("path to your ractive/r")

data = list(
    list(name="people",
       values=list(
                      list(label="Washington", born=-7506057600000, died=-5365324800000, enter=-5701424400000, leave=-5453884800000),
                      list(label="Adams", born=-7389766800000, died=-4528285200000, enter=-5453884800000, leave=-5327740800000),
                      list(label="Jefferson", born=-7154586000000, died=-4528285200000, enter=-5327740800000, leave=-5075280000000),
                      list(label="Madison", born=-6904544400000, died=-4213184400000, enter=-5075280000000, leave=-4822819200000),
                      list(label="Monroe", born=-6679904400000, died=-4370518800000, enter=-4822819200000, leave=-4570358400000)
                  )
        ),
    list(
      name= "events",
      format= list(type="json", parse=list(when="date")),
      values= list(
                list(name="Decl. of Independence", when="July 4, 1776"),
                list(name="U.S. Constitution",     when="3/4/1789"),
                list(name="Louisiana Purchase",    when="April 30, 1803"),
                list(name="Monroe Doctrine",       when="Dec 2, 1823")
              )

    )
)

clickme_vega(data,"lifelines",params=list(height=100,width=400,padding=list(top=60, left=5, bottom= 30, right=30))) 
```
