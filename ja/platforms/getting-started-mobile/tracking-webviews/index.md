---
title: Webviewのトラッキング
description: JavaScriptインターフェイスを使用して、アプリ内Webviewからイベントをトラッキングする方法について説明します。
url: https://docs.tealium.com/ja/platforms/getting-started-mobile/tracking-webviews/
---
ネイティブアプリでは、Webコンテンツを表示し、Webviewと呼ばれる埋め込みブラウザーに機能を委任できます。Tealium iOSまたはAndroid SDKでWebviewからイベントをトラッキングするには、ネイティブコードとの通信ブリッジが必要です。これは、JavaScriptを使用してアプリにメッセージを送信し、ネイティブコードを呼び出すことで実現します。


<blockquote>
このソリューションは、Tealium Universal Tag（utag.js）がインストールされているかどうかにかかわらず、Webviewで動作します。
</blockquote>


## 仕組み

このソリューションでは、次のコンポーネントを使用します。

* **Webview JavaScriptハンドラー**  
このJavaScriptコードは、Webベースのイベントトラッキングをラップし、イベントをネイティブアプリに送信します。
    * タグ管理を使用する場合 - 拡張機能を使用して、このコードをページにすばやく追加します。
    * Tealiumを使用しない場合 - 既存のイベントトラッキングを使用するか、ページにトラッキングを追加します。
* **ネイティブメッセージハンドラー**  
このネイティブコードは、JavaScriptインターフェイスを使用してイベントデータを含むメッセージを受信します。

## Webview JavaScriptハンドラー

次のJavaScriptコードには、Webベースのトラッキング呼び出しをネイティブコードに転送するために、ビューのトラッキング用とイベントのトラッキング用の2つのラッパー関数が用意されています。このコードはiOSとAndroidの両方で動作します。

```javascript
function tealView(tealiumEvent, data) {
  if (!tealiumEvent) {
    return;
  }
  if (window.WebViewInterface) {
    window.WebViewInterface.trackView(tealiumEvent, JSON.stringify(data));
  } else if (window.webkit
      && window.webkit.messageHandlers
      && window.webkit.messageHandlers.tealium) {
    var message = {
      command: 'trackView',
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
      && window.webkit.messageHandlers
      && window.webkit.messageHandlers.tealium) {
    var message = {
      command: 'track',
      title: tealiumEvent,
      data: data
    };
    window.webkit.messageHandlers.tealium.postMessage(message);
  }
}
```

### Tealiumを使用するWebview

Webviewに読み込まれるページにTealium Universal Tag（`utag.js`）がすでに含まれている場合は、2つの[JavaScriptコード拡張機能](https://docs.tealium.com/advanced-javascript-code-extension/)を使用してJavaScriptハンドラーコードを追加します。一方はラッパー関数を初期化するため、もう一方は既存のトラッキング呼び出しをJavaScriptインターフェイスに転送するために使用します。


<blockquote>
このシナリオでは、Webviewページとネイティブアプリで異なるタグ管理プロファイルを使用する必要があります。
</blockquote>


1. [JavaScriptハンドラーコード](#webview-javascript-handler)を、**Pre Loader**をスコープとするJavaScriptコード拡張機能に追加します。
2. 次のコードを、**All Tags - After Tags**をスコープとする2つ目のJavaScriptコード拡張機能に追加します。これにより、Webview内ですでに発生している既存のTealiumトラッキング呼び出しが、ネイティブホストアプリに転送されます。

    ```javascript
    if (a == "view") {
      tealView(b.tealium_event, b);
    } else if (a == "link") {
      tealEvent(b.tealium_event, b);
    }
    ```

### Tealiumを使用しないWebview

Webviewに読み込まれるページにTealiumが含まれていない場合は、Webview内に読み込まれる各ページにJavaScriptハンドラーコードを追加します。その後、ページビューをトラッキングするには`tealView`を呼び出し、ボタンのクリックやカートイベントなど、ページビュー以外のイベントが発生した場合は`tealLink`を呼び出します。

## ネイティブメッセージハンドラー




JavaScriptからAndroidのネイティブコードを呼び出すには、[`@JavaScriptInterface`](https://developer.android.com/reference/android/webkit/JavascriptInterface)でマークされたメソッドを持つクラスを実装します。

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

ネイティブインターフェイスを作成したら、それを`WebView`に登録し、`WebView`内で実行されるJavaScriptコードから参照できるようにします。

```java
mWebView.addJavascriptInterface(mInterface, "WebViewInterface");
```


<blockquote>
[`addJavascriptInterface()`](https://developer.android.com/reference/android/webkit/WebView.html#addJavascriptInterface(java.lang.Object,%20java.lang.String))メソッドは、`webView.loadUrl()`メソッドを呼び出す前に呼び出してください。また、セキュリティ上の理由から、[`JavaScriptInterface`](https://developer.android.com/reference/android/webkit/WebView#addJavascriptInterface(java.lang.Object,%20java.lang.String))はAPIバージョンJELLY_BEAN_MR1以降でのみ追加してください。
</blockquote>





WebViewのユーザー[コンテンツコントローラー](https://developer.apple.com/documentation/webkit/wkusercontentcontroller)に、次のメッセージハンドラーを追加します。

```swift
webView.configuration.userContentController.add(self, name: "tealium")
```

JavaScriptからiOSのネイティブコードを呼び出すには、[`WKScriptMessageHandler`](https://developer.apple.com/documentation/webkit/wkscriptmessagehandler)プロトコルに準拠するメッセージハンドラークラスを作成します。トラッキングするには、[`userContentController:didReceive:`](https://developer.apple.com/documentation/webkit/wkscriptmessagehandler/1396222-usercontentcontroller)コールバック内で[`Tealium.track`](https://docs.tealium.com/ja/platforms/ios-swift/track/)を呼び出します。

```swift
func userContentController(_ userContentController: WKUserContentController,
                          didReceive message: WKScriptMessage) {

  guard let body = message.body as? [String: Any],
      let command = body["command"] as? String,
      let title = body["title"] as? String,
      let webViewData = body["data"] as? [String: Any] else {
          return
  }

  switch command {
  case "track":
      TealiumHelper.shared.tealium?.track(title: title,
                                          data: webViewData,
                                          completion: nil)
  case "trackView":
      TealiumHelper.shared.tealium?.trackView(title: title,
                                              data: webViewData,
                                              completion: nil)
  default:
      break
  }
}
```






## サポートされているライブラリ

次のプラットフォームでは、JavaScriptインターフェイスソリューションがサポートされています。

* [Tealium for Android](https://docs.tealium.com/ja/platforms/android-java/)
* [Tealium for iOS](https://docs.tealium.com/ja/platforms/ios-swift/)