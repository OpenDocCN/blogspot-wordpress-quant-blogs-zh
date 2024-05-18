<!--yml
category: 未分类
date: 2024-05-18 15:00:40
-->

# Timely Portfolio: “Building ractives is so addictive it should be illegal!”

> 来源：[http://timelyportfolio.blogspot.com/2013/03/building-ractives-is-so-addictive-it.html#0001-01-01](http://timelyportfolio.blogspot.com/2013/03/building-ractives-is-so-addictive-it.html#0001-01-01)

[clickme](https://github.com/nachocab/clickme) is an amazing R package. I was not sure what to expect when I first saw [Nacho Caballero's](https://twitter.com/nachocaballero) announcement. I actually was both skeptical and intimidated, but neither reaction was justified. The examples prove its power, and [his wiki tutorials](https://github.com/nachocab/clickme/wiki/_pages) ease the noobie difficulties. Very similar to shiny, clickme serves as an integration point for html, javascript (especially [d3](http://d3.js.org)), and R. While clickme does not allow the R websocket interactivity that shiny does, its more concentrated focus on quick reproducibility and sharing makes it a very useful tool. This is very much in the spirit of [http://dexvis.wordpress.com/ Reusable Charts](http://dexvis.wordpress.com/2013/03/27/reusable-charts-part-6-parallel-coordinates/). **ractives** [defined](https://github.com/nachocab/clickme/wiki) as

> (short for interactives-a hat tip to Neal Stephenson), which are simple folder structures that contain a template file used to populate the JS code with R input data

provide the structure for clickme to produce an html file from

1.  a template in R markdown (template.rmd)
2.  a translator R script (translator.r)
3.  a data source
4.  external scripts (probably javascript) and styles (.css).

Inspired by the [clickme longitudinal heatmap example](http://bl.ocks.org/timelyportfolio/raw/5225228/), I just had to try to create my own ractive. I thought [Mike Bostock's line chart example](http://bl.ocks.org/mbostock/3902569) would serve as a nice template for my first ractive. The data not surprisingly will come from the R finance package **PerformanceAnalytics** dataset named **managers**. With very minor modifications to the Bostock source and a simple custom R script translator (translator.R shown below), we have everything we need for this ractive, which I will call multiline.

```
#' Translate the data object to the format expected by current template

#'

#' @param data input data object

#' @param opts options of current template

#' @return The opts variable with the opts$data variable filled in

translate <- function(data, opts = NULL) {

    require(df2json)

    # I would like to generalize this to handle both price and return right

    # now just handles return clickme template.Rmd javascript can handle

    # prices or cumulative so we will send cumulative which can serve as price

    # remove na

    data[is.na(data)] <- 0

    # get cumulative growth

    data <- cumprod(1 + data)

    # convert to data frame

    data.df <- data.frame(cbind(format(index(data), "%Y-%m-%d"), coredata(data)))

    colnames(data.df)[1] = "date"

    # melt the data frame so we have our data in long form

    data.melt <- melt(data.df, id.vars = 1, stringsAsFactors = FALSE)

    colnames(data.melt) <- c("date", "indexname", "price")

    # remove periods from indexnames to prevent javascript confusion these .

    # usually come from spaces in the colnames when melted

    data.melt[, "indexname"] <- apply(matrix(data.melt[, "indexname"]), 2, gsub, 

        pattern = "[.]", replacement = "")

    opts$data <- df2json(data.melt)

    opts

} 
```

Now to create our first clickme html page, we just need a couple lines of code in R.

```
# if not already installed, uncomment the tow lines below

# library(devtools) install_github('clickme', 'nachocab')

require(clickme)

# set location where you put your multiline ractive

set_root_path("your-path-goes-here/ractives") 
```

```
require(PerformanceAnalytics)

data(managers)  #although I use managers, really any xts series of returns will work

clickme(managers, "multiline") 
```

Then, we have a web page that will create an interactive d3 line chart using the cumulative growth of the **managers** return series. If you do not see the embed below, then please follow the [link](http://bl.ocks.org/timelyportfolio/5257985).

Eventually, it will be very nice to have an entire gallery of amazing ractives.