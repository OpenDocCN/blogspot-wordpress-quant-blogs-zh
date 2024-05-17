<!--yml
category: 未分类
date: 2024-05-18 05:14:45
-->

# Magmasystems Blog: Getting Started with CAB

> 来源：[http://magmasystems.blogspot.com/2006/11/getting-started-with-cab.html#0001-01-01](http://magmasystems.blogspot.com/2006/11/getting-started-with-cab.html#0001-01-01)

It looks like, for various reasons that shall accompany me to the grave, we will be bootstrapping the "top part" of our client-side framework with Microsoft's Composite Application Block. I am excited to finally be given the chance to learn CAB, and to lead the team doing the new client-side framework for my investment bank.

I will try to document my learning process with CAB so that I can save my successors some pain.

**Installation of CAB and Accessories** 

Download and install the following files in order (make sure to install GAX before installing GAT):

1)

[Download](http://www.gotdotnet.com/codegallery/releases/checkForDownload.aspx?id=22f72167-af95-44ce-a6ca-f2eafbf2653c&releaseid=e3136cf0-67dc-41aa-83ff-c10e024503af)

Composite Application Block for C# (CAB)

2)

[Download](http://msdn.microsoft.com/library/?url=/library/en-us/dnpag2/html/EntLib2.asp)

Enterprise Library 2006 (

**EntLib**

)

3)

[Download](http://www.microsoft.com/downloads/details.aspx?familyid=C0A394C0-5EEB-47C4-9F7B-71E51866A7ED&displaylang=en)

the Guidance Automation Extensions (

**GAX**

)

4)

[Download](http://www.microsoft.com/downloads/details.aspx?FamilyId=E3D101DB-6EE1-4EC5-884E-97B27E49EAAE&displaylang=en)

the Guidance Automation Toolkit (

**GAT**

)

(At this point, before installing the Smart Client Software Factory, you must build CAB using the *CompositeUI.sln* solution file located in the directory *C:\Program Files\Microsoft Composite UI App Block\CSharp*. You must also close Visual Studio before installing SCSF.) 

5)

[Download](http://www.microsoft.com/downloads/info.aspx?na=47&p=1&SrcDisplayLang=en&SrcCategoryId=&SrcFamilyId=7B9BA1A7-DD6D-4144-8AC6-DF88223AEE19&u=details.aspx%3ffamilyid%3d2B6A10F9-8410-4F13-AD53-05A202FBDB63%26displaylang%3den)

the Smart Client Software Factory (June 2006 version) (

**SCSF**

)

6)

[Download](http://www.microsoft.com/downloads/details.aspx?familyid=AB44F082-3ABE-4583-8844-7252FF7C9638&displaylang=en)

the CAB Hands-on Lab

7)

[Download](http://www.gotdotnet.com/codegallery/releases/viewuploads.aspx?id=22f72167-af95-44ce-a6ca-f2eafbf2653c)

the Intro to CAB document and the CAB help files (you might want to create shortcuts on the desktop for these files.)

8) Download the Sample Visualizations

If you have problems uninstalling GAX or GAT, read

[this](http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=525052&SiteID=1)

.

**Resources** 

· The

[CAB home](http://practices.gotdotnet.com/projects/cab)

on Microsoft Patterns and Practices area on GotDotNet

·

[CabPedia](http://www.cabpedia.com/index.php?title=Main_Page)

·

[MSDN Magazine Article](http://msdn.microsoft.com/msdnmag/issues/06/09/SmartClients/default.aspx)

·

[Getting Started with CAB](http://weblogs.asp.net/bsimser/archive/2006/07/27/Composite-UI-Application-Block-_2D00_-Soup-to-Nuts-_2D00_-Getting-Started.aspx)

on the Fear and Loathing blog

·

[Understanding CAB](http://geekswithblogs.net/kobush/archive/2006/01/06/65033.aspx)

series on Szymon’s blog

**Class Hierarchy** 

Here is a diagram of the major classes in CAB:

[![](img/d2b3afc88078cc5bbc08635e6193f61c.png)](http://photos1.blogger.com/blogger/138/258/1600/CAB%20Class%20Hierarchy.jpg)

©2006 Marc Adler - All Rights Reserved