<!--yml
category: 未分类
date: 2024-05-12 19:28:54
-->

# Showstopper! | Coding the markets

> 来源：[https://etrading.wordpress.com/2020/12/08/showstopper/#0001-01-01](https://etrading.wordpress.com/2020/12/08/showstopper/#0001-01-01)

## Showstopper!

### December 8, 2020

I’ve just finished reading Zachary’s Showstopper, a riveting account of the development of Windows NT at Microsoft in the late 80s and early 90s. I do love industry war stories, so I’m puzzled by the fact I missed this book somehow. Other similar works I’ve enjoyed include Ferguson’s No Prisoners, Kidder’s Soul of a New Machine and Levy’s Hackers. The book is slightly marred at times by clunky explanations of core development activities like coding, test, debugging and building. Zachary is a tech journo, but obviously not a coder. Beyond that minor objection there’s much to enjoy, and several surprises. Those who’ve been around the software world for the last couple of decades will recognize the dramatis personae: Bill Gates, Steve Ballmer, Nathan Myrhvold, and the NT lead, Dave Cutler, developer of VMS at DEC. The narrative follows an arc familiar to any who have worked on a large software project, with all the typical setbacks and pressures. Here are the points that surprised me…

*   Cutler joined MS in Oct 88, and NT development was well underway before the decision to make NT the successor to Windows 3\. Originally OS/2 had taken that role. But the unexpected success of Windows 3 in 1990, and Microsoft’s strained relationship with IBM changed all that. Before that NT was a traditional multitasking console OS like VMS or Unix.
*   Cutler had three prime design directives: reliability, personality and portability. Reliability was achieved with a properly partitioned kernel mode, unlike DOS & Windows. Personality was accomplished by presenting a different user mode API (Win32) to apps, and keeping the kernel API private. Which much later in WinNT’s history would enable WSL version 1\. Personality also enabled Windows 3 apps to run under NT. Portability meant minimizing assembly coding.
*   Cutler original target CPU was Intel’s RISC offering, the i860\. A CPU so new and buggy that Cutler brought his hardware buddy Roy Short over from DEC to build i860 based systems at MS. Gates wanted to target 80386 first, but deferred to Cutler on many key decisions. Later support for MIPS and DEC Alpha would be added. I remember seeing Alpha based NT workstations in the mid 90s and being very impressed by the power and speed.
*   Manual builds! There was no CI/CD automation back then. The guys running the “Build Lab” selected the patches they would take, merged, and built. And the build took 19 hours.
*   Most of NT was coded in C, but much of the graphics was in C++. The graphics coders were long time Microsofties, not Cutler cronies from DEC, and they had Gates support in C++. Since Windows graphics only entered the NT picture in 1990, and Cutler was not a GUI guy, they didn’t have to follow his language choice. I remember early C++ compilers – Glockenspiel CommonView anyone? Coding part of a new OS in C++ in 1990 was a very bold choice.
*   20% of the NT team were first jobbers!

Will we ever see a big new OS dev project again? Maybe not. Cutler’s Personality idea enabled the pivot to Windows by NT, but now we have virtualization and cheap hardware, so the Personality job is done by hypervisors. Just look at WSL2 compared to WSL1! OSes have become commoditized, and since Linux is open source, it enables a style of innovation that proprietary OSes can’t match. So, in conclusion, Showstopper is a strong recommend from me, and a nostalgic read for this veteran dev. Almost a “when dinosaurs roamed the earth” experience. And Cutler may have been difficult to work with, but he obviously had massive coding chops.