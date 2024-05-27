<!--yml

category: 未分类

date: 2024-05-12 19:30:53

-->

# Windows 容器 | 编写市场代码

> 来源：[`etrading.wordpress.com/2015/10/13/windows-containers/#0001-01-01`](https://etrading.wordpress.com/2015/10/13/windows-containers/#0001-01-01)

## Windows 容器

### October 13, 2015

最近，微软已经为 Windows Server 添加了对容器的支持。它可用于 Azure 云上运行 Windows Server 2016 Tech Preview 3 的虚拟机。我一直在使用它，并且我已经在容器内成功运行了 SpreadServe。这里有[更多详细信息](http://spreadserve.readthedocs.org/en/latest/cont1.html)。但总结一下，我发现需要三个解决方法…

+   一个两步骤的过程来构建镜像，因为 Windows 容器不喜欢 SpreadServe 的 NSIS 安装程序

+   容器内的 Web 服务器应该只在内部使用端口 80

+   需要一个一行的启动脚本来设置环境变量
