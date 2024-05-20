<!--yml
category: 未分类
date: 2024-05-18 05:43:02
-->

# WatchKit Packaging and WKInterfaceController | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/04/10/watchkit-packaging-and-wkinterfacecontroller/#0001-01-01](https://mdavey.wordpress.com/2015/04/10/watchkit-packaging-and-wkinterfacecontroller/#0001-01-01)

## WatchKit Packaging and WKInterfaceController

Having spent the last few (late) night with Xcode playing with WatchKit apps, there are a few interesting takeaways for any new WatchKit developers:

*   Packaging of WatchKit apps is nicely explained by this diagram – target [structure](https://developer.apple.com/library/ios/documentation/General/Conceptual/WatchKitProgrammingGuide/ConfiguringYourXcodeProject.html#//apple_ref/doc/uid/TP40014969-CH2-SW1).   The storyboards are separate from the actual WatchKit code (WKInterfaceController etc).  More interestingly, and least well publicised is the fact that Apple Watch also uses wifi if possible, [together](http://www.raywenderlich.com/94672/watchkit-faq) with the default Bluetooth LE to communicate with its paired iPhone.
*   Actions and [Outlets](https://developer.apple.com/library/ios/documentation/General/Conceptual/Devpedia-CocoaApp/Outlet.html) work as you’d expect – Control-Drag the UI widget from the storyboard into the [Assistant](http://www.raywenderlich.com/89562/watchkit-tutorial-with-swift-getting-started) editor page that contains the WKInterfaceController derived code, and the outlet will automatically be created and bound.  Essentially creating an IPC channel over Bluetooth to the paired iPhone 🙂
*   Shared app group’s are relevant if you want the two processes to access the same files or data (e.g. preference)
*   [openParentApplication](https://developer.apple.com/library/prerelease/ios/documentation/WatchKit/Reference/WKInterfaceController_class/index.html#//apple_ref/occ/clm/WKInterfaceController/openParentApplication:reply:) looks like effectively an RPC call between the WatchKit extension sandbox process and the parent iOS process.
*   This tutorial offers [assistance](http://www.raywenderlich.com/96741/watchkit-tutorial-with-swift-tables-glances-and-handoff) on adding Glances and Handoff functionality to your WatchKit app.

~ by mdavey on April 10, 2015.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)