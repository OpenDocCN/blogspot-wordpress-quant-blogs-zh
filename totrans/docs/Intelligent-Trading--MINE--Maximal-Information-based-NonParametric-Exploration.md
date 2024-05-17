<!--yml
category: 未分类
date: 2024-05-18 04:44:21
-->

# Intelligent Trading: MINE: Maximal Information-based NonParametric Exploration

> 来源：[http://intelligenttradingtech.blogspot.com/2012/01/there-was-lot-of-buzz-in-blogosphere-as.html#0001-01-01](http://intelligenttradingtech.blogspot.com/2012/01/there-was-lot-of-buzz-in-blogosphere-as.html#0001-01-01)

There was a lot of buzz in the blogosphere as well as the science community about a new family of algorithms that are able to find non-linear relationships over extremely large fields of data. What makes it particularly useful is that the measure(s) it uses are based upon mutual information rather than standard pearson's correlation type measures, which do not capture non-linear relationships well.

The (java based) software can be downloaded here: http://www.exploredata.net/ In addition, there is the capability to directly run the software from R.

 Fig 1\. Typical non-linear relationship exemplified by intermarket relationships.

The algorithm seems promising as it would allow us to possibly mine very large data sets (such as financial intermarket relationships) and find potentially meaningful non-linear relationships. If we were to use the typical pearson's correlation measures, such relationships would show very small R^2 values, and thus be discarded as non significant relationships.

I decided to take it for a spin on an example of a non-linear example, taken from M. Katsanos' book on intermarket trading strategies (p 25\. fig 2.3). In figure 1, we can clearly see that the relationship between markets is non-linear, and thus the traditional linear fit returns a low R^2 value of .143 (red line), a loess fit is also shown in blue. After running the same data through MINE, the results returned in a .csv file, were...

MIC           (strength)    MIC-p^2          (nonlinearity)

0.16691002    0.62445            7.129283    -0.3777441

The MIC (Mutual Information Coefficient) of .167 was not much greater than theR^2 measure of .143 above. However, one of the mentions in the paper was that as the signal becomes more obscured by noise, the MIC will degrade comparably.

The next step would be too find some type of fit to minimize the noise component and make updated comparisons.

In order to show a better illustration of how useful it might be, I am attaching a screenshot of the reference material here.

Figure 2\. Reproduced from Fig 6\. 'www.sciencemag.org/cgi/content/full/334/6062/1518/DC1'

Notice the MIC Score measure outperforms other traditional methods on many non-linear structural relationships.

Here is the full R-Code to repeat the basic experiment.

###############################################

# MINE example from intelligenttradingtech.blogspot.com 1/31/2012

library(quantmod)

library(ggplot2)

getSymbols('^GSPC',src='yahoo',from='1992-01-07',to='2007-12-31')

getSymbols('^N225',src='yahoo',from='1992-01-07',to='2007-12-31')

sym_frame<-merge(GSPC[,6],N225[,6],all=FALSE)

names(sym_frame)<-c('GSPC','N225')

p<-qplot(N225, GSPC, data=data.frame(coredata(sym_frame)),

geom=c('point'), xlab='NIKKEI',ylab='S&P_500',main='S&P500 vs NIKKEI 1992-2007')

fit<-lm(GSPC~ N225, data=data.frame(coredata(sym_frame)))

summary(fit)

fitParam<-coef(fit)

p+geom_abline(intercept=fitParam[1], slope=fitParam[2],colour='red',size=2)+geom_smooth(method='loess',size=2,colour='blue')

### MINE results

library("rJava")

setwd('/home/self/Desktop/MINE/')

write.csv(data.frame(coredata(sym_frame)),file="GSPC_N225.csv",row.names=FALSE)

source("MINE.r")

MINE("GSPC_N225.csv","all.pairs")

##########################################################

The referenced paper is, "Detecting Novel Associations in Large Data Sets"

David N. Reshef, et al.

Science 334, 1518 (2011)

As an aside, I've been hooked on a sitcom series called, "Numb3rs," playing on Amazon Prime. It's about an FBI agent who gets assistance from his genius brother, a professor of Mathematics at a prestigious University. So far, they've discussed markov chains, bayesian statistics, data mining, econometrics, heat maps, and a host of other similar concepts applied to forensics.