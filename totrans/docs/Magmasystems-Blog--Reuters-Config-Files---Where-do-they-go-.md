<!--yml
category: 未分类
date: 2024-05-18 04:57:30
-->

# Magmasystems Blog: Reuters Config Files - Where do they go?

> 来源：[http://magmasystems.blogspot.com/2008/11/reuters-config-files-where-do-they-go.html#0001-01-01](http://magmasystems.blogspot.com/2008/11/reuters-config-files-where-do-they-go.html#0001-01-01)

If you are using the Reuters RFA 6.x APIs to consume market data, you know that there are three config files that RFA needs to find. These configuration files are

*   RFA.CFG
*   appendix_a
*   enumtype.def

Usually, if you are running a console or WinForms application, you put these config files in the same directory as your executable.

However, what if you are running a

Windows Service

that uses RFA?

After some experimentation, we found that you need to store the files in these places:

*   Windows 32 - Put the files in c:\WINNT\system32
*   Windows 64 - Put the files in c:\WINNT\SysWow64

A service or an executable that uses RFA (the Marketfeed API, not the OMM API) uses 32-bit DLLs. This is because Reuters does not yet have 64-bit DLLs for RFA. Therefore, you need to use

[CorFlags.exe](http://msdn.microsoft.com/en-us/library/ms164699%28VS.80%29.aspx)

on a 64-bit Windows 2003 server in order to get your application to run.

Thanks to the wonderful Procmon utility from SysInternals for helping us out with this issue.

©2008 Marc Adler - All Rights Reserved.

All opinions here are personal, and have no relation to my employer.