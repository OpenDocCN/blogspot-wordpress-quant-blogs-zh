<!--yml

类别：未分类

日期：2024-05-18 06:15:59

-->

# Silverlight 5 Beta (5.0.6401.0)与 IE 9 的困扰 | 从交易台传来的故事

> 来源：[`mdavey.wordpress.com/2011/06/02/silverlight-5-beta-5-0-6401-0-pain-with-ie-9/#0001-01-01`](https://mdavey.wordpress.com/2011/06/02/silverlight-5-beta-5-0-6401-0-pain-with-ie-9/#0001-01-01)

## Silverlight 5 Beta (5.0.6401.0)与 IE 9 一起的困扰

所以看起来我的 Silverlight 4 应用程序可以与 Internet Explorer 9 (9.0.8112.16421)、Google Chrome (11.0.696.71)和 Firefox (4.0b12)一起工作。但是当我安装了 Silverlight 5 beta (5.0.6401.0)后，再次用这三个浏览器进行测试，IE9 在网络堆栈上出现了一些问题。当我用 Visual Studio 2010 处理一个来自 POST 请求的响应时（[`localhost:9000`](http://localhost:9000)），它显示了这个问题：

```

'iexplore.exe' (Silverlight): Loaded 'c:\Program Files (x86)\Microsoft Silverlight\5.0.60401.0\en-US\System.Windows.debug.resources.dll'
A first chance exception of type 'System.Net.WebException' occurred in System.Windows.dll

```

在 Visual Studio 2010 中 Breaking on System.Net.WebException 显示：

```

System.Windows.dll!System.Net.Browser.BrowserHttpWebRequest.EndGetResponse(System.IAsyncResult asyncResult) + 0x13b bytes

System.Net.WebException occurred
  Message=The remote server returned an error: NotFound.
  StackTrace:
       at
System.Net.Browser.BrowserHttpWebRequest.EndGetResponse(IAsyncResult
asyncResult)
  InnerException:

```

所以利用 VS2010 的.NET Reflector 7 插件，我可以为 SL5 运行时“探索反编译程序”：

```

    [SecuritySafeCritical]
    public override WebResponse EndGetResponse(IAsyncResult asyncResult)
    {
      if (XcpImports.OnMainThread())
      {
        return this.InternalEndGetResponse(asyncResult);
      }
      WebResponse response = null;
      AsyncHelper.BeginOnUI(delegate (object sendState) {
        response = this.InternalEndGetResponse(asyncResult);
      }, null);
      if (response == null)
      {
        this._response = new BrowserHttpWebResponse(this._method, this._reqUri, HttpStatusCode.NotFound, &quot;&quot;, null);
        throw new WebException(Resx.GetString(&quot;HttpWebRequest_WebException_RemoteServer&quot;, new object[] { HttpStatusCode.NotFound.ToString() }), null, WebExceptionStatus.UnknownError, this._response);
      }
      return response;
    }

```

~ mdavey 于 2011 年 6 月 2 日。

发布在[.NET](https://mdavey.wordpress.com/category/languages/net/)类别下

标签：[Microsoft](https://mdavey.wordpress.com/tag/microsoft/)
