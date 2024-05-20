<!--yml
category: 未分类
date: 2024-05-18 14:49:40
-->

# Timely Portfolio: visNetwork, Currencies, and Minimum Spanning Trees

> 来源：[http://timelyportfolio.blogspot.com/2015/05/visnetwork-currencies-and-minimum.html#0001-01-01](http://timelyportfolio.blogspot.com/2015/05/visnetwork-currencies-and-minimum.html#0001-01-01)

Just because I’m ignorant doesn’t mean I won’t try things.  Feel free to correct any ignorance that follows.  More than anything I would like to feature the new htmlwidget [visNetwork](http://dataknowledge.github.io/visNetwork).  I thought  the example from [Minimum Spanning Trees in R](https://mktstk.wordpress.com/2015/01/03/minimum-spanning-trees-in-r/) applied to currency data (similar to this research paper [Minimum Spanning Tree Application in the Currency Market](http://www.nbs.sk/_img/Documents/_PUBLIK_NBS_FSR/Biatec/Rok2013/07-2013/05_biatec13-7_resovsky_EN.pdf)) would be a good way to demonstrate this fancy new widget.  We’ll grab the currency data from FRED using quantmod code from this old post [Eigen-who?](http://timelyportfolio.blogspot.com/2011/05/eigen-who-how-can-i-write-about-eigen.html).

*Code*

```
 # get MST using code from this post
#   https://mktstk.wordpress.com/2015/01/03/minimum-spanning-trees-in-r/

library(quantmod)
# #get currency data from the FED FRED data series
Korea <- getSymbols("DEXKOUS",src="FRED",auto.assign=FALSE) #load Korea
Malaysia <- getSymbols("DEXMAUS",src="FRED",auto.assign=FALSE) #load Malaysia
Singapore <- getSymbols("DEXSIUS",src="FRED",auto.assign=FALSE) #load Singapore
Taiwan <- getSymbols("DEXTAUS",src="FRED",auto.assign=FALSE) #load Taiwan
China <- getSymbols("DEXCHUS",src="FRED",auto.assign=FALSE) #load China
Japan <- getSymbols("DEXJPUS",src="FRED",auto.assign=FALSE) #load Japan
Thailand <- getSymbols("DEXTHUS",src="FRED",auto.assign=FALSE) #load Thailand
Brazil <- getSymbols("DEXBZUS",src="FRED",auto.assign=FALSE) #load Brazil
Mexico <- getSymbols("DEXMXUS",src="FRED",auto.assign=FALSE) #load Mexico
India <- getSymbols("DEXINUS",src="FRED",auto.assign=FALSE) #load India
USDOther <- getSymbols("DTWEXO",src="FRED",auto.assign=FALSE) #load US Dollar Other Trading Partners
USDBroad <- getSymbols("DTWEXB",src="FRED",auto.assign=FALSE) #load US Dollar Broad
#combine all the currencies into one big currency xts
currencies<-merge(Korea, Malaysia, Singapore, Taiwan,
                  China, Japan, Thailand, Brazil, Mexico, India,
                  USDOther, USDBroad)

currencies<-na.omit(currencies)

colnames(currencies)<-c("Korea", "Malaysia", "Singapore", "Taiwan",
                        "China", "Japan", "Thailand", "Brazil", "Mexico", "India",
                        "USDOther", "USDBroad")
#get daily percent changes
currencies <- currencies/lag(currencies)-1  
currencies[1,] <- 0

cor.distance <- cor(currencies)
corrplot::corrplot(cor.distance)

library(igraph)
g1 <- graph.adjacency(cor.distance, weighted = T, mode = "undirected", add.colnames = "label")
mst <- minimum.spanning.tree(g1)
plot(mst)

library(visNetwork)
mst_df <- get.data.frame( mst, what = "both" )
visNetwork( 
  data.frame(
    id = 1:nrow(mst_df$vertices) 
    ,label = mst_df$vertices
  )
  , mst_df$edges
) %>%
  visOptions( highlightNearest = TRUE, navigation = T ) 

```