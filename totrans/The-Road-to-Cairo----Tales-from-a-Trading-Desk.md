<!--yml
category: 未分类
date: 2024-05-18 06:07:48
-->

# The Road to Cairo? | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2008/07/15/the-road-to-cairo/#0001-01-01](https://mdavey.wordpress.com/2008/07/15/the-road-to-cairo/#0001-01-01)

## The Road to Cairo?

It’s been clear for quite some time that [Microsoft](http://www.microsoft2.net/) would at some point like to offer an OS in managed code (remember WinFX and the managed [API](http://www.joelonsoftware.com/articles/APIWar.html) PDC statements?). Couple this view with recent “cloud” thoughts, and you can see that one of Microsoft’s future goals is a distributed cloud managed OS. Microsoft Research has been actively rolling down this road with a number of initiatives – [Singularity](http://research.microsoft.com/os/Singularity/), [CHESS](http://research.microsoft.com/projects/CHESS/) and [Dryad](http://research.microsoft.com/research/sv/Dryad/) – have a look at [slide 35](http://research.microsoft.com/projects/CHESS/chess.ppt). Midori may or may not be the product that we see in a few years that provides this managed stack.

One of the problems as I understand it with the Windows OS today is its need to be [backwards compatible](http://blogs.msdn.com/oldnewthing/). One though I had after seeing [MinWin](http://channel9.msdn.com/shows/Going+Deep/Mark-Russinovich-On-Working-at-Microsoft-Windows-Server-2008-Kernel-MinWin-vs-ServerCore-HyperV/) was that Microsoft should release MinWin as essentially a VM OS (25Mb), which by default hosts Windows Vista and XP. Singularity/Midori should be the third hosted OS, which would offer the first 100% Microsoft managed OS and move .NET to the next paradigm. Using MinWin avoids the need to pollute Midori, thereby allowing a clean future generation OS to evolve, yet maintaining Microsoft’s backward compatibility for legacy applications.

Midori in summary could possible be [Microsoft’s](http://blogs.zdnet.com/Bott/?p=486) latest attempt to delivery [Cairo](http://en.wikipedia.org/wiki/Cairo_(operating_system)). However, based on previous attempts to delivery Cairo, at this stage its unclear if we will ever actually see Singularity/Midori outside of the incubator stage. Maybe Microsoft needs to put its research division at the heart of the company to keep innovation alive – we don’t want another [WinFS](http://en.wikipedia.org/wiki/WinFS)….

~ by mdavey on July 15, 2008.

Posted in [.NET](https://mdavey.wordpress.com/category/languages/net/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)