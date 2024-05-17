<!--yml
category: 未分类
date: 2024-05-18 06:13:36
-->

# Installing Dryad On Windows HPC 2008 R2 | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2010/04/28/installing-dryad-on-windows-hpc-2008-r2/#0001-01-01](https://mdavey.wordpress.com/2010/04/28/installing-dryad-on-windows-hpc-2008-r2/#0001-01-01)

## Installing Dryad On Windows HPC 2008 R2

When you install Dryad the installer looks for “Microsoft HPC Pack\Bin” but R2 puts HpcScheduler.exe in “Microsoft HPC Pack 2008 R2\Bin”. Hence do the following:

> In the Program Files folder where “Microsoft HPC Pack 2008 R2” is located, create a folder named “Microsoft HPC Pack”.
> Create a “Bin” folder in “Microsoft HPC Pack” and copy HpcScheduler.exe fom “Microsoft HPC Pack 2008 R2\Bin” to “Microsoft HPC Pack\Bin”.
> Install Dryad on the cluster.

~ by mdavey on April 28, 2010.

Posted in [HPC](https://mdavey.wordpress.com/category/hpc/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)