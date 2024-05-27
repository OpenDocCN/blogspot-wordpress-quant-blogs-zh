<!--yml

分类：未分类

日期：2024-05-18 05:43:02

-->

# WatchKit 打包和 WKInterfaceController | 交易台的故事

> 来源：[`mdavey.wordpress.com/2015/04/10/watchkit-packaging-and-wkinterfacecontroller/#0001-01-01`](https://mdavey.wordpress.com/2015/04/10/watchkit-packaging-and-wkinterfacecontroller/#0001-01-01)

## WatchKit 打包和 WKInterfaceController

通过几个（晚上）与 Xcode 一起玩 WatchKit 应用，对于任何新的 WatchKit 开发人员都有一些有趣的经验教训：

+   通过这个[结构](https://developer.apple.com/library/ios/documentation/General/Conceptual/WatchKitProgrammingGuide/ConfiguringYourXcodeProject.html#//apple_ref/doc/uid/TP40014969-CH2-SW1)图解释了 WatchKit 应用的打包情况。故事板与实际的 WatchKit 代码（WKInterfaceController 等）是分开的。更有趣的是，但最不为人所知的是，Apple Watch 在可能的情况下也会使用 wifi，[与](http://www.raywenderlich.com/94672/watchkit-faq)默认的蓝牙 LE 一起与配对的 iPhone 进行通信。

+   动作和 [Outlets](https://developer.apple.com/library/ios/documentation/General/Conceptual/Devpedia-CocoaApp/Outlet.html) 像你期望的那样工作 - 从故事板将 UI 小部件控件拖到包含 WKInterfaceController 派生代码的[助手](http://www.raywenderlich.com/89562/watchkit-tutorial-with-swift-getting-started)编辑页面，将自动创建和绑定输出。基本上在蓝牙上创建了一个 IPC 通道到配对的 iPhone 🙂

+   如果你希望这两个进程访问相同的文件或数据（例如偏好设置），共享应用程序组是相关的。

+   [openParentApplication](https://developer.apple.com/library/prerelease/ios/documentation/WatchKit/Reference/WKInterfaceController_class/index.html#//apple_ref/occ/clm/WKInterfaceController/openParentApplication:reply:) 看起来实际上是 WatchKit 扩展沙盒进程与父 iOS 进程之间的 RPC 调用。

+   本教程提供了关于如何向你的 WatchKit 应用添加 Glances 和 Handoff 功能的[帮助](http://www.raywenderlich.com/96741/watchkit-tutorial-with-swift-tables-glances-and-handoff)。

~ 作者 mdavey，于 2015 年 4 月 10 日。

发布在 [未分类](https://mdavey.wordpress.com/category/uncategorized/) 中
