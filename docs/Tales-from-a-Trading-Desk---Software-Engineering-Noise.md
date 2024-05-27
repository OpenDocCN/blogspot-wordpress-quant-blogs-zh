<!--yml

分类：未分类

日期：2024-05-18 06:37:39

-->

# 交易台故事 | 软件工程噪音

> 来源：[`mdavey.wordpress.com#0001-01-01`](https://mdavey.wordpress.com#0001-01-01)

在等待我的林地区域光纤可用，感觉像是等了好几年之后，三周前，我终于把光纤安装到了我的房子里，但解决连通性问题花了几周时间😦 以下是一份总结，希望能帮助后来者：

我一直使用[Plusnet](https://www.plus.net/)宽带。宽带通过铜质电话线进入，经过 OpenReach 桥接，再从桥接器接到 Plusnet 4 端口路由器。以前我将路由器连接到 UDM Pro 的 Port9（默认端口）(WAN)。这样是可以的，直到你想使用静态 IP 地址，这时你需要将 OpenReach 桥接器直接连接到 WAN，即默认的 Port9，然后通过 UDM Pro 控制面板，设置/互联网，选择默认（WAN），在高级设置中，选择手动，对于 IPv4 连接选择 PPPoE，并输入 Plusnet 用户名和密码。这应该可以让 UDM Pro 通过 PPPoE 连接到 Plusnet。

我决定在一段时间内保留 Plusnet，同时我安装 Hey!Broadband Fibre，并了解服务质量。Plusnet 在过去几年中提供了良好的服务质量，但在我的地区不提供光纤。

[Hey!Broadband Fibre](https://heybroadband.co.uk/for-home)提供一个桥接模型，在非桥接安装中，会连接到无线路由器。我选择了桥接模式，并使用静态 IP，因此不需要无线路由器。UDM Pro Port10（WAN2）是需要的从光纤桥接调制解调器连接以太网线的端口。一旦连接完成，UDM Pro 控制面板，设置/互联网，选择备份（WAN2）高级设置需要启用 PPPoE，并输入正确的用户名和密码。如果你想在启用 PPPoE 时查看日志，从你局域网中的任何一台机器通过 SSH 登录到 UDM Pro，并查看/var/log/message 的尾端。你也许还想要使用 ifconfig 和 route -n 命令来检查在成功连接后接口是否设置如预期。在服务初始设置过程中，我遇到的错误从找不到远程主机、不支持的地址族、格式错误的 DNS 回复到无法完成 PPPoE 发现。

现在你的 UDM Pro 控制面板（左上角）应该显示 WAN 和 WAN2，并在网关 IP 上方显示 IP 地址。你应该能够从 UDM Pro 控制面板（右下角）对两个互联网连接（WAN/WAN2）进行速度测试，通过选择 WAN 或 WAN2，然后选择速度测试。

在安装光纤整体过程中，我遇到了两个问题。嘿！宽带没有正确设置桥接调制解调器。我用笔记本电脑进行了诊断，通过桥接调制解调器进行 PPPoE 连接，并报告了我看到的问题。在成功进行 PPPoE 连接后，我发现桥接调制解调器或进一步进入嘿！宽带网络的 DNS 解析存在问题。我将此问题报告给技术支持，在第二天早上 6.40 解决了问题——实际上他们为我分配了一个新的静态 IP。

在成功进行 PPPoE 连接和解决 DNS 问题之间，我希望 OpenReach PPPoE 能从 Port10（WAN2）工作，因为它将是故障转移的手段。后来发现 Port10 不能降级到 100Mb，这是 OpenReach 桥接能达到的最大连接。实际上我现在有了 Port9（WAN）Plusnet 和 Port10（WAN2）嘿！宽带光纤，这与故障转移的默认 UDM Pro 设置正好相反。为了解决这个问题，我进入了 UDM Pro 的[端口管理](https://help.ui.com/hc/en-us/articles/360008365334-UniFi-Configure-Port-Remapping)，并将 WAN 交换到 Port10，WAN2 交换到 Port9。解决了问题。

在上述故障转移配置就绪后，PPPoE 连接成功，但 DNS 问题未解决，UDM Pro 故障转移到了 WAN2，并使用了较慢的 Plusnet 宽带。在凌晨 1 点到 6:40 之间，嘿！宽带解决了 DNS/PPPoE 问题，UDM Pro 恢复到了 WAN。

发布在[未分类](https://mdavey.wordpress.com/category/uncategorized/)
