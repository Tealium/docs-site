---
title: Webviewsの追跡
description: JavaScriptインターフェースを使用して、アプリ内のwebviewからイベントを追跡する方法を学びます。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/tracking-webviews/
---
ネイティブアプリは、webviewと呼ばれる組み込みブラウザに機能を委任してWebコンテンツを表示することができます。TealiumのiOSまたはAndroid SDKでwebviewからイベントを追跡するには、ネイティブコードへの通信ブリッジが必要です。これは、JavaScriptを使用してアプリにメッセージを送信することでネイティブコードを呼び出すことによって行われます。

このソリューションは、Tealium Universal Tag（utag.js）がインストールされているかどうかに関係なく、webviewsで動作します。

## 仕組み

このソリューションは以下のコンポーネントを使用します：

* **Webview JavaScriptハンドラ**  
このJavaScriptコードは、webベースのイベント追跡をラップして、イベントをネイティブアプリに送信します。
    * Tealium iQタグ管理を使用 - 拡張機能を使用してこのコードをページに迅速に追加します。
    * Tealiumを使用しない場合 - 既存のイベント追跡を使用するか、ページに追跡を追加します。
* **ネイティブメッセージハンドラ**  
このネイティブコードは、イベントデータを含むメッセージを受信するためのJavaScriptインターフェースを使用します。

## Webview JavaScriptハンドラ

以下のJavaScriptコードは、ビューの追跡とイベントの追跡のための2つのラッパー関数を提供し、webベースの追跡呼び出しをネイティブコードに転送します。このコードはiOSとAndroidで動作します。

```javascript
function tealView(tealiumEvent, data) {
  if (!tealiumEvent) {
    return;
  }
  if (window.WebViewInterface) {
    window.WebViewInterface.trackView(tealiumEvent, JSON.stringify(data));
  } else if (window.webkit
      &amp;&amp; window.webkit.messageHandlers
      &amp;&amp; window.webkit.messageHandlers.tealium) {
    var message = {
      command: &#39;trackView&#39;,
      title: tealiumEvent,
      data: data
    };
    window.webkit.messageHandlers.tealium.postMessage(message);
  }
}

function tealEvent(tealiumEvent, data) {
  if (!tealiumEvent) {
    return;
  }
  if (window.WebViewInterface) {
    window.WebViewInterface.trackEvent(tealiumEvent, JSON.stringify(data));
  } else if (window.webkit
      &amp;&amp; window.webkit.messageHandlers
      &amp;&amp; window.webkit.messageHandlers.tealium) {
    var message = {
      command: &#39;track&#39;,
      title: tealiumEvent,
      data: data
    };
    window.webkit.messageHandlers.tealium.postMessage(message);
  }
}
```

### Tealium付きのWebview

webviewでロードされるページにすでにTealium Universal Tag（`utag.js`）がある場合、JavaScriptハンドラコードを2つの[JavaScript Code extensions]()を使用して追加します：一つはラッパー関数を初期化し、もう一つは既存の追跡呼び出しをJavaScriptインターフェースに転送します。

このシナリオでは、webviewのページとネイティブアプリは異なるTealium iQプロファイルを使用しなければなりません。

1. [JavaScriptハンドラコード](#webview-javascript-handler)を**Pre Loader**の範囲にあるJavaScript Code extensionに追加します。
2. 以下のコードを**All Tags - After Tags**の範囲にある2つ目のJavaScript Code extensionに追加します。これにより、webview内で既に発生しているTealiumの追跡呼び出しをネイティブのホストアプリに転送します。

    ```javascript
    if (a == &#34;view&#34;) {
      tealView(b.tealium_event, b);
    } else if (a == &#34;link&#34;) {
      tealEvent(b.tealium_event, b);
    }
    ```

### TealiumなしのWebview

webviewでロードされるページにTealiumがない場合、JavaScriptハンドラコードをwebview内でロードされる各ページに追加します。その後、ページビューを追跡するために`tealView`を呼び出し、ボタンクリックやカートイベントなどの非ページビューイベントが発生したときに`tealLink`を呼び出します。

## ネイティブメッセージハンドラ




JavaScriptからネイティブのAndroidコードを呼び出すには、[`@JavaScriptInterface`](https://developer.android.com/reference/android/webkit/JavascriptInterface)でマークされたメソッドを持つクラスを実装します：

```java
public class WebViewInterface {

    @JavascriptInterface
    public void trackView(String viewName, String data) throws JSONException {
	    tealium.track(viewName, new JSONObject(data));
    }

    @JavascriptInterface
    public void trackEvent(String eventName, String data) throws JSONException {
    	tealium.track(eventName, new JSONObject(data));
    }
}
```

ネイティブインターフェースが作成されたら、それを`WebView`に登録して、`WebView`で実行されているJavaScriptコードから見えるようにします。

```java
mWebView.addJavascriptInterface(mInterface, &#34;WebViewInterface&#34;);
```

[`addJavascriptInterface()`](https://developer.android.com/reference/android/webkit/WebView.html#addJavascriptInterface(java.lang.Object,%20java.lang.String))メソッドを`webView.loadUrl()`メソッドを呼び出す前に呼び出します。また、セキュリティ上の懸念から、[`JavaScriptInterface`](https://developer.android.com/reference/android/webkit/WebView#addJavascriptInterface(java.lang.Object,%20java.lang.String))をAPIバージョンJELLY_BEAN_MR1以降にのみ追加します。




WebViewのユーザー[content controller](https://developer.apple.com/documentation/webkit/wkusercontentcontroller)に以下のメッセージハンドラを追加します：

```swift
webView.configuration.userContentController.add(self, name: &#34;tealium&#34;)
```

JavaScriptからネイティブのiOSコードを呼び出すには、[`WKScriptMessageHandler`](https://developer.apple.com/documentation/webkit/wkscriptmessagehandler)プロトコルに準拠したメッセージハンドラクラスを作成します。追跡のために、[`userContentController:didReceive:`](https://developer.apple.com/documentation/webkit/wkscriptmessagehandler/1396222-usercontentcontroller)コールバック内で[`Tealium.track`](/ja/platforms/ios-swift/track/)を呼び出します：

```swift
func userContentController(_ userContentController: WKUserContentController,
                          didReceive message: WKScriptMessage) {

  guard let body = message.body as? [String: Any],
      let command = body[&#34;command&#34;] as? String,
      let title = body[&#34;title&#34;] as? String,
      let webViewData = body[&#34;data&#34;] as? [String: Any] else {
          return
  }

  switch command {
  case &#34;track&#34;:
      TealiumHelper.shared.tealium?.track(title: title,
                                          data: webViewData,
                                          completion: nil)
  case &#34;trackView&#34;:
      TealiumHelper.shared.tealium?.trackView(title: title,
                                              data: webViewData,
                                              completion: nil)
  default:
      break
  }
}
```






## サポートされているライブラリ

以下のプラットフォームはJavaScriptインターフェースソリューションをサポートしています：

* [Tealium for Android](/ja/platforms/android-java/)
* [Tealium for iOS](/ja/platforms/ios-swift/)
