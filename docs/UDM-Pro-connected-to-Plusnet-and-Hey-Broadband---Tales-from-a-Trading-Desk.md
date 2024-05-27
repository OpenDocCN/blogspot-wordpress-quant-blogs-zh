<!--yml

分类：未分类

日期：2024-05-18 05:25:57

-->

# **UDM Pro** 连接到 Plusnet 和 Hey!Broadband | 交易桌旁的故事

> 来源：[`mdavey.wordpress.com/2023/02/08/udm-pro-connected-to-plusnet-broadband-and-heybroadband-fibre/#0001-01-01`](https://mdavey.wordpress.com/2023/02/08/udm-pro-connected-to-plusnet-broadband-and-heybroadband-fibre/#0001-01-01)

在等待光纤在我的地区可用，感觉像是几年的时间里，三周前，我终于在家中安装了光纤，但解决连接问题花了几周时间😦 以下是一份总结，帮助其他跟随我脚步的人：

我长期以来一直在使用 [Plusnet](https://www.plus.net/) 宽带。宽带通过铜质电话线接入，进入 OpenReach 桥接，然后从桥接接到 Plusnet 四端口路由器。以前我将路由器连接到 UDM Pro 的默认端口 9（WAN）。这很好，直到你决定你需要一个静态 IP 地址，这时你需要将 OpenReach 桥接直接连接到 WAN 默认端口 9，并通过 UDM Pro 仪表板，设置/互联网，选择默认（WAN），在高级部分，选择手动，对于 IPv4 连接选择 PPPoE，并输入 Plusnet 用户名和密码。这应该允许**UDM Pro** 通过 PPPoE 连接到 Plusnet。

我决定在一段时间内保留 Plusnet，同时我安装 Hey!Broadband Fibre，并对服务质量有一个了解。Plusnet 在过去的几年里提供了良好的服务质量，但在我的地区没有提供光纤。

**Hey!Broadband Fibre** 以桥接模式接入，而在非桥接安装中，会连接到无线路由器。我选择了桥接模式，带有静态 IP，因此不需要无线路由器。**UDM Pro** 端口 10（WAN2）是需要从光纤桥接调制解调器连接以太网电缆的端口。一旦连接完成，需要在**UDM Pro** 仪表板，设置/互联网，选择备份（WAN2）高级设置中启用 PPPoE，并输入适当的用户名和密码。如果你想在启用 PPPoE 时查看日志，需要从 LAN 上的任何机器通过 SSH 连接到**UDM Pro**，并尾随 /var/log/message。你也许还需要运行 ifconfig 和 route -n 来检查在成功连接后接口是否设置如预期。在服务初始设置过程中，我遇到的错误从找不到远程主机、不支持的地址族、格式错误的 DNS 回复到无法完成 PPPoE 发现。

现在你的**UDM Pro** 仪表板（左上角）应该显示 WAN 和 WAN2，并在网关 IP 上面有 IP 地址。你应该能够从 UDM Pro 仪表板（右下角）运行速度测试，通过选择 WAN 或 WAN2 然后选择速度测试，为两个互联网连接（WAN/WAN2）。

在整个光纤安装过程中，我遇到了两个问题。Hey!Broadband 没有正确设置桥接调制解调器。我用笔记本电脑进行了诊断，通过 PPPoe 连接到桥接调制解调器，并报告了我看到的问题。在成功建立 PPPoe 连接后，我在桥接调制解调器或更远处的 Hey!Broadband 网络上看到了 DNS 解析问题。我将这个问题报告给技术支持，在第二天早上 6:40 解决了问题——实际上他们为我分配了一个新的静态 IP。

在成功的 PPPoe 连接和解决的 DNS 问题之间，我希望 OpenReach PPPoe 能够从 Port10（WAN2）工作，因为它将是故障转移的目标。后来发现 Port10 不能降级到 100Mb，这是 OpenReach 桥接能够实现的最大连接。实际上我现在拥有 Port9（WAN）的 Plusnet 和 Port10（WAN2）的 Hey!Broadband Fibre，这与故障转移的默认 UDM Pro 设置相反。为了解决这个问题，我进入了 UDM Pro 的[端口管理](https://help.ui.com/hc/en-us/articles/360008365334-UniFi-Configure-Port-Remapping)，将 WAN 交换到 Port10，将 WAN2 交换到 Port9。问题解决。

在上述故障转移配置实施后，虽然 PPPoe 连接成功，但 DNS 问题仍未解决，UDM Pro 故障转移至 WAN2，并且使用了速度较慢的 Plusnet 宽带。通常在凌晨 1 点到 6:40 之间，Hey!Broadband 会解决 DNS/PPPoe 问题，UDM Pro 会故障恢复至 WAN。

~ mdavey 于 2023 年 2 月 8 日。

发布在[未分类](https://mdavey.wordpress.com/category/uncategorized/)。
