<!--yml
category: 未分类
date: 2024-05-18 04:49:19
-->

# Magmasystems Blog: .NET Parallelism and a Worthy Cause

> 来源：[http://magmasystems.blogspot.com/2011/10/net-parallelism-and-worthy-cause.html#0001-01-01](http://magmasystems.blogspot.com/2011/10/net-parallelism-and-worthy-cause.html#0001-01-01)

A

[fascinating case study](http://www.microsoft.com/casestudies/Microsoft-Visual-Studio-2010/Massachusetts-General-Hospital/Parallelization-of-Native-C-Code-Helps-Reduce-3-D-Image-Processing-Times-by-a-Factor-of-20/4000010935)

is available from Microsoft on how Massachusetts General Hospital (MGH) greatly reduced the time (and cost) to analyze the results from a colonoscopy. For men over 50, a colonoscopy is practically mandatory, and the process is somewhat disruptive and uncomfortable. The use of parallelism has reduced the analysis time by many orders of magnitude, and has made the concept of "virtual colonoscopies" even more real.

Microsoft had pushed MGH to port its code to C#, but for a variety of reasons, this was impossible. I wonder if there would have been even more magnitude of improvements if the code was ported.

Bringing this to capital markets, companies might find that their real-time pricing and risk (and stress tests) might benefit from a rearchitecture to the .NET/C#/TPL stack.

©2011 Marc Adler - All Rights Reserved. All opinions here are personal, and have no relation to my employer.