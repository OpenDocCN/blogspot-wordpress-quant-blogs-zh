<!--yml

分类：未分类

日期：2024-05-18 06:05:06

-->

# Vista：蓝屏死机 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2006/11/18/vista-blue-screen-of-death/#0001-01-01`](https://mdavey.wordpress.com/2006/11/18/vista-blue-screen-of-death/#0001-01-01)

## Vista：蓝屏死机

老实说，这是预料之中的。在戴尔 D620 便携式电脑上安装 Windows Vista RTM 没有遇到任何障碍 - 不足为奇，因为硬件不到 3 个月。我的戴尔台式机完全是另一回事。基本上，我与 RC1 和[RC2](https://mdavey.wordpress.com/2006/05/27/vista-build-5384-office-beta-2/)遇到相同的驱动程序问题。问题的根源是我的台式机拥有不错的 512Mb [ATI](http://ati.amd.com/) Radeon X1600 PRO，但是在安装 Windows Vista RTM 时，微软慷慨提供的此卡的驱动程序版本为 7.14，日期为 2006 年 8 月 21 日，而 ATI 网站上提供的驱动程序为[8.31](http://www.atitech.ca/support/drivers/vista32/common-vista32.html)，日期为 2006 年 11 月 2 日。7.12 驱动程序似乎导致 Vista 安装在加载驱动程序时挂起；这立即导致蓝屏死机。然后这个问题变成了下一个问题；蓝屏在出现约 1-2 秒后，PC 重新启动，尝试继续安装。在这段时间内，我设法读到的唯一单词是“驱动程序在无限循环”或类似内容，这并不非常有帮助。我最终安装了 Vista，但是只有按照这些步骤才能实现：

+   用原始戴尔视频卡替换 X1600 视频卡 - NVIDIA g-Force 2 MX.

+   安装 Windows Vista

+   重新安装 X1600 PRO 视频卡.

+   在 Vista 启动时，它会友好地检测到新视频卡，并安装由微软提供的旧驱动程序 - 似乎没有简单的方法可以取消此安装，所以如果您在此之后重新启动，那么 Vista 将再次蓝屏，您必须进入安全模式并删除图形卡.

+   安装最新的 ATI 驱动程序

现在 Vista Aero 在我的戴尔台式机上运行良好。我必须解决的最后问题是，戴尔最初附带 CNET 以太网卡，如预期的那样没有 Vista 驱动程序 😦 幸运的是，[Dabs](http://www.dabs.com)以不到 10 英镑的价格出售 D-Link DFE-530TX 卡 - 此网络卡的驱动程序似乎已经在 Vista 中提供。

总的来说我对便携式电脑上的 Vista 感到满意，但是对于 4 岁的戴尔台式机上的 Vista 印象深刻.

~ mdavey 于 2006 年 11 月 18 日.

发布于：[未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签：[微软](https://mdavey.wordpress.com/tag/microsoft/)
