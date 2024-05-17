<!--yml
category: 未分类
date: 2024-05-18 05:12:27
-->

# Magmasystems Blog: Syncfusion GridControl vs GroupingGrid

> 来源：[http://magmasystems.blogspot.com/2007/02/syncfusion-gridcontrol-vs-groupinggrid.html#0001-01-01](http://magmasystems.blogspot.com/2007/02/syncfusion-gridcontrol-vs-groupinggrid.html#0001-01-01)

I am starting to write the grid abstraction for my client-side framework. Developers will code to a "virtual grid" API, and there will be adapters for the actual implementations of the grids (Syncfusion, Infragistics, WinForms, DevExpress, etc).

Because most of Wall Street uses Syncfusion grids for trading apps, this is the first adapter that I need to write.

Syncfusion has 3 different grids: the regular old GridControl, the DataBoundGrid, and the GroupingGrid. The grouping grid is used a lot in my place to provides rollups of data. You would think that the GroupingGrid would inherit from the GridControl, but unbelievably, it does not. The API sets are not even consistent.

I have spent my time using Lutz Roeder's very excellent Reflector to try to hunt and peck through the Syncfusion class hierarchy in search of the various classes and functions in the GroupingGrid that implement the same functionality as the GridControl. The fact that I am dealing with two incompatible API sets has increased my work by 100%.

C'mon Syncfusion ... you should know better than that!

©2007 Marc Adler - All Rights Reserved