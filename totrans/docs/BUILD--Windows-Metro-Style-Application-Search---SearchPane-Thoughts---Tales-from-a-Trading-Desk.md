<!--yml
category: 未分类
date: 2024-05-18 06:16:42
-->

# BUILD: Windows Metro Style Application Search – SearchPane Thoughts | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2011/09/15/build-windows-metro-style-application-search-searchpane-thoughts/#0001-01-01](https://mdavey.wordpress.com/2011/09/15/build-windows-metro-style-application-search-searchpane-thoughts/#0001-01-01)

## BUILD: Windows Metro Style Application Search – SearchPane Thoughts

So your building a Metro style Windows application – is C# still you language of choice?. Within the VS2011 project there is now a new file, Package.appxmanifest, that allows the setting of applications [metadata](http://msdn.microsoft.com/en-us/library/windows/apps/br211380#specifying_app_capabilities). Here’s why you need to specify meta data:

> A Metro style app runs in a security container with limited access to the file system, network resources, and hardware. Whenever a user installs an app from the Windows Store, Windows looks at the metadata in the Package.appxmanifest file to figure out what capabilities the app needs to function. For example, an app might need to access data from the Internet, documents from the user’s Document Library, or the user’s webcam and microphone. When the app is installed, it displays to the user the capabilities it needs, and the user must grant permission for it to access those resources. If the app doesn’t request and receive access to a resource it needs, it will not be allowed access to that resource when the user runs it.

Additionally, we can specify metadata declarations. Search is one such declaration. If you browser over to [here](http://code.msdn.microsoft.com/windowsapps/Search-app-extension-sample-6baa6270/sourcecode?fileId=43964&pathId=298223712) you’ll see an example of how to integrate you application into Search. Basically hooking into [Windows.ApplicationModel.Search.SearchPane](http://msdn.microsoft.com/en-us/library/windows/apps/windows.applicationmodel.search.searchpane). What’s very cool about this is that the Windows 8 search can now do searches into your applications. Take the [default](http://www.guardian.co.uk/technology/2011/sep/13/windows-metro-microsoft-tablet-apps) Window 8 Metro interface with the Stocks and News applications running. Imagine if I entered “Vodafone” in the Windows 8 search. Effectively I could search/restrict the stocks in the Stocks application, and see only the news on Vodafone in the News application. Very cool

~ by mdavey on September 15, 2011.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)