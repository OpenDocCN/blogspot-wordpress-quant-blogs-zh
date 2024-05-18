<!--yml
category: 未分类
date: 2024-05-18 13:50:11
-->

# In R: Cross Sectional Volatility | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/03/07/code-r-cross-sectional-volatility/#0001-01-01](https://quantivity.wordpress.com/2011/03/07/code-r-cross-sectional-volatility/#0001-01-01)

Readers of [Cross Sectional Volatility](https://quantivity.wordpress.com/2011/03/02/cross-sectional-volatility/) raised numerous questions on implementing the trading signal derived from *cross sectional volatility*. Towards exploring and visualizing these questions, an implementation in R is considered here.

Begin by assuming a frame exists named `ret` which contains a sequence of log returns (columns are stocks, rows are seconds), measured at second intervals, with ![T + H](img/a61cc2d72b56252da0da844f585fe5b2.png) observations. Define values for the key model constants:

```

N <- 5		# number of stocks
T <- 50		# number of seconds in &quot;past&quot;
H <- 60		# number of seconds in &quot;future&quot;
k <- 4		# number of PCA eigenvectors to use

```

For simulation sake, suitable values drawn from a *normal distribution* can be constructed as:

```

ret <- data.frame(replicate(N, log(1 + rnorm(T + H)/100)))

```

Given returns in `ret`, construct ![X](img/794e4ed8a3c3c8bb8e8b00198c6103c8.png), ![M](img/eb44ec3c0dcc9f29a8750db07e9e5890.png), ![Y](img/63e7cd04349f08d31d7afd3b8ec5de33.png), per p. 26; `X` is the “past” returns over which principal components are calculated, with length `T` (![T \times N](img/04699d8fef8f326b1523370f8a7b6af4.png)); `future` are the “future” returns over which prediction is generated, with length `H` (![H \times N](img/68274602cb2e85fd06e76c4393e0089f.png)); `M` is the average return for each stock (![1 \times N](img/7cba92d9ea69bb7d44af635616443025.png)), and `Y` is the de-meaned “past” (![T \times N](img/04699d8fef8f326b1523370f8a7b6af4.png)):

```

N <- length(ret)
X <- as.matrix(ret[1:T,])
future <- ret[(T+1):(T+H),]
M <- colMeans(X)
Y <- scale(X, scale=FALSE)

```

Visualize log returns and cumulative log returns via plotting the following:

```

plot.ts(X)
par(mfrow=c(3,2))
for (i in c(1:N)) { 
  lab <- paste('X', i);
  plot(cumsum(X[,i]), type='l', main=lab, ylab='', xlab='') 
}

```

Providing charts which look like familiar medium-frequency equities:

Next, perform PCA and construct ![D ](img/9b99697119ba9275b05e5090634c55ee.png) from the top ![k](img/7881e4ad2e7a375a9b4dd9dea1f6a3ae.png) eigenvectors in ![\phi](img/2091dd12efe62f5560f0e90f96ef4889.png) projected onto ![Y](img/63e7cd04349f08d31d7afd3b8ec5de33.png), via [SVD](http://en.wikipedia.org/wiki/Singular_value_decomposition) (as proposed on p. 58). Recall the eigenvectors are *columns* in `rotation`, thus `[,c(1:k)]` selects the top-![k](img/7881e4ad2e7a375a9b4dd9dea1f6a3ae.png):

```

phi <- prcomp(X)$rotation[,c(1:k)]
D <- Y %*% phi

```

A `summary` on `prcomp(X)` reveals:

```
Importance of components:
                           PC1      PC2      PC3      PC4      PC5
Standard deviation     0.01137 0.009963 0.009274 0.008849 0.008132
Proportion of Variance 0.28177 0.216240 0.187370 0.170580 0.144040
Cumulative Proportion  0.28177 0.498010 0.685380 0.855960 1.000000 
```

Thus, the top ![k](img/7881e4ad2e7a375a9b4dd9dea1f6a3ae.png) principal components explain 85.6% of variance, leaving the remaining 14.4% to denoise.

Given ![D](img/fd6081407ca943a923c743cb5596009a.png), calculate the matrix of ![\beta](img/e59dd600f7eb22f952e355797bceba2e.png) (which is ![N \times k](img/96869c7cd44bcacf53c9d11dd5568a46.png)) from the long-horizon regressions for each stock, iterating the summation from ![(t + 1)](img/48b29450357e5785b5ad5b9aa729ff64.png) to ![(T + H)](img/6dcace480cda3b7eca82519f10209b1c.png), per p. 28 (which due to lacking rigor, has several possible interpretations):

```

B <- c()
for (i in c(1:N))    # iterate over stocks
{
  hsum <- future[1,i]
  Dsum <- D[T,]
  for (j in c(2:H))&nbsp;&nbsp;&nbsp;# generate rows by walking up the horizon
  {
    hsum <- rbind(hsum, sapply(data.frame(future[c(1:j),i]), sum))
    Dsum <- rbind(Dsum, sapply(data.frame(D[c((T-j+1):T),]), sum))
  }
  B <- cbind(B, lm(hsum ~ Dsum)$coefficient[c(1:k+1)])
}

```

Plot `hsum` and `Dsum` for a given stock:

[![](img/1d32657f76003fb7ba80dcfd1d5190fd.png "sums")](https://quantivity.wordpress.com/wp-content/uploads/2011/03/sums.png)

via:

```

par(mfrow=c(3,3))
plot(hsum, type='l')
for (i in c(1:k)) {
  lab=paste("Dsum[",i,"]");
  plot(Dsum[,i], type='l', ylab=lab)
}

```

And, OLS residuals for all N stocks (which exhibit serial correlation, but do look mostly stationary):

[![](img/3c2e446b3f3194b15b40f921ed7b9aa5.png "residuals")](https://quantivity.wordpress.com/wp-content/uploads/2011/03/residuals.png)

Generate accumulated estimated ![\hat{S}](img/4afbff9deffdcb0bb4f4d4a5716de7f4.png) and actual returns ![R](img/e9185405078a808ad045a6921814a68b.png), using ![D](img/fd6081407ca943a923c743cb5596009a.png) and ![M](img/eb44ec3c0dcc9f29a8750db07e9e5890.png) (p. 29):

```

Dhat <- colSums(D[c((T-H):T),])
S <- Dhat %*% B
Shat <- as.vector(S + M)
R <- as.vector(colSums(future))

```

Where each is a vector, with *one accumulated horizon estimate per stock*. Inequality comparison of estimated and actual generates the trading signal:

```

signal <- R > Shat
cat('Shat:',  Shat, "\n")
cat('R:', R, "\n")
cat(ifelse(signal==TRUE, 'SELL', 'BUY'))

```

With results:

`Shat: 0.02340865 -0.00604718 -0.03142925 0.02960236 0.04318216
R: 0.04080749 -0.002699089 -0.05541317 0.02654577 0.04163165
Signal: SELL SELL BUY BUY BUY`

Thus, signal for the *current second*: sell short stocks 1 and 2; buy stocks 3, 4, and 5.