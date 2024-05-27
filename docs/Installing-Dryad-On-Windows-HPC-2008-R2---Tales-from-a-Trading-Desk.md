<!--yml

分类：未分类

日期：2024-05-18 06:13:36

-->

# 在 Windows HPC 2008 R2 上安装 Dryad | 来自交易桌的传奇

> 来源：[`mdavey.wordpress.com/2010/04/28/installing-dryad-on-windows-hpc-2008-r2/#0001-01-01`](https://mdavey.wordpress.com/2010/04/28/installing-dryad-on-windows-hpc-2008-r2/#0001-01-01)

## 在 Windows HPC 2008 R2 上安装 Dryad

当你安装 Dryad 时，安装程序会寻找“Microsoft HPC Pack\Bin”，但是 R2 将 HpcScheduler.exe 放在了“Microsoft HPC Pack 2008 R2\Bin”中。因此，执行以下操作：

> 在“程序文件”文件夹中，找到“Microsoft HPC Pack 2008 R2”的位置，创建一个名为“Microsoft HPC Pack”的文件夹。
> 
> 在“Microsoft HPC Pack”中创建一个“Bin”文件夹，并将“Microsoft HPC Pack 2008 R2\Bin”中的 HpcScheduler.exe 复制到“Microsoft HPC Pack\Bin”。
> 
> 在集群上安装 Dryad。

~ mdavey 于 2010 年 4 月 28 日。

发布在[HPC](https://mdavey.wordpress.com/category/hpc/)分类下

标签：[Microsoft](https://mdavey.wordpress.com/tag/microsoft/)
