<!--yml

分类：未分类

日期：2024-05-18 13:57:31

-->

# 在您的 itunes 库中，预计尝试所有歌曲多少次？| NaN 数量 - 数量交易，统计学习，编程和头脑风暴

> 来源：[`quantlife.wordpress.com/2013/03/20/how-many-times-are-expected-to-try-all-songs-in-your-itune-library/#0001-01-01`](https://quantlife.wordpress.com/2013/03/20/how-many-times-are-expected-to-try-all-songs-in-your-itune-library/#0001-01-01)

### 在您的 itunes 库中，预计尝试所有歌曲多少次？

今天，当我对 iphone 音乐库中的所有歌曲感到非常无聊时，我突然想到一个快速但有用的数学难题：假设 iphone 库中有 100 首歌曲，你使用随机播放（重新取样）下一首歌，预计需要听多少次才能听完所有这些歌曲？

这与经典的[优惠券收集](http://en.wikipedia.org/wiki/Coupon_collector's_problem)问题非常相似。这是一个快速而简单的 R 模拟，包括两个常规比例和对数比例的图表：

N.songs = 100

temp <- function(N.songs){

return ( sum(N.songs/(1:N.songs)) )

}

x <- 1:N.songs

y <- sapply(x,temp)

par(mfrow=c(1,2))

plot(x,y,type=’l’,col=3, lty=2, lwd=2,log =’x’, xlab=’新增歌曲数量’, ylab = “所需尝试次数”)

plot(x,y,type=’l’,col=3, lty=2, lwd=2, xlab=’新增歌曲数量’, ylab = “所需尝试次数”)

![songs

暂无评论。
