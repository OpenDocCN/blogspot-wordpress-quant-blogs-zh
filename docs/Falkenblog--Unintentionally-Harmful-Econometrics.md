<!--yml

category: 未分类

日期：2024-05-12 21:31:36

-->

# Falkenblog: 不经意间有害的计量经济学

> 来源：[`falkenblog.blogspot.com/2010/05/mostly-harmless-econometrics.html#0001-01-01`](http://falkenblog.blogspot.com/2010/05/mostly-harmless-econometrics.html#0001-01-01)

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiEg3tclSucrfdi3AsL6ICp-FDGQU7aBhUCt_MBMYeUT3_Ow_EwrzVV7l83_og_H879L0deZ6vhYz7_IpbxdpGcAXGNkRNZG0-MAxREg2XW6A1D80ZUy2MO54dDpkCEXJ9YLPla2g/s1600/econ.gif)

劳动经济学家约书亚·安格里斯特和约恩·史蒂芬·皮什克在计量经济学上有一本小册子：

[Mostly Harmless Econometrics](http://www.mostlyharmlesseconometrics.com/)

。唉，与道格拉斯·亚当斯写的任何东西的链接都有些牵强，但我欣赏他们轻松的做法。基本上，他们概述了困扰计量经济研究的根本问题：数

[遗漏变量偏差](http://carecon.org.uk/UWEcourse/OVbias.pdf)

.

比如你想要估计教育对收入的影响。上学时间更长的人收入更高。但他们也有更好的纪律，来自更好的社会经济背景，并且有更高的智商，这些都可能是真正的原因。如果你没有在回归中包括这些变量，你会因为这些遗漏的变量（通常很难或在智商的情况下是禁忌的）而将太多的好处归因于教育。所以这本书介绍了各种方法来揭示真正的关系。在这种方法中，最重要的是

[Freakonomics](http://en.wikipedia.org/wiki/Freakonomics)

自然实验方法。这是当某些任意事件创造了不同的样本，有利于关注的变量（学校教育），但其他因素（智商、财富、纪律）是相同的。

基本上，你要比较一组受某种任意过程影响而导致 B 组无法获得更多教育的群体，并与 A 组进行比较，其它方面是无法区别的，但 A 组获得了更多的教育。该书中的典型例子是

[Angrist and Krueger](http://aysps.gsu.edu/isp/files/ISP_SUMMER_SCHOOL_2008_ERARD_INSTRUMENTAL_VARIABLES.pdf)

（1991）年的论文，利用了许多州要求儿童在 16 岁之前上学，并且他们必须在 6 岁时开始上学的事实。由于学年在 6 月结束，这意味着刚开始上学前出生的孩子在另一年开始之前将年满 16 岁，而那些刚出生后的孩子只有 15 岁，必须至少开始另一年的学习。这是因为孩子由于其出生日期而仅获得不同程度的教育，而这与智商、纪律和社会经济地位无关。一种“自然实验”。

找到“识别限制”的确切方法并不那么重要。它是严格研究的中流砥柱，但最终，如果您的结果只通过两阶段最小二乘法的系数 t 统计值显示出来，而不是图表，那么它就不在那儿。这些收入是，那些多上了一年学的孩子有什么区别？在这里，我们看到了计量经济学的问题。作者们对安格里斯特和克鲁格研究的 12 月 31 日左右显示出显著生日增长的锯齿形图案非常兴奋，突出了说留校多一年提供了收入上的统计显著增长。

但效应很小，因为那些因太晚出生而无法跳过最后一年级的孩子，有大约 3％的工资效应。当然，有足够的观察结果才是重要的，但这并不足以改变世界。它成为了哈佛经济学家一代人的灵感，就因为这种方法似乎使用了聪明才智和高级的计量技术来解决问题。然而，并不是每个留校一个额外的年级的 16 岁意味着也去上大学会有帮助。很少有效果是线性的。我可能上几节高尔夫课就能把我的得分降低 10 杆；但这并不能意味着，一年后，我就可以参加美巡赛。作者似乎忽略了这一点。

人们可能会说，他对非线性有很长的部分，实际上他确实有。但他对他的 3％工资增长给予的过多关注替盖了这种知识。净推论很明显是，3％的工资增长具有政策意义，否则他和劳动经济学界不会引用它这么多。最终，他不认为非线性与他有关

人们可以设想他们在国会作证，认为他们的研究证明我们应该在大学上花更多的钱，但这假设了很多事情。它假定他们 16 岁时的结果是线性的外推。它假定在大学教育上花更多的钱真的会增加学业，而不是学校所收费的费用。它假定人们会学习真正与技能相关的学科，而不是成为不学到任何有用东西的电影研究专业毕业生。

通过计量技术和自然实验对常识的所有激动 ant 都被这篇关于文件共享对唱片销售的影响的论文最好地展示出来

[Oberholzer-Gee 和 Strumpf](https://docs.google.com/viewer?url=http://www.unc.edu/~cigar/papers/FileSharing_March2004.pdf)

，作为 2007 年 2 月《政治经济学杂志》（莱维特的期刊）的头条文章发表，受到了极大的欢迎。他们所测得的乐器（德国学生放假期间）与其仪器化的美国下载相关的变量之间的关系看来有很大的影响，可能是因为德国人下载和分享大量音乐，并且在度假期间花了很多时间分享文件。

无论如何，奥伯霍尔泽-吉和斯特朗普的大部分工作强调的是计量经济学，而不是其他东西。

[斯坦利博维茨](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1598037)

提出来的问题，比如在德国学校的学生中实际下载音乐的比例占音乐下载量的百分比，以及他们占美国音乐销售额的百分比。假期时间与传统的美国季节模式相关，因为音乐销售在圣诞节前激增，而德国的孩子们在学校的原因与文件分享无关（圣诞袜需要 CD）。基本上，经验问题是一个机构细节的问题，了解音乐销售的季节性、学校时间表、音乐下载的时间，而与强调他们学术作品中的识别限制几乎无关。

在某种意义上，计量经济学作为一门科学，允许粗糙的经验研究隐藏在对避免这些问题的装腔作势的技术之后。矢量自回归或自然实验并不能免除对常识和所应用工具的主题的理解的需求。在 20 世纪 80 年代显而易见的未能预测股票收益、商业周期、利率的表现，促使计量经济学家寻找存在自然实验的小课题，然后进行一些伟大的推断。人们对问题的思考不如对方法的思考多，然后假设因为结果如此干净，它就会很深刻。我认为很多计量经济学家希望是这样，这样他们就可以专注于自己真正喜欢的数学，同时又能对重要问题如学校教育提出有趣的观点。

如果，比如，推断风险溢价的唯一方法是使用基于某个基本效用函数的 3 个识别限制的方法矩估计，但最终你无法说可口可乐是否比通用汽车更风险，那么你没有结果。这是学术性的。
