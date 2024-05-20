<!--yml
category: 未分类
date: 2024-05-12 19:51:14
-->

# The power of R: curve fitting | Coding the markets

> 来源：[https://etrading.wordpress.com/2006/08/15/the-power-of-r-curve-fitting/#0001-01-01](https://etrading.wordpress.com/2006/08/15/the-power-of-r-curve-fitting/#0001-01-01)

## The power of R: curve fitting

### August 15, 2006

I’ve got a bunch of XY cartesian coords that I want to plot. When charted the curves are jagged. Fortunately, each point has an associated weight – the number of observations used to create it. So how do I fit a curve to the data, using the weights to smooth and reduce the influence of the outlying points resulting from fewer observations ?

With R, it’s easy…

# x,y define straight line at 45%
x <- 0:19
y <- 0:19

# make the line jagged by shifting points
# [down,no move, up] in a repeating group of 3
y <- y + (-1:1)
plot(x,y,type=’b’)# generate vector of weights that give more
# weight to the unshifted points
w <- rep(0,20)
w <- w + c(1,3,1)

# reconstruct the unshifted straight line
f <- glm.fit(x,y,w)
lines(x,f$fitted.values)