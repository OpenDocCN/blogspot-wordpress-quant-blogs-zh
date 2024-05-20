<!--yml
category: 未分类
date: 2024-05-18 04:44:56
-->

# Intelligent Trading: Can one beat a Random Walk-- IMPOSSIBLE (you say?)

> 来源：[http://intelligenttradingtech.blogspot.com/2011/03/can-one-beat-random-walk-impossible-you.html#0001-01-01](http://intelligenttradingtech.blogspot.com/2011/03/can-one-beat-random-walk-impossible-you.html#0001-01-01)

Firstly, apologies for the long absence as I've been busy with a few things.  Secondly, apologies for the horrific use of caps in the title (for the grammar monitors).  Certainly, you'll gain something useful from today's musing, as it's a pretty profound insight for most (was for me at the time). I've also considered carefully, whether or not to divulge this concept, but considering it's often overlooked and in the public literature (I'll even share a source), I decided to discuss it.

Fig 1\. Random Walk and the 75% rule

I've seen the same debate launched over and over on various chat boards, which concerns the impossibility of theoretically beating a random walk.  In this case, I am giving you the code to determine the answer yourself.

The requirements: 1) the generated data must be from an IID gaussian distribution 2) series must be coaxed to a stationary form.

The following script will generate a random series of data and follow the so called 75% rule which says,

Pr[Price>Price(n-1) & Price(n-1) < Price_median] Or [Price < Price(n-1) & Price(n-1) > Price_median] = 75%.  This very insightful rule (which is explained both mathematically and in layman's terms in the book 'Statistical Arbitrage' linked on the amazon box to the right), shows that given some stationary, IID, random sequence that has an underlying Gaussian distribution, the above rule set can be shown to converge to a correct prediction rate of 75%!

Now, we all know that market data is not Gaussian (nor is it commision/slippage/friction free), and therein lies the rub. But hopefully, it gives you some food for thought as well as a bit of knowledge to retort, when you hear the debates about impossibilities of beating a random walk.

R Code is below.

##################################################

#gen rnd seq for 75% RULE

#generate stationary rw time series

rw<-rnorm(100)

m<-median(rw)

trade<-rep(0,length(rw))

for(i in 1:(length(rw)-1)){

if(rw[i] < m) trade[i]<- (rw[i+1]-rw[i])

if(rw[i] > m) trade[i]<- (rw[i]-rw[i+1])

if(rw[i] == m) trade[i]<- 0}

eq_curve<-cumsum(trade)

par(mfrow=c(2,1))

plot(rw,type='l',main='random walk')

plot(eq_curve,type='l',main='eq_curve')