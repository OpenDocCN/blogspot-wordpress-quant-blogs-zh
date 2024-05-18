<!--yml
category: 未分类
date: 2024-05-18 15:00:36
-->

# Timely Portfolio: Old Price Tables in Modern d3 Visualization

> 来源：[http://timelyportfolio.blogspot.com/2013/04/old-price-tables-in-modern-d3.html#0001-01-01](http://timelyportfolio.blogspot.com/2013/04/old-price-tables-in-modern-d3.html#0001-01-01)

In my post [Dust off 130 Year Old Gold Books on Google Bookshelf](http://timelyportfolio.blogspot.com/2013/03/dust-off-130-year-old-gold-books-on.html), I reproduced some of the old and way out of copyright price tables from the appendices in [Gold and Prices Since 1873 by James Laurence Laughlin](http://books.google.com/books?id=UFMuAAAAYAAJ&printsec=frontcover#v=thumbnail&q&f=false) using **latticeExtra xyplot**. Now, with the [**clickme**](https://github.com/nachocab/clickme) multiline [d3](http://d3js.org) ractive built in my last post [“Building ractives is so addictive it should be illegal!”](http://timelyportfolio.blogspot.com/2013/03/building-ractives-is-so-addictive-it.html), we can easily transform this data into an interactive time series line chart.

I tried to generalize the [multiline ractive](https://github.com/timelyportfolio/clickme_multiline_generic/) to create almost any line chart for an xts object from [R](http://r-project.org). See the [commit history](https://github.com/timelyportfolio/clickme_multiline_generic/commits/) for the minor modifications that I made to the [original ractive](https://github.com/timelyportfolio/clickme_multiline):

1.  Take data as given instead of transforming to a cumulative line
2.  Allow parameters for a title and the location of the x-axis
3.  Handle data series with differing start and end dates

We can build the html file using [**clickme**](https://github.com/nachocab/clickme) with a couple of lines of R code.

```
# if not already installed, uncomment the two lines below
# library(devtools) install_github('clickme', 'nachocab')

require(clickme)
# set location where you put your multiline ractive
set_root_path("path to your ractive/r") 
```

```
clickme(data = priceTables["1850::", c(-1, -6, -8, -11, -12)], ractive = "clickme_multiline_generic", 
    params = list(title = "Price Tables from <em> Gold and Prices Since 1873 </em>", 
        x_axis_location = 100)) 
```

I had not seen an example of passing parameters, so I used title and x_axis_location as a test for how **clickme** handles parameters. If I read the source correctly, the template_config.yml specifies permissible parameters. Then the parameters can be specified by a list provided as params to the **clickme** function as shown above.

```
...
default_parameters: {
  width: 960,
  height: 500,
  title,
  x_axis_location
}
... 
```