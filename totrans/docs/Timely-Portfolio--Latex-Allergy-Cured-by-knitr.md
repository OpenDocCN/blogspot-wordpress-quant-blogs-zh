<!--yml
category: 未分类
date: 2024-05-18 15:07:48
-->

# Timely Portfolio: Latex Allergy Cured by knitr

> 来源：[http://timelyportfolio.blogspot.com/2012/04/latex-allergy-cured-by-knitr.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/04/latex-allergy-cured-by-knitr.html#0001-01-01)

I have always known that at some point I would have to succumb to the power of Latex, but Latex has been uncharacteristically intimidating to me.  I finally found the remedy to my Latex allergy with the amazing and fantastic [knitr package](http://yihui.name/knitr/) from Yihui Xie.  With very minimal effort, I ran my first experiment and now am extremely excited to incorporate it in production-quality performance reports (I plan to document the steps to get there in future posts).

For those starting from scratch on Windows, I think the easiest method to get up and running is to [install LyX](http://wiki.lyx.org/Windows/Windows), which will also install [MikTex](http://www.miktex.org/).  If these are successfully installed, then you should be ready to experiment with knitr in R.

I will use knitr’s stich function, which is clearly not designed for the robust production use of knitr, but makes for a very easy first test.  stitch will open a very short script, apply a template, and generate a Sweave style .Rnw (can be changed).  knit2pdf converts the .Rnw file into a pdf, and with a couple lines of code you get [a remarkable result](http://www.box.com/shared/fdcc4483e733f9b00c44).

<embed src="http://www.box.com/embed/i2ho666gmcn6dt4.swf" wmode="opaque" type="application/x-shockwave-flash" allowfullscreen="true" allowscriptaccess="always">

[R code from GIST (unbelievably only 7 lines):](https://gist.github.com/2362469)