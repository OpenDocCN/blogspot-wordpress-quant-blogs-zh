<!--yml
category: 未分类
date: 2024-05-18 15:00:21
-->

# Timely Portfolio: d3 Lifeline from vega and clickme

> 来源：[http://timelyportfolio.blogspot.com/2013/04/d3-lifeline-from-vega-and-clickme.html#0001-01-01](http://timelyportfolio.blogspot.com/2013/04/d3-lifeline-from-vega-and-clickme.html#0001-01-01)

This has been an exciting week for [d3.js](http://d3js.org) and [R](http://r-project.org) with the

1.  release of [**vega**](https://github.com/trifacta/vega) by the data vis powerhouses at [Trifacta](http://trifacta.com/about)
2.  launch of [**clickme**](https://github.com/nachocab/clickme) and already significant rewrite to accommodate **vega**
3.  inception of a very promising d3 templates [DexCharts](https://github.com/PatMartin/DexCharts) described in [multiple posts](http://dexvis.wordpress.com).

I am glad to have had time to play with all three, and I have actually already used them for legitimate purposes. I only understand the basics, but I thought I would post how we can combine a **clickme** ractive and a **vega** template to produce the [lifelines example](http://trifacta.github.com/vega/editor/) included in **vega**. I like the lifelines example because it is the one with the most complex data source and number of d3 elements. Fortunately, both projects are well documented, especially for early releases. I strongly recommend reading through both wikis to quickly progress along the learning curve. I will try to fill in some gaps in [the **clickme** “**clickme** and **vega**” wiki page](https://github.com/nachocab/clickme/wiki/clickme-and-vega).

### **vega** frameworks

**vega** frameworks are JSON objects to ease the construction of interactive d3 visualizations. In the [wiki](https://github.com/trifacta/vega/wiki/Documentation), the authors liken **vega** to **ggplot2** but say

> However, in service of rapid specification these systems make a number of decisions on behalf of the user, and also impose limits on the type of visualizations one can create. **vega** is intended to be lower-level, enabling fine-gained control of the visualization design.

**ggplot2** and **lattice** users should immediately be familiar with words like “axes”,“scales”, “data”, and “marks”.

### **clickme** ractives

**clickme** ractives are a directory structure with files that provide at a minimum a R markdown template (template.rmd) for a visualization and a R translator (translator.r) to allow the use of R data and calculations in the finished HTML5 rendering. Although **clickme** was developed unaware of **vega**, the author immediately saw the potential of combining both and rewrote **clickme** to allow easy integration. The synergy of the two is demonstrated by the ability to create 7 **vega** examples with all the same template.rmd and translator.r. **vega** templates now fall in the spec subdirectory of the data directory of a **clickme** ractive.

### **clickme** filling **vega**

If we look at the original [lifelines **vega** spec](https://github.com/trifacta/vega/blob/master/examples/vega/lifelines.json), we will see some spots where we might like R to provide the information, such as

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

I am guessing that some R users might stumble a little with the data section of this JSON, so let's translate into lists, something I hope might be a little more familiar.

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

Then in the translator.R part of our ractive, we can use the [rjson package](http://cran.r-project.org/web/packages/rjson/index.html) to translate the list into a JSON equivalent. Most of the data for d3 and **vega** can usually  just come from data.frames. The **clickme** author actually also wrote **df2json** to better handle the translation of data.frames to JSON, and there are numerous ractive examples using data.frames in the **clickme** package.

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

Now we just need to fill the **vega** spec with our data. We can replace the data section with

```
"data": {{ get_data_as_json(opts) }} 
```

When we run the **clickme_vega** function, **clickme** will use the [**knit_expand** function](https://github.com/yihui/knitr/blob/master/man/knit_expand.Rd) from **knitr** to expand/run the get_data_as_json function on the data supplied as a parameter to **clickme_vega** and replace like a mail merge with our translated JSON data representation.  With our ractive, we will also specify height, width, margins, title, etc. We can produce our HTML page with just one line.

```
clickme_vega(data,"lifelines",params=list(height=100,width=400,padding=list(top=60, left=5, bottom= 30, right=30)))
```

### R to clickme to vega to d3 visualization workflow

Assuming we already have a predefined **clickme** ractive and **vega** spec, the workflow from R to a pretty d3 visualization becomes ridiculously easy:

2.  Just like we would if we were creating an R graph, we get our data, clean our data, and run our calculations

3.  in R, we run clickme_vega(data=our_data_from_step1, ractive=nameofourractive)

4.  show off and use our amazing, beautiful, and interactive visualization (might need a simple http server for some cases).

If we do not have a predefined **clickme** ractive, then we can easily borrow/steal from the [unbelievable repository of d3 examples](http://biovisualize.github.com/d3visualization/) or a possible future **vega** repository, and follow the instructions in the [**clickme** wiki](https://github.com/nachocab/clickme/wiki/Creating-the-%22par_coord%22-ractive) to convert into a ractive.

### Live Example

if embed does not show go to [http://bl.ocks.org/timelyportfolio/5316682](http://bl.ocks.org/timelyportfolio/5316682).

### Reproduce me

Below is all the code to run this specific example. The ractive and **vega** spec are in this [Git repo](https://github.com/timelyportfolio/clickme_vega_lifelines/).

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