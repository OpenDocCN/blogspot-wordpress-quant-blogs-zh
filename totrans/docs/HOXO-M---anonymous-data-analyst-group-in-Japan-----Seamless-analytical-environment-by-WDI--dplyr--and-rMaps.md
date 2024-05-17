<!--yml
category: 未分类
date: 2024-05-18 06:48:17
-->

# HOXO-M - anonymous data analyst group in Japan - : Seamless analytical environment by WDI, dplyr, and rMaps

> 来源：[http://mockquant.blogspot.com/2014/03/seamless-analytical-environment-by-wdi.html#0001-01-01](http://mockquant.blogspot.com/2014/03/seamless-analytical-environment-by-wdi.html#0001-01-01)

Recently I found that My R Guru [@ramnath_vaidya](https://twitter.com/ramnath_vaidya) is developping a new visualization package [rMaps](https://github.com/ramnathv/rMaps).

I was so excited when I saw it for the first time and I think that it's really awesome for plotting any data on a map.

Let me explain how we can

*   Get data(WDI package)
*   Manipulate data(dplyr package)
*   Visualize the result(rMaps package)

with greate R packages.

Except for rMaps package, you can install these packages(WDI, dplyr) from CRAN by usual way.

```
install.packages(c("WDI", "dplyr")) 
```

To install rMaps package, you just write the following commands on R console.

```
require(devtools)
install_github("ramnathv/rCharts@dev")
install_github("ramnathv/rMaps") 
```

(Don't forget to install “devtools” package to use install_github function.)

Now, as an example, I show you that

*   Get “CO2 emissions (kt)” data from World Bank by WDI package
*   Summarze it to by dplyr package
*   Visualize it by rMaps package

The result is shown below:

…Enjoy!!!

By the way, recently an Japanese R professional guy often posts his greate articles. I recommend you to see these articles if you are interested in visualizing and dplyr especially.

Source codes:

```
library(WDI)
library(rMaps)
library(dplyr)
library(countrycode)
# Get CO2 emission data from World bank
# Data source : http://data.worldbank.org/indicator/EN.ATM.CO2E.KT/
df <- WDI(country=c("all"), 
          indicator="EN.ATM.CO2E.KT", 
          start=2004, end=2013)
# Data manipulation By dplyr
data <- df %.% 
  na.omit() %.%
  #Add iso3c format country code 
  mutate(iso3c=countrycode(iso2c, "iso2c", "iso3c")) %.% 
  group_by(iso3c) %.%
  #Get the most recent CO2 emission data
  summarize(value=EN.ATM.CO2E.KT[which.max(year)])
# Visualize it by rMaps
i1 <- ichoropleth(value~iso3c, data, map="world")
i1$show("iframesrc", cdn = TRUE) # for blog post
#... or you can direct plot by just evaluating "i1" on R console. 
```