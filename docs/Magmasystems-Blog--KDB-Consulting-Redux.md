<!--yml

分类：未分类

日期：2024-05-18 05:04:14

-->

# Magmasystems Blog: KDB 咨询重生

> 来源：[`magmasystems.blogspot.com/2008/01/kdb-consulting-redux.html#0001-01-01`](http://magmasystems.blogspot.com/2008/01/kdb-consulting-redux.html#0001-01-01)

在过去几周里，我收到了一些私人邮件，人们对我在博客上关于 KDB+的帖子感到好奇，想知道如何成为 KDB+顾问。或许成为一名心脏病专家更容易，而不是自学成为一名 KDB 咨询师。

我当然不会把自己当成职业顾问。你不应该期待我能为你打开未来的财富之门。我所做的一切就是观察市场。我经常为我们的需求招聘人员，并且经常有招聘人员给我打电话。我在华尔街和金融城有很多同事。因此，我能收集到很多不同的数据点，其中一些我会在这个博客上分享。

关于 KDB+，你能找到的一切信息都要谷歌一下。向 KX Systems 申请访问编码区域。获取 Jeff Borror 所著的《Q for Mortals》一书的副本。在你公司找到 KDB 社区的成员，请他们解释他们的源代码给你听。

如果你读到这里……

你需要获取一份 KDB+的副本，这并不容易。很可能，你不能上 LimeWire 或 Kazaa 找到一份 KDB 的副本。即使你找到了，你还需要找到一个许可证密钥。

你需要去[这里](http://www.kx.com/developers/software.php)，思考如何说服 Niall Dalton 或 Simon Garland 让你试试 KDB。或者，等待下一届 SIFMA 会议，找到 KDB 展位，提出带 KDB 团队去希尔顿酒店的大堂酒吧。或者，开发一个可能与 KDB 互补的产品（就像 Panopticon 那样），并试图向 Simon 展示它将提高 KDB 的普及度。也许是一个英文字符串到 Q 语言的翻译器？也许是一个真正的 KDB ODBC 驱动程序？也许是一个 Q 代码混淆器？

另一条途径是尝试接近第一导数。他们是 KX 系统的首要合作伙伴，相当于 KX 系统的阴阳面。暗示：他们喜欢 Guinness 啤酒。

如果你认为我在针对 KDB……同样的情况也适用于任何利基产品。我想你不可能有一天醒来决定成为一名 Vhayu 咨询师。为了专注于任何一种利基产品，你需要利用该产品的现有资源。这是在大型金融机构或大型专业提供金融服务的大型咨询公司工作的一个优势。

你需要进入正确的心态来处理 KDB。它是一个非常简约的产品，手动调整，处理实时买卖流数据的速度极快。实际的 Q.exe 引擎大约是一个 150K 的文件。你没有得到像 SQL Server 和 Oracle 这样的东西那样的舒适膨胀。使用 KDB 会让你回到写 DOS TSR 的日子，使用古老的 INT 21H（对于 80 年代后出生的人来说，TSR 是一个终止并常驻的程序……DOS 是一个古老的操作系统，让微软赚了很多钱）。

仿佛你还没有完全信服……以下代码来自一个名为 holiday.q 的 Q 文件。一旦你理解了这段代码，就给 KX Systems 的 Niall 或 Simon，或者 First Derivatives 的人发送电子邮件，向他们展示你可以不看任何东西就能编写这种东西（这还是温和的……等你接触到更有趣的东西再看）。

`/day:(day;year)

dy:{"D"$string[y],x}

/residue

r:{y-x*y div x}

/adjust sat/sun

a:{d+0^(x,1)r[7]d:dy[y]z}

/goto dayofweek

b:{d+r[7]x-d:dy[y]z}

/good friday(1900-2099)

g:{d+:e:r7+5+2*r[4;x]+2*r[7]x;dy["0320";x]+d-7*(d=35)(d=34)&(e=6)&a>10}

/nyse holidays

nyse:(a[2]"0101";b[2]"0115";b[2]"0215";g;b[2]"0525";a[-1]"0704";b[2]"0901";b[5]"1122";a[-1]"1225")

nyse@/:\:2007 2008`

©2008 Marc Adler - All Rights Reserved
