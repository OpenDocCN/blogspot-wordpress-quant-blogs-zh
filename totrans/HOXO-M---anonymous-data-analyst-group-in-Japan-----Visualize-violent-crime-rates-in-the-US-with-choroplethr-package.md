<!--yml
category: 未分类
date: 2024-05-18 06:48:13
-->

# HOXO-M - anonymous data analyst group in Japan - : Visualize violent crime rates in the US with choroplethr package

> 来源：[http://mockquant.blogspot.com/2014/04/visualize-violent-crime-rates-in-us.html#0001-01-01](http://mockquant.blogspot.com/2014/04/visualize-violent-crime-rates-in-us.html#0001-01-01)

<title>Visualize violent crime rates in different US States with choroplethr package</title>

I have read

[choroplethr package](http://cran.r-project.org/web/packages/choroplethr/index.html)

from the blog post

[Animated Choropleths in R](http://blog.revolutionanalytics.com/2014/04/animated-choropleths-in-r.html)

a few days ago. As a another visualization tool in R language, I want to try this one.

To install the latest stable release(CRAN) type the following from an R console:

```
install.packages("choroplethr") 
```

To install the development version using the devtools package from github, type the following::

```
library(devtools)
install_github("choroplethr", "trulia")
library(choroplethr) 
```

It's not interesting for me to run just example codes written in choroplethr package. Instead, I used other data from

[rMaps](https://github.com/ramnathv/rMaps)

package as a quick data source and visualize it!

```
library(devtools)
install_github("ramnathv/rCharts@dev")
install_github("ramnathv/rMaps") 
```

Now we can use

**violent crime rates data in the US**

included in rMaps package.

We can create

**animated choropleths**

as the following page:

In my case, we just process the data and visualize it as the following simple code:

```
# load packages
library(rMaps)
library(choroplethr)
# initialization list and get years from violent_crime data
choropleths = list()
# Get years for loop
years <- sort(unique(violent_crime$Year))
# convert to level data
violent_crime$Crime <- cut(violent_crime$Crime, 9)
# Create choropleth component.
for (i in 1:length(years)) {
    df <- subset(violent_crime, Year == years[i])
    # We need to change the column names for choroplethr function
    colnames(df) <- c("Year", "region", "value")
    # Cut decimal off df$value <- round(df$value)
    title <- paste0("Violent crime rates: ", years[i])
    choropleths[[i]] = choroplethr(df, "state", title = title)
}
# Vizualize it!
choroplethr_animate(choropleths) 
```

The result is published via Dropbox as the following (image)link.

Enjoy!