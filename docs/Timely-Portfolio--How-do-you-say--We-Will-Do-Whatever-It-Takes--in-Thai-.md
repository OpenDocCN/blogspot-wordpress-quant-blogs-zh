```yml

category: 未分类

date: 2024-05-18 15:04:43

As the market has already started

# Timely Portfolio: How do you say “We Will Do Whatever It Takes” in Thai?

> 来源：[`timelyportfolio.blogspot.com/2012/08/how-do-you-say-we-will-do-whatever-it.html#0001-01-01`](http://timelyportfolio.blogspot.com/2012/08/how-do-you-say-we-will-do-whatever-it.html#0001-01-01)

```require(quantmod)

> #### **Too soon to crow**
> #### 
> 即使泰国的麻烦是地区级别的，其邻国仍然有理由担心对泰铢的成功攻击的连锁反应。现在，泰国还在为战胜投机者而欢呼。Amnuay 先生甚至承诺将利率（为了保护泰铢而保持高位）在今年降低两个百分点。仿佛一个小个子在与大个子恶霸打了一轮之后，还在挥舞着拳头跳舞，说：“来吧，再打我一次。”
> 
> ```They almost certainly will.** The defence of the baht was achieved by a series of extraordinary measures that will be hard to sustain…”

```panel.xyplot(x,y,...)

```

要查看整个**经济学人**在此期间关于泰国的文章，请访问[`www.economist.com/topics/thailand-1?page=33&%2524Version=0&%2524Path=%252F&%2524Domain=.economist.com`](http://www.economist.com/topics/thailand-1?page=33&%2524Version=0&%2524Path=%252F&%2524Domain=.economist.com)“http://www.economist.com/topics/thailand-1?page=33&%2524Version=0&%2524Path=%252F&%2524Domain=.economist.com"). 此外，请阅读 1997 年危机的非常详尽的描述[The Nation 博客](http://blog.nationmultimedia.com/search_blog_index.php?keyword=mini+series)**.**

If throughout financial market history, the central banks and politicians ever defeated the markets (greedy speculators), please let me know. 我对中央银行和政客的信心感到非常惊讶，尤其是在美国。

R 代码：

DEXTHUS <- 1/DEXTHUS["1995-01-01::1999-12-31",]

```

```require(latticeExtra)

A little graphical perspective might help us remember when this article was written.

```

![image](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhjfeX_8Qdk3Ia3JcxHsIMv_MfHr8k7FpGRRFjcvBmKZt6-wW-HoQRuyuVm2Nst_Thsvjamw6RQGqophT7LAfoQ3qdDTKQaNJHVq6rL2NHjJ4Y58ubDCK6uSSUGnfdPSvtMDkBAxF-JJw/s1600-h/image%25255B13%25255D.png)

asTheEconomist(

`xyplot(DEXTHUS,

```panel = function (x,y,...) {

```#plot Thai baht

panel.abline(v=index(DEXTHUS)[which(index(DEXTHUS)=="1997-05-22")],col="black", lty=3)

面板.文本(x=指数(DEXTHUS)[which(指数(DEXTHUS)=="1997-05-22")], y = 0.025, 标签="经济学人文章 泰铢泛滥", 颜色="indianred4", 角度=90, 位置=3)

},

主标题 = "危机前后的泰铢 (1995-1999) \n 来源：圣路易斯联邦储备银行"

)
