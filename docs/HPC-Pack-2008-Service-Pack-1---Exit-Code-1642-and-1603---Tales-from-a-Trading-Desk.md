<!--yml

类别：未分类

日期：2024 年 05 月 18 日，06:13:19

-->

# HPC Pack 2008 服务包 1 – 退出代码 1642 和 1603 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2010/04/20/hpc-pack-2008-service-pack-1-exit-code-1642-and-1603/#0001-01-01`](https://mdavey.wordpress.com/2010/04/20/hpc-pack-2008-service-pack-1-exit-code-1642-and-1603/#0001-01-01)

## HPC Pack 2008 服务包 1 – 退出代码 1642 和 1603

尝试在装有 HPC 2008 – HPC 集群管理程序客户端/服务器版本 2.0.1551.0 的 Windows Server 2008 数据中心版上安装 HPC Pack 2008 服务包 1 之时出现退出代码 1642\. 原因？在 64 位操作系统上运行 x86 安装程序无效 🙂 然而，一旦我运行了 x64 安装程序，现在出现：

> MSI (s) (40:B8) [10:45:20:335]: 产品：Microsoft HPC Pack – 更新“HPC Pack 2008 服务包 1 (KB972008) 的服务包 1”无法安装。出错代码 1603\. 更多信息请查看日志文件 C:\Users\ADMINI~1.LAB\AppData\Local\Temp\2\HPC_PATCH.log。
> 
> MSI (s) (40:B8) [10:45:20:336]: Windows Installer 安装了更新。 产品名称：Microsoft HPC Pack。 产品版本：2.1.1703.0\. 产品语言：1033\. 生产厂家：微软公司。 更新名称：HPC Pack 2008 服务包 1 (KB972008)。 安装成功还是出错状态：1603。
> 
> MSI (s) (40:B8) [10:45:20:336]: 注：1: 1729
> 
> MSI (s) (40:B8) [10:45:20:336]: 产品：Microsoft HPC Pack — 配置失败。
> 
> MSI (s) (40:B8) [10:45:20:337]: Windows Installer 重新配置了产品。 产品名称：Microsoft HPC Pack。 产品版本：2.1.1703.0\. 产品语言：1033\. 生产厂家：微软公司。 重新配置成功还是出错状态：1603。

有人知道如何解决这个问题吗？

~ 作者 mdavey，2010 年 4 月 20 日。

发布在 [HPC](https://mdavey.wordpress.com/category/hpc/)

标签：[Microsoft](https://mdavey.wordpress.com/tag/microsoft/)
