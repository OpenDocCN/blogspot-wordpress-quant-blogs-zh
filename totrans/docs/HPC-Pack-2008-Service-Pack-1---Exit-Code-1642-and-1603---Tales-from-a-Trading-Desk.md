<!--yml
category: 未分类
date: 2024-05-18 06:13:19
-->

# HPC Pack 2008 Service Pack 1 – Exit Code 1642 and 1603 | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2010/04/20/hpc-pack-2008-service-pack-1-exit-code-1642-and-1603/#0001-01-01](https://mdavey.wordpress.com/2010/04/20/hpc-pack-2008-service-pack-1-exit-code-1642-and-1603/#0001-01-01)

## HPC Pack 2008 Service Pack 1 – Exit Code 1642 and 1603

Trying to install HPC Pack 2008 Service Pack 1 onto Windows Server 2008 Data Center with HPC 2008 – HPC Cluster Manager client/server version 2.0.1551.0 – generate Exit Code 1642\. Reason? Running x86 installer for a 64bit OS doesn’t work 🙂 However, once I ran the x64 installed, I now get:

> MSI (s) (40:B8) [10:45:20:335]: Product: Microsoft HPC Pack – Update ‘Service Pack 1 for HPC Pack 2008 (KB972008)’ could not be installed. Error code 1603\. Additional information is available in the log file C:\Users\ADMINI~1.LAB\AppData\Local\Temp\2\HPC_PATCH.log.
> MSI (s) (40:B8) [10:45:20:336]: Windows Installer installed an update. Product Name: Microsoft HPC Pack. Product Version: 2.1.1703.0\. Product Language: 1033\. Manufacturer: Microsoft Corporation. Update Name: Service Pack 1 for HPC Pack 2008 (KB972008). Installation success or error status: 1603.
> MSI (s) (40:B8) [10:45:20:336]: Note: 1: 1729
> MSI (s) (40:B8) [10:45:20:336]: Product: Microsoft HPC Pack — Configuration failed.
> MSI (s) (40:B8) [10:45:20:337]: Windows Installer reconfigured the product. Product Name: Microsoft HPC Pack. Product Version: 2.1.1703.0\. Product Language: 1033\. Manufacturer: Microsoft Corporation. Reconfiguration success or error status: 1603.

Anyone know how to fix this?

~ by mdavey on April 20, 2010.

Posted in [HPC](https://mdavey.wordpress.com/category/hpc/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)