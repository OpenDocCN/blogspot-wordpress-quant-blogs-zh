<!--yml
category: 未分类
date: 2024-05-18 13:57:31
-->

# How many times are expected to try all songs in your itune library? | NaN Quantitavity - Quant Trading, Statistical Learning, Coding and Brainstorming

> 来源：[https://quantlife.wordpress.com/2013/03/20/how-many-times-are-expected-to-try-all-songs-in-your-itune-library/#0001-01-01](https://quantlife.wordpress.com/2013/03/20/how-many-times-are-expected-to-try-all-songs-in-your-itune-library/#0001-01-01)

### How many times are expected to try all songs in your itune library?

Today, when I was very boring with all my songs in iphone libary, I suddenly thought about one quick but useful math puzzle: assuming the iphone library has 100 songs and you use random shuffle (with re-sample) for next song, how many times are expected to listen all these songs?

This is very similar as the classical [Coupon Collection](http://en.wikipedia.org/wiki/Coupon_collector's_problem) problem. Here is a quick dirty R simulations, with two plots in regular scale and log scale:

N.songs = 100
temp <- function(N.songs){
return ( sum(N.songs/(1:N.songs)) )
}

x <- 1:N.songs
y <- sapply(x,temp)

par(mfrow=c(1,2))
plot(x,y,type=’l’,col=3, lty=2, lwd=2,log =’x’, xlab=’Number of New Songs’, ylab = “# Trials Needed”)
plot(x,y,type=’l’,col=3, lty=2, lwd=2, xlab=’Number of New Songs’, ylab = “# Trials Needed”)

![songs](img/4b13d3d25644e2e3953ea6a1c10ee776.png)

No comments yet.