在 Android 和 iOS 系统中，Webview 都提供了相关的方法来监听网页加载的状态，以便在加载完成后进行相应的处理。具体如下：

1. Android 系统，Webview 提供了一个 WebViewClient 类，该类中有一个 onPageFinished() 方法，该方法会在网页加载完成后被调用。

示例代码：

```
webView.setWebViewClient(new WebViewClient() {
  @Override
  public void onPageFinished(WebView view, String url) {
    // TODO: 网页加载完成后的处理
  }
});
```

1. iOS 系统，Webview 提供了一个 UIWebViewDelegate 协议，该协议中有一个在网页加载完成后被调用的方法 webViewDidFinishLoad()。

示例代码：

```
- (void)webViewDidFinishLoad:(UIWebView *)webView {
  // TODO: 网页加载完成后的处理
}
```

需要注意的是，在使用 Webview 加载网页时，如果对网页的加载状态进行了监听，在加载完成前不要进行与网页相关的任何操作，以防止出现异常。
