<!--yml
category: 未分类
date: 2024-05-12 19:30:53
-->

# Windows Containers | Coding the markets

> 来源：[https://etrading.wordpress.com/2015/10/13/windows-containers/#0001-01-01](https://etrading.wordpress.com/2015/10/13/windows-containers/#0001-01-01)

## Windows Containers

### October 13, 2015

Recently Microsoft has added support for containers to Windows Server. It’s available on the Azure cloud on VMs running Windows Server 2016 Tech Preview 3\. I’ve been playing with it and I’ve got SpreadServe running inside a container. There’s [much more detail here](http://spreadserve.readthedocs.org/en/latest/cont1.html). But to summarise I found three workarounds were necessary…

*   A two step process to build images as Windows container doesn’t like SpreadServe’s NSIS installer
*   Web server inside the container should be on port 80 only internally
*   A one line launch script that sets up environment variables is necessary