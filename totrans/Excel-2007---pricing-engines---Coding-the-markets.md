<!--yml
category: 未分类
date: 2024-05-12 19:52:04
-->

# Excel 2007 & pricing engines | Coding the markets

> 来源：[https://etrading.wordpress.com/2006/07/27/excel-2007-pricing-engines/#0001-01-01](https://etrading.wordpress.com/2006/07/27/excel-2007-pricing-engines/#0001-01-01)

## Excel 2007 & pricing engines

### July 27, 2006

I went to the Office 2007 event at Credit Suisse on Tuesday night. Jim Burns, CTO financial services Microsoft UK opened the event. A CSFBer called Leslie spoke for a few minutes. He announced he worked for R&D in CSFB, that they identified emerging trends for the next 3 to 5 years, and that virtualisation and MS Office 2007’s distributed work features were the coming things. Then Ian Moulster, Product Manager for the Dev & Platform Group in MS UK spoke briefly. Then finally, we got the meat in the sandwich, an hour long presentation by Paul Foster, Developer Evangelist on Excel Services and InfoPath.

Excel Services is based on Sharepoint, which seems to provide some app server like hosting of the all new Excel Server calculation engine. Excel Server hosted worksheets can be rendered in a browser, and support interaction using AJAX techniques. Excel Server hosted worksheets can be invoked programmatically from a client using a web services API too. Paul alluded to [XLLs](https://etrading.wordpress.com/excel/) a couple of times. I asked him about them afterwards. From the [Excel 12 blog](http://blogs.msdn.com/excel), it looks like [C/C++ XLLs on a client Excel](http://blogs.msdn.com/excel/archive/2006/01/03/508985.aspx) will be similar. However, a server side XLL, running under Excel services, [must be managed code](http://blogs.msdn.com/excel/archive/2006/05/03/589094.aspx), though unmanaged code can be wrapped. When I asked Paul about injection of real time data into a server side worksheet, he indicated that my [DDE based technique](https://etrading.wordpress.com/excel/) wouldn’t work for Excel services, as Windows permissioning would disallow it. And now the [cumgranosalis](http://blogs.msdn.com/cumgranosalis) blog tells us that [RTD doesn’t really work for Excel services](http://blogs.msdn.com/cumgranosalis/archive/2006/05/23/RTDPart1.aspx).

Why is this a problem ? It’s not unknown for traders to implement ad hoc pricing engines in Excel. I’ve worked on an Excel based system that autoquoted exchange traded option strategies. The recalcs were driven by a real time feed of futures prices – the future being the underlying for the options. We injected the futures price with DDE. It’s looking like it won’t be possible to implement this kind of system with Excel services, which is a great pity.