<!--yml
category: 未分类
date: 2024-05-12 19:33:35
-->

# BT HomeHub 2 limited connectivity | Coding the markets

> 来源：[https://etrading.wordpress.com/2013/03/23/bt-homehub-2-limited-connectivity/#0001-01-01](https://etrading.wordpress.com/2013/03/23/bt-homehub-2-limited-connectivity/#0001-01-01)

## BT HomeHub 2 limited connectivity

### March 23, 2013

Going off topic here, as this isn’t etrading related, but I’ll blog it as I suspect others might be having problems with Windows 7 and 8 PCs dropping connections to BT HomHub 2 modem routers. If you’re connection only lasts for a few minutes, and then shows as “limited connectivity” it could be because recent Windows does DHCP differently than Homehub. I found an MS KB article that suggests adding a registry flag in HKEY_LOCAL_MACHINE/SYSTEM/CurrentControlSet/Services/Tcpip/Parameters/Interfaces/{GUID}. The flag is called DhcpConnEnableBcastFlagToggle, it should be a DWORD, and be set to 1\. There may be several GUIDs under Interfaces, depending on how many Wifi hubs your PC talks to. Look inside each and examine IP addresses to figure out which is the Homehub.