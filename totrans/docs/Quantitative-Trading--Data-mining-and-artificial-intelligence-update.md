<!--yml
category: 未分类
date: 2024-05-12 19:03:28
-->

# Quantitative Trading: Data mining and artificial intelligence update

> 来源：[http://epchan.blogspot.com/2010/10/data-mining-and-artificial-intelligence.html#0001-01-01](http://epchan.blogspot.com/2010/10/data-mining-and-artificial-intelligence.html#0001-01-01)

Long time readers of this blog know that I haven't found

[data mining or artificial intelligence](http://epchan.blogspot.com/2006/12/artificial-intelligence-and-stock.html)

techniques to be very useful for my own trading, for they typically overfit to non-recurring past patterns. (Not surprisingly, they are much more useful for

[driverless cars](http://www.nytimes.com/2010/10/10/science/10google.html)

.) Nevertheless, one must keep an open mind and continues to keep tabs on new developments in this field.

To this end,

[here](http://www.eecs.berkeley.edu/Pubs/TechRpts/2010/EECS-2010-63.pdf)

is a new paper written by an engineering student at UC Berkeley which uses "support

vector machine" together with 10 simple technical indicators to predict the SPX index, purportedly with 60% accuracy. If one includes an additional indicator which measures the number of news articles on a stock in the previous day, then the accuracy supposedly goes up to 70%.

I did not have the chance to reproduce and verify this result yet, but I invite you to try it out and share your findings here. If you do so, you may find this new data mining product called

[11Ants Analytics](http://www.11antsanalytics.com/)

useful. It is an Excel-based software that includes

[11 machine learning algorithms](http://www.11antsanalytics.com/aboutus/uth.aspx)

including the aforementioned support vector machines. It also includes decision trees which are sometimes quite useful in automatically generating a small set of trading rules from an input set of technical indicators. (Whether those rules remain profitable in the future is another question!) If you have tried this product, I would also appreciate your comments here.

(If you are a die-hard MATLAB fan, support vector machines are available in their Bioinformatics Toolbox, and classification and decision trees in their Statistics Toolbox.)