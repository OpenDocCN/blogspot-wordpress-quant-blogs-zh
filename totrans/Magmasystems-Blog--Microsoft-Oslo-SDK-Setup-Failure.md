<!--yml
category: 未分类
date: 2024-05-18 04:57:45
-->

# Magmasystems Blog: Microsoft Oslo SDK Setup Failure

> 来源：[http://magmasystems.blogspot.com/2008/11/microsoft-oslo-sdk-setup-failure.html#0001-01-01](http://magmasystems.blogspot.com/2008/11/microsoft-oslo-sdk-setup-failure.html#0001-01-01)

It looks like you need SQL Server 2008 installed in order to use Oslo. Microsoft does not state this anywhere, nor does its installation program warn you of this. Here is my experience in trying to install Oslo on my laptop.

1) I downloaded the Oslo SDK CTP from the Microsoft site.

2) I extracted the files, and ran the setup. The setup completed without any warnings and error messages. So far so good.

3) I have Windows Vista SP1 with both SQL Server 2005 and SQL Server Express 2005 installed. I opened up SQL Server Management Studio and searched both servers for any trace of the Oslo repositories. No luck.

4) In the directory

C:\Users\Marc\AppData\Local\Temp

, I found a file called

Oslo_Repository_Setup.log

. I opened this file in Notepad and found the following lines:

Property(C): ExecuteSilentCmd = "C:\Program Files\Microsoft Repository\CreateRepository.exe" /v+
Property(C): WIXUI_EXITDIALOGOPTIONALTEXT = Warning: repository database creation failed. Please see %temp%\RepositorySetup.log for more details. 

However, at the very end of the file, I found the following lines:

MSI (c) (B0:48) [06:51:33:985]: Product: Microsoft Codename "Oslo" Repository -- Installation completed successfully.

MSI (c) (B0:48) [06:51:33:987]: Windows Installer installed the product. Product Name: Microsoft Codename "Oslo" Repository. Product Version: 3.0.1342.0\. Product Language: 1033\. Installation success or error status: 0. 

So, it looks like the installer considered the installation to be a success, even though the repository could not be created.

5) In the file RepositorySetup.log, I found the following lines:

message: Creating repository database ...

error: Cannot assign a default value to a local variable.

Must declare the scalar variable "@login".

[11/3/2008 - 6:51:24]Completed execution of: "C:\Program Files\Microsoft Repository\CreateRepository.exe" /v+

6) We see other users who have

[reported this](https://connect.microsoft.com/oslo/feedback/ViewFeedback.aspx?FeedbackID=378415)

. Microsoft says that this is not a bug. It is "By Design".

7) At

[this link](http://social.msdn.microsoft.com/Forums/en-US/oslo/thread/c0ee4730-4595-4971-a2f3-a988997c4616)

, we find a comment by Carlos Gomez of Microsoft:

We do not support Sql Server 2005 at all, because some of the repository features depend on Sql Server Katmai.

In other words, you need to have SQL Server 2008 installed. Well, my company is still on SS 2005, so I guess that means that Oslo will be just for my personal experimentation for the forseeable future.

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.