<!--yml
category: 未分类
date: 2024-05-18 06:15:59
-->

# Silverlight 5 Beta (5.0.6401.0) Pain with IE 9 | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2011/06/02/silverlight-5-beta-5-0-6401-0-pain-with-ie-9/#0001-01-01](https://mdavey.wordpress.com/2011/06/02/silverlight-5-beta-5-0-6401-0-pain-with-ie-9/#0001-01-01)

## Silverlight 5 Beta (5.0.6401.0) Pain with IE 9

So it appear that my Silverlight 4 application work with Internet Explorer 9 (9.0.8112.16421), Google Chrome (11.0.696.71) and Firefox (4.0b12). But when I install Silverlight 5 beta (5.0.6401.0), and re-test with the three browsers, IE9 experiences some issues with the network stack. Visual Studio 2010 shows me this when processing a response from a POST ([http://localhost:9000](http://localhost:9000)):

```

'iexplore.exe' (Silverlight): Loaded 'c:\Program Files (x86)\Microsoft Silverlight\5.0.60401.0\en-US\System.Windows.debug.resources.dll'
A first chance exception of type 'System.Net.WebException' occurred in System.Windows.dll

```

Breaking on System.Net.WebException using VS2010 shows:

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

So leveraging VS2010 .NET Reflector 7 add-on, I can “Explore Decompiled Assembly” for SL5 runtime and find where the exception is throw:

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

~ by mdavey on June 2, 2011.

Posted in [.NET](https://mdavey.wordpress.com/category/languages/net/)
Tags: [Microsoft](https://mdavey.wordpress.com/tag/microsoft/)