<!--yml

类别：未分类

日期：2024-05-18 06:16:42

-->

# BUILD: Windows Metro Style 应用搜索 – SearchPane 思考 | 来自交易台的故事

> 来源：[`mdavey.wordpress.com/2011/09/15/build-windows-metro-style-application-search-searchpane-thoughts/#0001-01-01`](https://mdavey.wordpress.com/2011/09/15/build-windows-metro-style-application-search-searchpane-thoughts/#0001-01-01)

## BUILD: Windows Metro Style 应用搜索 – SearchPane 思考

所以你正在构建一个 Metro 风格的 Windows 应用程序 – C# 仍然是你的首选语言吗？在 VS2011 项目中，现在有一个新文件，Package.appxmanifest，允许设置应用程序的 [元数据](http://msdn.microsoft.com/en-us/library/windows/apps/br211380#specifying_app_capabilities)。这就是为什么你需要指定元数据的原因：

> 一个 Metro 风格的应用程序在安全容器中运行，对文件系统、网络资源和硬件的访问受到限制。每当用户从 Windows 商店安装应用程序时，Windows 会查看 Package.appxmanifest 文件中的元数据，以确定应用程序需要的功能。例如，一个应用程序可能需要访问来自互联网的数据、用户文档库中的文档，或用户的网络摄像头和麦克风。当应用程序安装时，它会向用户显示它需要的功能，并且用户必须授予其访问这些资源的权限。如果应用程序没有请求并获得它需要的资源的访问权限，则用户在运行它时将不允许访问该资源。

此外，我们可以指定元数据声明。搜索就是其中之一。如果你浏览到[这里](http://code.msdn.microsoft.com/windowsapps/Search-app-extension-sample-6baa6270/sourcecode?fileId=43964&pathId=298223712)，你会看到一个集成你应用程序到搜索的示例。基本上就是钩入[Windows.ApplicationModel.Search.SearchPane](http://msdn.microsoft.com/en-us/library/windows/apps/windows.applicationmodel.search.searchpane)。这非常酷的一点是 Windows 8 搜索现在可以搜索你的应用程序。拿 Windows 8 的默认 Metro 界面和运行的股票和新闻应用程序为例。想象一下如果我在 Windows 8 搜索中输入“Vodafone”。实际上我可以搜索/限制股票应用程序中的股票，并在新闻应用程序中只看到有关 Vodafone 的新闻。非常酷。

~ 由 mdavey 于 2011 年 9 月 15 日发布。

发表在 [未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签：[微软](https://mdavey.wordpress.com/tag/microsoft/)
