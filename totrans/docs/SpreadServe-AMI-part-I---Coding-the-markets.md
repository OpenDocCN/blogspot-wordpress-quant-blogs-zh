<!--yml
category: 未分类
date: 2024-05-12 19:30:19
-->

# SpreadServe AMI part I | Coding the markets

> 来源：[https://etrading.wordpress.com/2017/01/16/spreadserve-ami-part-i/#0001-01-01](https://etrading.wordpress.com/2017/01/16/spreadserve-ami-part-i/#0001-01-01)

## SpreadServe AMI part I

### January 16, 2017

Recently I’ve been working on building an [EC2 AMI](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html) for [SpreadServe](http://spreadserve.com), so deployment becomes a one click operation for [Amazon AWS](https://aws.amazon.com/) users. I ran into an interesting snag so I thought I’d capture it here. My aim was to deploy SpreadServe as a Windows Service on an [AWS Windows Server 2012 R2](https://aws.amazon.com/marketplace/pp/B00KQOWCAQ) image, so I used [pywin32](https://pypi.python.org/pypi/pywin32)‘s excellent [win32service](https://pypi.python.org/pypi/infi.win32service) module. Here’s my [github boilerplate project](https://github.com/osullivj/MTWService) for a Windows Service in Python. On my AWS host my SpreadServe Windows Service was failing to start, and leaving no trace in the system or application event logs. pywin32service has a debug mode; when I tried that I got a Windows 0xc00007b error, which indicates a mix of 32 and 64 bit binaries. SpreadServe is 32 bit all the way, so something was wrong. I turned to [procmon](https://technet.microsoft.com/en-us/sysinternals/processmonitor.aspx) to try and figure what was failing. procmon showed that my 32 bit pythonservice.exe was loading a 64 bit python27.dll, instead of the 32 bit python27.dll that’s part of the SpreadServe install tree. The 64 bit DLL was coming from the C:\Program Files\Amazon\cfn-bootstrap directory, which is added to the standard Windows 2012 R2 image by Amazon to support [CloudFormation](https://aws.amazon.com/cloudformation/), and is on the system path. After much experimenting I couldn’t find a way to stop Windows Service Host from using the system path, so I had to change it to replace cfn-bootstrap with SpreadServe directories. Problem solved…