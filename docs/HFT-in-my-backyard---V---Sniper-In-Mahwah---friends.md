<!--yml

category: 未分类

date: 2024-05-18 14:17:02

-->

# 我后院的高频交易 | V - 马瓦狙击手及其朋友们

> 来源：[`sniperinmahwah.wordpress.com/2015/01/14/hft-in-my-backyard-v/#0001-01-01`](https://sniperinmahwah.wordpress.com/2015/01/14/hft-in-my-backyard-v/#0001-01-01)

是时候结束“我的后院的高频交易”系列了。上周在我周围都很紧张，我觉得有时候保持沉默是件好事。而且，这篇第五部分关于数据传输的过去和未来需要一些时间来完成 - 我发现了太多有趣的数据。我觉得我可以写一本新书的续集（那会很有趣）；话虽如此，我只会总结自去年九月以来积累的东西。 （*后记*：我将在一月份晚些时候发布系列的最后一部分，题为“杂项”，那里我将修改一些不准确的事实，并尝试回答我被问到的一些问题 - 至少，我会尽力，因为我并不知道所有的答案。）让我们从一点历史开始。

**介绍：军备竞赛和信息传输**

这是一个众所周知的故事：1815 年，英国银行家内森·梅耶·罗斯柴尔德用信鸽成为第一个知道滑铁卢战役结束的人。信鸽轻易地穿过了海峡（它们不会因为水的反射而产生问题），到达伦敦，告诉罗斯柴尔德拿破仑的失败，因此这位银行家“[通过购买英国政府债券捞了一把](http://www.ft.com/intl/cms/s/0/255b75e0-c77d-11e2-be27-00144feab7de.html#axzz3NwLg99JT)”。官方故事说罗斯柴尔德赚了一大笔钱是因为他有最快的传输技术（信鸽），但这并不是真的：故事的另一部分（几乎不为人知）是拿破仑拥有比鸽子更快的技术：**夏蒂信号**。简而言之，这个由[克洛德·夏蒂](http://en.wikipedia.org/wiki/Claude_Chappe)发明的“光学”或“空中”网络利用各种信号台去传输信息遍布整个法国：

![克洛德·夏佩的光学网络](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/chappe.jpg)这些网络在当时属于“光学”网络，因为用于点对点通信的信号塔需要具有视线（就像今天的微波网络一样）；这也解释了为什么这些信号塔都建在已有的高处（比如山峰）或者建在独立的塔上。拿破仑的军队是夏佩的狂热客户，皇帝还投入了资金到这个网络，所以滑铁卢惨败的消息应该*先于*伦敦抵达巴黎。但罗斯柴尔德的信鸽赢了比赛。为什么？雾！1815 年 6 月 18 日，在滑铁卢，雾很浓，以至于拿破仑的士兵感到不安，而夏佩网络完全瘫痪：因为雾太大，从滑铁卢发送的信号根本无法传到法国北部的信号塔——你什么都看不见。这是一个了不起的故事，因为两个世纪后，在滑铁卢惨败之后，雾对于新的 HFT（微波）网络仍然是一个问题。技术或许变了，但自然依然如故。

一场战争的结果一直是一个延迟问题。格雷格·劳克林，曾[研究](http://arxiv.org/abs/1302.5966)纽约和芝加哥间最新的信息传输（从光纤到微波），在[博客](http://oklo.org/2014/11/28/optical-data-transmission/)上谈到了一次古老而神秘的光学数据传输：“*特洛伊战败的消息在一夜之间传到了斯巴达的克吕泰涅斯特拉*”。在伊斯库罗斯的《阿伽门农》中，有这样的描述：“*山顶的赫菲斯托斯，火之主，/ 发出信号；回荡，回荡，/ 信号之火从山顶到具有赫尔墨斯之名的雷姆诺斯，/ 再到宙斯的宝座，这个巍峨的高地的广告一样灿烂*”，等等。信号是火焰，因为伊斯库罗斯列出了“信号站”的名字，格雷格[成功](http://people.seas.harvard.edu/~jones/history/comm_chron1.html) 绘制了特洛伊到迈锡尼的 600 公里网络地图：

![截屏 2015-01-11 09.38.17](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-11-c3a0-09-38-17.png)

最长路径是 177 公里（从著名的阿索斯山到坎迪利翁），地势高于海平面，而且大部分信号站都位于山上或高地上。如果你放大观察耶拉涅亚山，你猜到那里能看到什么吗？一个美丽的新的金属塔：

![截屏 2015-01-13 09.57.26](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-13-c3a0-09-57-26.png)

再次，技术可能会改变，但它们仍然必须使用自然界的相同特征。“*就在迈锡尼遗址外面，这个风景看上去好像在 3,000 年里没什么变化。我认为这张谷歌地球截图…*”

[![屏幕截图 2015-01-11 上午 10.34.07](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/screen-shot-2015-01-11-at-10-34-07-am.png)](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/screen-shot-2015-01-11-at-10-34-07-am.png)

* …（就在遗迹外面，朝向阿拉克涅峰的大致方向），细微却又肯定的印证了古老的希腊理想 – 传递到罗马，再到启蒙时代，再到信息革命，最后到谷歌地图相机的阴影*” ，Laughlin 补充道。“*鉴于消息只有一个比特，信号编码正好在香农极限之内*”。

##### **过去的我：霍特姆，从美国陆军到跳跃交易**

让我们开始着手调查现在（或不久之后）HFT 公司在伦敦（斯劳/巴西尔登）和法兰克福之间使用的微波网络的原因。这个[Bloomberg 文章](http://www.bloomberg.com/news/2014-07-15/wall-street-grabs-nato-towers-in-traders-speed-of-light-quest.html)就是我调查的导火索，标题为“华尔街购买北约微波塔，追求速度” – 这里的“华尔街”指的是“[Jump Trading LLC](http://www.jumptrading.com)”中的一个最大的芝加哥市场制造商，他们购买了比利时霍特姆的这座高塔。这座塔再次出现了（有关细节请阅读[第二部分](https://sniperinmahwah.wordpress.com/2014/09/25/hft-in-my-backyard-ii/)）：

[![](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-05-c3a0-10-45-37.png)]

在开始寻找欧洲高频世界中其他的塔来绘制地图之前，我核实了这座塔的历史，很快意识到这座拉线塔不是由或为北约建造（即使北约也不远）。彭博社在文章中提到“*美国武装部队*”是正确的，因为这座塔是美国军队在欧洲建造的旧微波网络故事的一部分。试图总结军事网络的历史不是一件容易的事情（因为所谓的“国防保密”，但故事的开端可能是 1963 年 4 月 19 日的这份“[美利坚合众国政府和比利时政府关于某些通信设施的协议](https://books.google.be/books?id=6peOAAAAMAAJ&pg=PA415&lpg=PA415&dq=flobecq+agreement+between+the+government+of+the+united+states+and+the+government+of+Belgium+communications&source=bl&ots=OSJlUegCH7&sig=JcIQba3BYr4jAfR-tzkM-WiX2yY&hl=fr&sa=X&ei=mJOrVP_fEoPxapW1gNAI&redir_esc=y#v=onepage&q=flobecq%20agreement%20between%20the%20government%20of%20the%20united%20states%20and%20the%20government%20of%20Belgium%20communications&f=false)”中提到。article 1 称：“*比利时政府授权，批准和确认美国政府在弗洛贝克和其他由美国和比利时当局现在或以后同意的场所建立、运营和维护通信设施*”。这意味着：从 1963 年开始，美国开始在欧洲建造不同的微波网络作为国防通信系统（DCS）的一部分。在这封协议中没有提到胡特姆塔，但弗洛贝克（比利时的一个小村庄）这个名字令人惊讶，因为在 2015 年，不同的高频交易竞争者（[Flow Traders](http://webcache.googleusercontent.com/search?q=cache:FYRvzAFt3wwJ:cadastreantenne.issep.be/Dossiers9/5354/RP1-RAP-12-03989-VAB.pdf+&cd=2&hl=fr&ct=clnk&client=safari), [Jump](http://cadastreantenne.issep.be/Dossiers8/5214/RP1-RAP-12-01777-BEP.pdf)，可能还有 Optiver）在这座旧军事塔上设置了天线：

![Capture d’écran 2015-01-06 à 09.07.09](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-06-c3a0-09-07-09.png)

国防通信系统在比利时、希腊、意大利、葡萄牙、西班牙、土耳其和英国设有设施，包括一种混合的微波无线电链路和卫星通信终端。这些网络并非是在几毫秒内建立的：感谢朱利安·阿桑奇（Julian Assange）和维基解密（Wikileaks），我们通过阅读这份解密的[cable](https://www.wikileaks.org/plusd/cables/1973BRUSSE01930_b.html)（1973 年 4 月 6 日的标题为*美国在比利时的微波系统*）得知：“*微波系统的原始完成目标日期为 1973 年 5 月，但我们了解到，合同目前正在经重新协商，以确立新的目标日期为 1973 年末或 1974 年初* […] *我们正在传递 1973 年 1 月 2 日日期的现场访问报告的副本，这份报告概述了六个比利时站点中六个站已完成的工作和剩下的工作（Houtem, Westrozebeke, Flobecq, Shape, Le Chenoi and Ben Ahin）*。” 这是对 Houtem 塔的首次提及。通过阅读[这个网站](http://usarmygermany.com/Units/USAFE%20Units/USAREUR_HqUSAFE%201.htm)，我们得知 DCS 网络的比利时部分从 1974 年中期起开始传输数据（这与其他数据表明，Houtem 塔是在 1973 年建成的）。

在 1989 年出版的书籍[*美国军队和驻欧洲设施*](https://books.google.be/books?id=dzKr3mSKyIgC&pg=PA16&dq=us+military+forces+and+installation+in+belgium&hl=fr&sa=X&ei=vZ2rVIqXDYfd7QaEtoDYDg&ved=0CCAQ6AEwAA#v=onepage&q=us%20military%20forces%20and%20installation%20in%20belgium&f=false)中，我们得知美国陆军在比利时有 19 个设施（军火库、办公室等），包括这三座塔：

![Capture d’écran 2015-01-06 à 09.27.52](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-06-c3a0-09-27-52.png)再深入挖掘一些，您可以找到一些关于 Flobecq 和 Houtem 塔与国防通信系统（Defense Communication System）的旧地图：

![Capture d’écran 2015-01-06 à 09.42.47](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-06-c3a0-09-42-47.png)

这些文件很有意思，因为我们可以将原本由 Jump 拥有的 Houtem 塔与与 Flow Traders 合作的 Flobecq 塔联系起来。您可以看到旧 DCS 网络的路径几乎与 HFT 公司从 Flobecq（比利时）到 Swingate（英国）使用的路径相同：

![Capture d’écran 2015-01-06 à 09.52.18](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-06-c3a0-09-52-18.png)

美国军方还管理着另一个名为“[欧洲波动散射](http://www.usarmygermany.com/Sont.htm?http&&&www.usarmygermany.com/Units/Signal/USAREUR_SignalCorps%20ETA.htm)”的微波网络。真是惊人，因为该网络的一部分从 Flobecq 到...法兰克福！这让我猜想德国的 HFT 塔，因为在这个国家没有关于它们的公开数据。我在地图上标志了波动散射路径（下图），并且我怀疑 1）如果 Custom Connect 路线是否通往 Prüm， 2）Simmerath 所有竞争对手（McKay, Jump, Vigilant, Optiver 和 Latent）通过 Weibern 塔经过后，是否都使用菲尔德贝格塔，离法兰克福的 Deutsche Bourse/Eurex 匹配引擎数据中心仅 20km。

![捕捉的屏幕截图 2015-01-13at10.43.32](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-13-c3a0-10-43-321.png)

在 Flobecq 的另一边，Houtem-Swingate 路线似乎引起了关注，因为穿越海峡是一项艰巨的任务（可能会有雾，必须处理水面反射等）。有至少三篇关于这些困难的学术文章发表，第一篇是 1979 年由国防技术信息中心出版的，*[Houtem-Swingate 链接的延迟线要求](http://books.google.be/books/about/Delay_Line_Requirements_for_Houtem_Swing.html?id=Qny2tgAACAAJ&redir_esc=y)。第二篇论文于 1979 年由美国商务部发布，*[5 GHz 微波链路穿越英吉利海峡的信号级分布和衰落事件分析*](http://permanent.access.gpo.gov/gpo29426/79-30_ocr.pdf)，描述了“*用于研究衰落和在英吉利海峡上 88km 多重多样性直射微波链路的测量结果，工作在 4-5 GHz 频率范围内”（现在 Jump 使用 7.470 Ghz 频率穿越海峡）。至少三篇旧的技术论文突出了微波路径穿越海峡的困难，这可能解释了我在[第四部分](https://sniperinmahwah.wordpress.com/2014/11/03/htf-in-my-backyard-iv/)中谈到的“*大量的猜测*”，当时 HFT 公司/供应商决定在 2012 年在欧洲建立他们的微波路径。

根据美国空军部 1996 年发布的这份[文件](http://nato.radioscanner.ru/files/article63/communications_elect.pdf)，DCS 网络从 1979 年开始进行升级，并成为数字欧洲骨干(DEB)：“DEB 项目用数字微波和大容量加密设备取代了意大利、德国、比利时、荷兰和英国 DCS 现有的模拟微波设备”。1988 年，“阶段 III 通过比利时将数字服务扩展到英国。这条连接还提供了数字通信系统形成四重信号消隔的连线，并提供了横跨英吉利海峡的连接”，这意味着 Houtem 塔在 1990 年代仍被美国军队使用。根据国防部发布的这份[文件](http://www.comw.org/qdr/basestructure1999.pdf)，1999 年所有比利时的塔仍被美国所有。但是 2006 年 1 月 20 日，国防部[宣布](http://www.defense.gov/Releases/Release.aspx?ReleaseID=9245)“决定停用并归还三个微波无线电站给比利时。这些站点分别是：Houtem，Westrozebeke 和 Flobecq。“由于 1996 年安装的无线电中继系统所提供的服务将被更高容量、更低成本的商业通信服务所取代”，即光纤电缆。“关闭这些站点预计每年可节省 84000 美元以上。”

2006 年，三座塔被归还比利时，但我的~~后院~~国家很快意识到它们的昂贵和无用。Westrozebeke 塔被摧毁；Flobecq 被比利时国防部使用，但由于这份[文件](http://ventderaison.eu/melles_mourcourt/eie_windforever_2014/etude_incidence.pdf)，我们知道无线电链路是在 2015 年 1 月 1 日的两周前关闭的；2012 年，比利时决定[出售](http://www.servicespatrimoniaux.be/interfpatrnl/Green/Immeubles/Brugge/BruggeVeurneReiger/BruggeVeurneReiger.html)状况不佳的 Houtem 塔。我在[第二部分](https://sniperinmahwah.wordpress.com/2014/09/25/hft-in-my-backyard-ii/)中谈到了剩下的故事：2012 年 12 月 18 日，在 Houtem 举行了一场史诗般的拍卖，比利时政府以 255,000 欧元的起拍价开始，但各种 HFT 公司/微波供应商都在竞争，最终 Jump Trading 以 500 万美元成交并于 2013 年 1 月购买了这座塔（至少再花费一百万重建设施）。这就是 1973 年美国军队在比利时竖立的一座古老的美国塔 40 年后被一家美国公司购买的方式。令人惊讶的细节是：军队归还了塔，因为新的光纤电缆在带宽方面更高效，后来这座塔被一家美国公司购买，因为微波与光纤相比在延迟方面更高效。这是多么讽刺啊？

##### **过去，II：美军-北约驻扎**

Houtem 塔从未由北约建造或拥有。话虽如此，它与北约存在联系。北大西洋公约组织还有各种无线电网络，主要的是“欧洲盟军高级指挥”（[ACE High](http://en.wikipedia.org/wiki/ACE_High)）。该网络建于 1956 年左右，并于 1980 年代末解除。以下是地图：

![ACE HIGH 地图](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/ace-high-map.jpg)

该网络从土耳其经法国和英国通往瑞典。但 1966 年，查尔斯·戴高乐“*[退出](http://www.dailymail.co.uk/news/article-1161642/As-France-rejoins-NATO-humorous-reminder-missed-them.html)北约军事同盟的核心，称加入北约军事指挥体系损害了法国独立和主权*”。这意味着无线电网络不能再使用法国的塔。于是，北约决定通过意大利、德国和比利时创建新路径，以便到达英国。这是 1966 年后使用的“备用/迁移路径”的地图（在下图中表示为蓝色和绿色）：

![2_2lx395yd](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/2_2lx395yd.jpg)

由于查尔斯·戴高乐，北约需要在比利时建造一座联通英吉利海峡的塔：这就是地图上的“BADZ”塔，位于 Adinkerke，距离 Houtem 塔 8 公里（它仍然矗立）：

![Capture d’écran 2015-01-06 à 13.07.27](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-06-c3a0-13-07-27.png)

关于北约网络的另一个惊人事实：[“空军微波中继网络”](http://cadastreantenne.issep.be/Dossiers8/5414/RP1-RAP-13-00197-BEP.pdf)中的一个子网络使用了比利时东部的 Baraque de Fraiture 塔。你能在 2015 年在这座塔上找到谁？是 HFT 微波提供商的天线。关于这些塔还有其他有趣的事情，但那会太长了。只需要注意的是，由于地缘政治原因，北约和美国陆军的网络都必须在蒙斯（比利时）连接。那里是北约的一个战略军事指挥中心——欧洲盟军最高司令部在法国退出北约后搬迁的地方。这种互联网络被称为… “*驻地共享*”;) 最后但同样重要的是：这两个网络都在土耳其结束，所以它们通过希腊。这就是 20 世纪微波网络（在下图中的绿色和蓝色）几乎与希腊山区的古老特洛伊-迈锡尼篝火网络相交的方式：

![Capture d’écran 2015-01-13 à 11.18.14](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-13-c3a0-11-18-14.png)

##### **过去，III：RAF 在英国**

关于英国皇家空军（RAF）和 Chain Home 雷达系统，历史将不完整。Chain Home 是英国在第二次世界大战前后建立的用于追踪德国飞机的网络（查看[地图](http://www.radarpages.co.uk/mob/images/map3l.jpg)）。最著名的塔楼可能是 1936 年建成的斯温盖特的“三姐妹”（这样一来，北约和美国军队网络在 60 至 70 年代才得以利用这些塔跨越海峡）。其中一座塔在 2010 年被拆除（因为变得不稳固），但在剩下的两座塔中，你可以找到一些 HFT 竞争者的天线，比如 McKay Brothers、Optiver 和 Jump Trading。多亏了豪滕架架，Jump 不再需要斯温盖特塔去到巴斯尔登 [参见[第二部分](https://sniperinmahwah.wordpress.com/2014/09/25/hft-in-my-backyard-ii/)]，但我敢打赌，这家芝加哥公司仍需要通过它向斯劳发出信号。

![Capture d’écran 2015-01-13 à 11.36.46](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-13-c3a0-11-36-46.png)

如果你想了解这些塔的历史，只需阅读 Jump Trading 在提交许可证时的[规划声明](http://planning.dover.gov.uk/online-applications/applicationDetails.do?activeTab=documents&keyVal=DCAPR_220195)。令人惊讶的是，Chain Home 网络从斯温盖特一直延伸到敦刻尔克……那里可以找到其他 HFT 公司（McKay、Latent、Optiver、Custom Connect）。因此（至少）两家公司，McKay Brothers 和 Optiver，使用的是 RAF 在 20 世纪 30 年代建立的准确的微波路线（关于 Custom Connect，请参阅这篇[文章](https://sniperinmahwah.wordpress.com/2014/12/04/hft-in-my-backyard-a-mystery-solved/)）。 

![Capture d’écran 2015-01-13 à 11.49.30](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-13-c3a0-11-49-301.png)

无论是斯温盖特塔还是敦刻尔克塔在英国都出了名。由于它们在第二次世界大战期间的作用，它们被列入了英格兰国家文物名录。现在这两座塔都是历史古迹，两家 HFT 公司，Custom Connect 和 Jump Trading，对历史缺少尊重，这是很遗憾的：我曾在[第三部分](https://sniperinmahwah.wordpress.com/2014/10/02/hft-in-my-backyard-iii/)中写过 Jump 就在提交规划申请之前就在斯温盖特安装了天线，“*本应在提交规划申请之前*”（他们自己的[话](http://planning.dover.gov.uk/online-applications/files/E997135014F4091378DD3AF44F29F01C/pdf/12_00732-PLANNING_STATEMENT-214045.pdf)）。后来我[发现](https://sniperinmahwah.wordpress.com/2014/10/06/hft-in-my-backyard-more-on-piracy/)，Custom Connect 在获得在敦刻尔克的许可之前已经安装了天线。正如一家 HFT 竞争对手告诉我的，“*在一座二战纪念碑上，这是一种重罪*”……

##### **未来，第一部分：海伯尼亚大西洋**

美国陆军，北约和英国皇家空军在 20 世纪下半叶设置了很多塔，这些塔现在被各种交易公司/微波提供商拥有的卫星接收器所占据。2006 年，$houtem_$塔被出售给了比利时，因为美国陆军发现了更好的技术：光纤电缆，但是有视线的微波塔发现了新的客户（高频交易者），因为延时比使用电缆更好。我试图找到一些存在于伦敦和法兰克福之间的光纤网络的地图（以便与微波路径进行比较），我甚至联络了一些网络提供商，但我得不到答复（“*商业机密*”）。我曾经在一个大型市场制造商的墙上看到一张显示伦敦光纤网络的大而详尽的地图，但我没有被授权拍照。通过 Google Images，你可以找到像[euNetworks](https://www.google.com/search?q=eunetworks+london+frankfurt&safe=off&client=safari&rls=en&source=lnms&tbm=isch&sa=X&ei=GiC2VNiVGefZ7Aat3IC4Ag&ved=0CA0Q_AUoAA&biw=1135&bih=919)这样提供商的“地图”，但这些图表过于简化。有一个例外:在[Zayo](http://www.zayo.com/solutions/financial-low-latency)网站上，你可以搜索这家公司管理的各个电缆网络。不用说，伦敦到法兰克福的路线远非一条直线：

![Zayo](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/zayo.jpg)

不同网路之间的互连被称为“*机房*”，让我们来看看英格兰南部康沃尔郡的机房。在那里，高频交易网络结束了它们的大陆线路，与越过大西洋所需的光纤电缆相遇。我在这个系列的之前部分犯了一个错误：那里不仅有*一条*电缆，而是*两条*，而且高频交易公司似乎不使用相同的电缆越过大西洋。

![Capture d’écran 2015-01-13 à 13.21.07](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-13-c3a0-13-21-07.png)

Jump 微波网络的最后一个设备位于“Skewjack”电缆登陆站。根据安德鲁·布卢姆（Andrew Blum）的这本精彩书籍*Tubes*，当地人称这个地方为“skewjack”，因为以前这个地点是冲浪者的露营地（阅读这篇有趣的[采访](http://www.theguardian.com/commentisfree/joris-luyendijk-banking-blog/2011/sep/15/computer-programmer-high-frequency-trading)了解冲浪者和高频交易算法之间的比较“*试图发现一波*”）。这个登陆站是 FLAG 大西洋 1（[FA-1](http://en.wikipedia.org/wiki/Fiber-Optic_Link_Around_the_Globe)）电缆的其中一个，由[Reliance](http://globalcloudxchange.com)所有。一个有趣的事实：请记住，名为 Perseus Telecom 的公司是欧洲不同高频交易公司的[微波提供商](http://www.bloomberg.com/news/2014-07-15/wall-street-grabs-nato-towers-in-traders-speed-of-light-quest.html)；Perseus 目前不拥有自己的网络，而是从 Jump 租赁带宽（参见[第二部分](https://sniperinmahwah.wordpress.com/2014/09/25/hft-in-my-backyard-ii/)），所以看到 Perseus 将 FA-1 电缆转售给他们的客户是有道理的 – 我并不是很清楚，但很可能 Perseus 的客户可能同时签约从法兰克福到康沃尔的微波网络 *和* 从康沃尔到美国的 FA-1 电缆。

Jump Trading 和 Perseus 之间的接近可能解释了为什么 Jump 的竞争对手（至少包括 Optiver 和 Vigilant）使用另一条电缆：大西洋穿越 1（[AC-1](http://en.wikipedia.org/wiki/Atlantic_Crossing_1)），“一个星球，一个网络”的*座右铭*。据说它比 FA-1 电缆更快。登陆站名为“Whitesands cable station”，你可以在 Andrew Blum 的*Tubes*中阅读有关该站点的描述，“*一个机架标记为 SLOUGH*” – 这是 Whitesands-Slough 电缆网络，但高频交易商对它已不再关心，因为他们已经使用微波，以节省两地之间的几毫秒。也就是说，康沃尔的这两个登陆站很可能在不久的将来成为历史。正如我在[第三部分](https://sniperinmahwah.wordpress.com/2014/10/02/hft-in-my-backyard-iii/)中写的那样，一条新的电缆正在英国和美国之间进行中：著名的 Hibernia 的[Project Express](http://www.hibernianetworks.com/project-express)。

海伯利亚是[金融界](http://www.hibernianetworks.com/hnservices/financial-markets/)的重要供应商 - 你可以在[这里](http://www.hibernianetworks.com/corp/wp-content/uploads/2014/07/HN-PoPs-11JUl14.pdf)找到他们光缆的不同出现点。AC-1 旧光缆提供了 65 毫秒的跨大西洋连接，但据说 Project Express 能够减少六毫秒的时间（这就是我书名为*6*的原因）。4600 公里的光缆原计划于 2012 年完工，但海伯利亚遇到了困难 - 其中主要问题是由于中国承包商华为的[网络安全](http://www.telecomramblings.com/2013/02/hibernias-express-buildout-suspended-due-to-huaweis-us-problems/)问题。Project Express 在 2013 年 7 月[重新回到正轨](http://www.telecomramblings.com/2014/07/hibernia-express-back-track/)，感谢[Herald Business](http://thechronicleherald.ca/business/1224651-continental-cable-connection)我们知道英国的着陆站在布里恩（顺便说一句，1 月初美国监管机构 FCC 批准 Hibernia LLC 的转让给名为 KCK Limited 的公司）。（着陆站不是新的，是为[另一条光缆](http://www.ofcom.org.uk/static/archive/fcc.htm)建造的。）所有使用微波加入康沃尔（Cornwall）的交易公司将会遇到一个小问题：布里恩不属于康沃尔，而是萨默塞特；这意味着所有从伦敦（或多弗/斯温盖特）到康沃尔的微波路径到某一点将会完全无用：

![before_after](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/before_after.jpg)

但我可能犯了另一个错误。业界的不同消息来源（以及一位记者）告诉我，海伯利亚（Hibernia）目前不会允许在布里恩着陆站设置天线。我努力想了解更多情况，但只得到了一些“*既不确认也不否认*”的回复。唉！人们知道但不说。我给海伯利亚写了封邮件，但明显得不到任何答复。然后其他消息来源告诉我，海伯利亚最终可能会允许放置天线……无论真相如何，正如我之前解释过的，不同的高频交易竞争对手已经预见到新的 Project Express 光缆，并在斯劳和布里恩之间的各个塔上预订了许可证/频率。我最终[找到了](https://www.google.com/fusiontables/DataSource?docid=1NOw4q4NeBGvNnM8_L2QoPZCsOoFUdAgLhk5QRQk#rows:id=1)Project Express 着陆站在[Brean](http://www.stevenheaton.co.uk/SubmarineCableLandingsUK/?p=198)看起来像这样的确切位置：

![Capture d’écran 2015-01-13 à 15.27.00](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-13-c3a0-15-27-00.png)

然后我回到了我的地图，多么令人惊讶… 猜猜在降落站的位置上拥有 Ofcom 牌照的是谁… 跳跃交易公司：

![Capture d’écran 2015-01-14 à 09.58.14](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/capture-d_c3a9cran-2015-01-14-c3a0-09-58-14.png)

Ofcom 的[牌照](http://spectruminfo.ofcom.org.uk/spectrumInfo/licences?googloc=(51.2860442329784%2c+-3.0130863189697266)&unit=GHz&ne=(51.286272378029565%2c+-3.012721538543701)&service=Fixed+Links&code=301010&se=(51.28581608679386%2c+-3.012721538543701)&googoffset=0.0&nw=(51.286272378029565%2c+-3.013451099395752)&sw=(51.28581608679386%2c+-3.013451099395752)&groupKey=1&licenceNum=0956280&submit=Find%20licence)于 2013 年 6 月 24 日获得，这是在项目快车因为华为而被[暂停](http://www.telecomramblings.com/2013/02/hibernias-express-buildout-suspended-due-to-huaweis-us-problems/)四个月后，也是在它[恢复](http://www.telecomramblings.com/2014/07/hibernia-express-back-track/)13 个月之前。这是一个有趣的时间节点。Hibernia 宣布新的电缆将于 2015 年 9 月可用。如果公司在那里允许装置，未来在欧洲的微波通信可能会围绕布里恩。拭目以待。

##### **未来 II：边缘云计算的终结？**

交易公司只需要通信网络，因为交易中心（匹配引擎）分布在世界各地。这就是为什么有些公司需要芝加哥和纽约之间的微波通信，或者伦敦和法兰克福之间的微波通信，欧洲和美国之间的光纤通信，或者美国和亚洲之间的光纤通信，等等。这都是关于地理位置的。在我书的结尾部分，我很快地讨论了一些与这些问题有关的理论文章，这篇文章由哈佛/麻省理工学院的亚历山大·威斯纳-格罗斯（Alexander Wissner-Gross）和卡梅伦·弗里尔（Cameron Freer）合著，标题为“[相对论统计套利](http://www.alexwg.org/publications/PhysRevE_82-056104.pdf)”，2010 年发表在*Physical Review*上。

我不会详细讨论统计套利（我将在我的下一系列文章中探索套利），本文有趣的地方在于空间和交易。简而言之：交易算法现在位于离交易所/撮合引擎非常近的位置（数据中心的共同位置），以便它们可以更快地执行订单（大约 200-500 微秒）；但数据*仍然*需要从一个交易所传输到另一个。 Wissner-Gross 和 Freer 试图想象一个世界，其中算法将安装在交易所之间的中间节点位置——*即*在最佳点或两个交易中心之间的中点。“*服务器可能安装在或接近计算的位置，使得信息传播的延迟在服务器和第一个交易中心之间实质上等于信息传播的延迟在计算位置和第一个交易中心之间*”。作者计算出了“*52 个主要交易所的所有配对的最佳位置（“节点”）*”，这里是这张地图上的蓝色，红点是交易所（请注意，该文章是在五年前发布的，自那时起，一些红点可能略有变化）：

![最佳交易地点](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/optimaltradinglocations.png)

我对想象交易服务器漂浮在海洋中感到非常感兴趣，所以我决定在我的书的封面上重新制作世界各地的水下光纤电缆*和*Wissner-Gross 和 Freer 的节点。 这是封面的欧洲部分：

![20140313_165439](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/20140313_165439.jpg)

“*请注意，虽然有些节点位于密集的光纤网络区域，但许多其他节点位于大洋或其他网络稀疏的区域，也许最终会激励在这些遥远但位置良好的位置部署低延迟交易基础设施*”，作者写道。当我在撰写这篇文章时，我意识到这项理论研究可能并不是那么理论性。事实上，2014 年 1 月 21 日，在美国，麻省理工学院提交了一项名为“相对统计证券交易系统和方法”的[专利](http://www.google.co.ug/patents/US8635133)，而“*发明者*”的姓名是亚历山大·Wissner-Gross 和卡梅隆·弗里尔。

这是对他们 2010 年文章的实用后续，里面有很多有关交易未来的细节。该系统可能包括一个处理器，该处理器根据通信链路的属性之一，计算服务器沿第一交易中心和第二交易中心之间的通信链路的位置*。*该系统将比合作站点更好：“*在两个交易中心之间的通信链路上放置服务器，方式减少分布式交易期间信息传播的延迟可能会使这样的交易更加频繁发生，并且可能允许高频分布式交易以比使用服务器与其中一个交易中心合作的常规方法速度更高的速度发生*”。以下是专利中的一个图表：

![Capture d’écran 2015-01-13 à 16.34.31](https://drive.google.com/viewerng/viewer?url=patentimages.storage.googleapis.com/pdfs/US8635133.pdf)

由于服务器 116 需要与交换所 102 和 108 进行通信，它们需要位于位置 108 的通信网络 104 上。“*在某些实施例中，通信链路 104 可能是使用任何适用的无线技术实现的无线链路，以便在不使用电线的情况下促进信息传输。通信链路 104 可以使用任何适当频率的电磁波来传输信息。例如，电磁波谱中的射频、微波、可见光、红外线和紫外线范围内的频率可被使用。通信链路 104 可以包括用于传输信息的任何无线技术，包括卫星、发射器、接收器、天线、中继器和/或无线电*”。

“*天真的解决方案是在低延迟的链路的两端放置预编程的计算机*”，Wissner-Groos 在这篇[采访](http://spectrum.ieee.org/computing/it/financial-trading-at-the-speed-of-light)中说，并且合作站点导致“*削减点对点延迟的一场军备竞赛。下一阶段是在节点上的设置*”。我记得与一家主要微波供应商的首席执行官在芝加哥和新泽西之间进行的一次讨论；我了解到这家供应商的大多数客户需要用微波从一家交易所（比如说欧罗拉的 CME）收集*数据*，以便他们可以在另一家交易所（比如说 Mahwah 的纽约证券交易所）下订单。这意味着大多数高频交易公司需要超快速网络以便*知道*这里发生了什么，那里发生了什么，然后使用这些数据，合作算法可以决定在哪里实施/合作买卖产品-例如，Mahwah 中的算法需要知道关于 E-mini S&P 期货（ES）的信息，以便它可以在 Mahwah 交易 SPDR S&P 500 ETF（SPY）。这就是为什么数据需要在这两个交易所之间尽可能快地传输-这是一场“军备竞赛”。

![B6nfhBpCUAA7UZN.jpg-large](http://oklo.org/2015/01/01/lightspeed/)

如果你是 McKay Brothers 微波网络（据说是最快的）的交易员和客户，在 Mahwah 和 Aurora 之间最佳的延迟为[4.062](http://www.quincy-data.com/product-page/#latencies)毫秒。从理论上讲，Wissner-Gross 和 Freer 的想法是将算法放置在 Aurora 和 Mahwah 中间的某处（节点），这样算法就可以在±2,031 毫秒内获取数据（这只是一个理论示例，因为大多数节点的最佳位置通常*不*是准确的中点）。由于作者提交了专利申请，并且他们在 2010 年与金融公司“*目前正在就授权[他们的]技术方案进行谈判*”，所以我推测他们的“相对统计证券交易系统和方法”可能具有实际应用，于是我写信给 Wissner-Gross 和 Freer 了解更多信息。回复很温和，但不幸的是他们“*目前无法谈论这个问题*”。太糟糕了。但在收到这个回复几天后，我意识到 2011-2012 年，[Alexander Wissner-Gross](http://www.alexwg.org/companies)和[Cameron Freer](https://www.linkedin.com/in/freer)都是一家名为 Hibernia 的公司的顾问委员会成员。这难道不是很有趣吗？我在想，如果这个系统对交易公司有潜在的用途，如果最快的通信链是微波网络，如果服务器/算法必须沿着这条链路被放置，那就意味着算法可能被放置在塔上，对吗？考虑到比利时位于伦敦-法兰克福路线的中间地带，这意味着我的后院可能被算法入侵…

##### **未来 III：气球还是对流散射？**

“*如果纽约和伦敦的交易中心通过跨洋光纤电缆相连，而将服务器放置在海洋中间可能成本太高或不切实际，即使这被确定为最合适的位置*”，Wissner-Gross 和 Cameron 在专利文件中写道。所以问题是：我们如何将服务器放置在海洋中间？难道要用浮动平台？

今天，一个交易公司可能在两个陆地点之间使用微波网络，但在英国和美国之间建立直线视距网络是不可能的，除非你在大西洋上建立一些浮动岛屿，但那将是复杂和愚蠢的。这就是为什么，至少目前还没有比光纤电缆更好的跨越大洋的解决方案。但在 2014 年 9 月 23 日，*PR Newswire* [宣布](http://www.prnewswire.com/news-releases/innovator-windy-apple-announces-transatlantic-plans-and-offers-promotional-pricing-for-new-york-to-chicago-microwave-network-276622811.html) 说 Windy Apple Technologies (WAT)有计划“使用设备设计和**非传统的部署平台的进步**[我加粗了]建立一项跨大西洋服务。计划包括高比特率和低比特率网络，以实现纽约和伦敦之间的低延迟链接，使 WAT 有机会成为市场上第一个，成本比目前由竞争对手建造的价值十亿美元的跨大西洋光纤系统更加高效。”我们在这里讨论什么？

-   “我们喜欢将不可行的概念变成可行的方式”，WAT 的 CEO Alex Pilosov 说道，他在 2010 年（就在 Spread Networks 光缆投入运营一个月后）建立了芝加哥和纽约之间的第一个微波网络。HFT/微波行业的某位人士告诉我，“Pilosov 就像是那种用两块口香糖就能建造太空火箭的典型俄罗斯工程师”。不幸的是，WAT 和 PR Newswire 对这些计划没有提供很多细节。“公司内部的研发计划探索了利用飞机、气球和卫星进行中继平台部署。”“气球”这个词可能是一个线索：去年 12 月在法国的一个会议上，McKay Brothers 的 CEO Stéphane Tyc 说 HFT 公司需要的微波网络在未来 4-5 年内仍将是最快的技术，然后[谷歌气球](http://www.google.com/loon/)出现了。

![6a00e5500b4a64883301b7c71cece9970b](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/6a00e5500b4a64883301b7c71cece9970b.jpg)

我真的不知道如何利用气球构建一个网络，但我猜（过于简化了）信号将由位于交换机顶部的天线发送，并由放置在平流层气球上的天线接收，然后信号将被发送回地面到另一个交换机？考虑到地球是一个球体，一个高空气球是否足以横跨大西洋？我完全不确定（但如果 Wissner-Gross 和 Cameron 系统投入使用，这种气球将是定位服务器在海洋上的完美场所）。另一个线索可能在我与比利时电信专家的[聊天](https://twitter.com/windyappletech/status/518965058182053888)中找到，他询问“*这些高频交易人员是否曾考虑过将对流散射作为廉价高效的替代方案*”以取代多条视距通讯塔。Alex Pilosov 发表了这样的回答：“*是的，我们做过。事实上，这正是给了我建立远程无线电的想法的源头*”。有趣。

对流层散射技术，简称为对流散射，是一种微波无线电技术，不需要视野通畅的塔。对流散射不是通过一座塔向另一座塔发送信号，而是利用对流层作为影响信号并将其返回地面，因此信号可以被接收天线接收到：

![对流层散射](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/tropospheric_scatter.jpg)

通过对流散射通信技术，信号可以传输长距离（长达 1000 公里），发射机和接收机都不需要“看到”对方。这很惊人，因为我上面提到的大多数旧微波网络（北约的 Ace High，美国军队的国防通信系统等）都是对流散射中继网。Houtem 的跳跃塔是一个“*DCS 对流散射通信链路*”。观察到这种旧的军事技术将来会被高频交易所利用，这不足为奇。对流散射需要的天线要比目前用于视距微波网络的天线大得多。这是英国北约微波 Ace High 网络的一些弃置对流散射天线的照片：

![对流层散射](https://sniperinmahwah.wordpress.com/wp-content/uploads/2015/01/tropodishes1.jpg)

我不太清楚 Windy Apple Technologies 的项目是否涉及对流散射，以及他们是否需要如此大的碟子（我不认为需要），但我们会看到的。总之，很明显军备竞赛还没有结束（还没结束）。高频交易将不得不再次占据自然优势。“*我认为这项工作是让整个地球表面变得更有计算能力的一种可能的理由，”* 亚历山大·维斯纳-格罗斯在这次[采访](http://www.kurzweilai.net/when-the-speed-of-light-is-too-slow)中说。“*实际上，让整个地球变得更聪明*。”我总结一下这个问题：地球对此有什么看法？
