---
title: Tracking Webviews
description: Learn how to track events from an in-app webview using a JavaScript interface.
url: https://docs.tealium.com/platforms/getting-started-mobile/tracking-webviews/
---
A native app can display web content and delegate functionality to an embedded browser called a webview. To track events from a webview in the Tealium iOS or Android SDK you need a communication bridge to the native code. This is done using JavaScript to invoke native code by sending messages to your app.


<blockquote>
This solution works in webviews _with or without_ the Tealium Universal Tag (utag.js) installed.
</blockquote>


## How It Works

This solution uses the following components:

* **Webview JavaScript Handler**  
This JavaScript code is a wrapper around your web-based event tracking to send the events to the native app.
    * With Tealium iQ Tag Management - Use extensions to quickly add this code to your pages.
    * Without Tealium - Use existing event tracking or add tracking to the pages.
* **Native Message Handler**  
This native code uses a JavaScript interface to receive the messages containing the event data.

## Webview JavaScript Handler

The following JavaScript code provides two wrapper functions, one for tracking views and one for tracking events, to forward a web-based tracking call to the native code. This code works for iOS and Android.

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

### Webview With Tealium

If the pages loaded in the webview already have the Tealium Universal Tag (`utag.js`), then add the JavaScript handler code using two [JavaScript Code extensions](https://docs.tealium.com/advanced-javascript-code-extension/): one to initialize the wrapper functions and one to forward existing tracking calls to the JavaScript interface.


<blockquote>
In this scenario the webview pages and the native app must be using different Tealium iQ profiles.
</blockquote>


1. Add the [JavaScript handler code](#webview-javascript-handler) to a JavaScript Code extension scoped to **Pre Loader**.
2. Add the following code to a second JavaScript Code extension scoped to **All Tags - After Tags**. This forwards the existing Tealium tracking calls, already occuring in the webview, to the native host app.

    ```javascript
    if (a == "view") {
      tealView(b.tealium_event, b);
    } else if (a == "link") {
      tealEvent(b.tealium_event, b);
    }
    ```

### Webview Without Tealium

If the pages loaded in the webview do not have Tealium, then add the JavaScript handler code to each page that loads inside a webview. Then call `tealView` to track page views and `tealLink` when a non-page view event occurs, such as a button click or cart event.

## Native Message Handler




To invoke native Android code from JavaScript, implement a class with methods marked [`@JavaScriptInterface`](https://developer.android.com/reference/android/webkit/JavascriptInterface):

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

Once the native interface is created, register it with your `WebView` to make it visible to JavaScript code running in the `WebView`.

```java
mWebView.addJavascriptInterface(mInterface, "WebViewInterface");
```


<blockquote>
Call the method [`addJavascriptInterface()`](https://developer.android.com/reference/android/webkit/WebView.html#addJavascriptInterface(java.lang.Object,%20java.lang.String)) prior to calling the `webView.loadUrl()` method. Also, due to security concerns, only add the [`JavaScriptInterface`](https://developer.android.com/reference/android/webkit/WebView#addJavascriptInterface(java.lang.Object,%20java.lang.String)) on API version JELLY_BEAN_MR1 and above.
</blockquote>





Add the following message handler to the WebView's user [content controller](https://developer.apple.com/documentation/webkit/wkusercontentcontroller):

```swift
webView.configuration.userContentController.add(self, name: "tealium")
```

To invoke native iOS code from JavaScript, create a message handler class conforming to the [`WKScriptMessageHandler`](https://developer.apple.com/documentation/webkit/wkscriptmessagehandler) protocol. For tracking, call [`Tealium.track`](https://docs.tealium.com/platforms/ios-swift/track/) inside the [`userContentController:didReceive:`](https://developer.apple.com/documentation/webkit/wkscriptmessagehandler/1396222-usercontentcontroller) callback:

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






## Supported Libraries

The following platforms support the JavaScript interface solution:

* [Tealium for Android](https://docs.tealium.com/platforms/android-java/)
* [Tealium for iOS](https://docs.tealium.com/platforms/ios-swift/)
