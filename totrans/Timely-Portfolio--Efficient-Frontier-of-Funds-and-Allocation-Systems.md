<!--yml
category: 未分类
date: 2024-05-18 15:07:28
-->

# Timely Portfolio: Efficient Frontier of Funds and Allocation Systems

> 来源：[http://timelyportfolio.blogspot.com/2012/04/efficient-frontier-of-funds-and.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/04/efficient-frontier-of-funds-and.html#0001-01-01)

I did a very basic experiment in [Efficient Frontier of Buy-Hold and Tactical System](http://timelyportfolio.blogspot.com/2011/10/efficient-frontier-of-buy-hold-and.html) where I determined the efficient frontier of the S&P 500 with itself transformed by a [Mebane Faber](http://www.mebanefaber.com/) 10-month moving average tactical allocation.

The result was interesting, but I did not pursue further.  Now with some inspiration and tools by [Systematic Investor](http://systematicinvestor.wordpress.com/), I thought I would extend the post. This time around we will use both the Vanguard U.S. Total Bond Market (VBMFX) and Vanguard U.S. S&P 500 (VFINX) combined with both portfolios determined by tactical methods (moving average, RSI, and omega) and those funds transformed individually by the same tactical methods.  I will as always warn you that this is not advice and large losses are almost guaranteed.  Also, I would like to note that I have checked the 10-month moving average every way possible (even manually in Excel), and it has been incredible on the VFINX since 1990.  Prior to 1990, results were good but nowhere near as amazing.  If I messed up, please let me know.

[R code from GIST:](https://gist.github.com/2416288)