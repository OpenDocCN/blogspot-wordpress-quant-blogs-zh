<!--yml

category: 未分类

日期：2024-05-12 19:30:19

-->

# 扩散服务 AMI 第一部分 | 编码市场

> 来源：[`etrading.wordpress.com/2017/01/16/spreadserve-ami-part-i/#0001-01-01`](https://etrading.wordpress.com/2017/01/16/spreadserve-ami-part-i/#0001-01-01)

## 扩散服务 AMI 第一部分

### 2017 年 1 月 16 日

最近我一直在为[SpreadServe](http://spreadserve.com)构建一个[EC2 AMI](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html)，以便在[Amazon AWS](https://aws.amazon.com/)上进行部署，成为一键操作。我遇到了一个有趣的问题，所以我决定在这里记录下来。我的目标是将 SpreadServe 部署为在[AWS Windows Server 2012 R2](https://aws.amazon.com/marketplace/pp/B00KQOWCAQ)镜像上的 Windows 服务，所以我使用了[pywin32](https://pypi.python.org/pypi/pywin32)的[win32service](https://pypi.python.org/pypi/infi.win32service)模块。这是我在 Python 中为 Windows 服务的一个[github 模板项目](https://github.com/osullivj/MTWService)。在我的 AWS 主机上，我的 SpreadServe Windows 服务无法启动，系统或应用程序事件日志中没有留下任何痕迹。pywin32service 有一个调试模式；当我尝试时，我得到了一个 Windows 0xc00007b 错误，这表明有 32 位和 64 位二进制文件的混合。SpreadServe 完全是 32 位的，所以有些地方出了问题。我转向[procmon](https://technet.microsoft.com/en-us/sysinternals/processmonitor.aspx)试图找出哪里出了问题。procmon 显示我的 32 位 pythonservice.exe 正在加载一个 64 位的 python27.dll，而不是 SpreadServe 安装树中的 32 位 python27.dll。64 位的 DLL 来自 C:\Program Files\Amazon\cfn-bootstrap 目录，Amazon 将其添加到标准的 Windows 2012 R2 镜像中以支持[CloudFormation](https://aws.amazon.com/cloudformation/)，并且它在系统路径上。经过大量的实验，我无法找到阻止 Windows 服务主机使用系统路径的方法，所以我不得不将其更改为用 SpreadServe 目录替换 cfn-bootstrap。问题解决…
