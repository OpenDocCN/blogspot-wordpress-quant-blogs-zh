<!--yml

类别: 未分类

日期: 2024-05-12 19:33:35

-->

# BT HomeHub 2 有限连接 | 编码市场

> 来源：[`etrading.wordpress.com/2013/03/23/bt-homehub-2-limited-connectivity/#0001-01-01`](https://etrading.wordpress.com/2013/03/23/bt-homehub-2-limited-connectivity/#0001-01-01)

## BT HomeHub 2 有限连接

### 2013 年 3 月 23 日

这里有点跑题，因为这与电子交易无关，但我会将它作为博客发布，因为我怀疑其他人可能会遇到 Windows 7 和 8 的 PC 与 BT HomHub 2 调制解调器路由器断开连接的问题。如果你的连接只能持续几分钟，然后显示为“有限连接”，可能是因为最近的 Windows 对 DHCP 的处理方式与 Homehub 不同。我找到了一篇微软的知识库文章，建议在 HKEY_LOCAL_MACHINE/SYSTEM/CurrentControlSet/Services/Tcpip/Parameters/Interfaces/{GUID}中添加一个注册表标志。该标志称为 DhcpConnEnableBcastFlagToggle，应为 DWORD，并设置为 1。根据你的 PC 与多少个 Wifi 中继器通信，Interfaces 下可能有几个 GUID。检查每个 GUID 并检查 IP 地址，以确定哪个是 Homehub。
