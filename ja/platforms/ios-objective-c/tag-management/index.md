---
title: タグ管理
description: Universal Tag（utag.js）JavaScript をクライアント側で実行するために、タグ管理がレンダリングされない WKWebView インスタンスとして実装される仕組みについて説明します。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/tag-management/
---
このタグ管理機能を使用すると、JavaScript ベースのベンダータグをアプリに統合し、Web サイトと同様に、タグ管理を使用してリモートで管理できます。

## 仕組み

タグ管理を有効にして[タグ管理でモバイルプロファイルを作成](https://docs.tealium.com/create-mobile-profile/)した後、アプリで Tealium インスタンスを初期化すると、Universal Tag `utag.js` を読み込むための Tealium のシンプルな HTML ファイルをロードする、レンダリングされない Web ビューが作成されます。この Web ビューがユーザーに表示されることはありません。

* iOS 11.0 以降で動作するバージョン 5.5.0 以降では、[WKWebView](https://developer.apple.com/documentation/webkit/wkwebview?language=objc) を使用します。
* iOS 10.0 以前で動作するバージョン 5.4.x 以前では、[UIWebView](https://developer.apple.com/documentation/uikit/uiwebview) を使用します。


<blockquote>
iOS 11.0 より前のバージョンをサポートしながら WKWebView を使用する場合は、バージョン 5.5.0 以降にアップグレードしてください。ただし、visitor_id およびその他の Cookie はリセットされます。これは、[WKHTTPCookieStore](https://developer.apple.com/documentation/webkit/wkhttpcookiestore) が iOS 11.0 以降でのみサポートされているためです。
</blockquote>


### サンプル

Tealium の `WKWebView` について詳しく理解するには、[WKWebView サンプル](https://github.com/Tealium/tealium-ios/tree/master/Samples/iOS_WKWebView%2BTealium_Objc)を参照してください。

### 使用方法

`WKWebView` は、レンダリングされない場合でも `UIView` にアタッチする必要があります。これに対応するため、Tealium SDK は、レンダリングされない `WKWebView` を `rootViewController.view` にアタッチしようとします。これは、ウィンドウの `rootViewController` が `UIViewController` のサブクラス、または Apple のコンテナビューコントローラー（`UINavigationController` または `UITabBarController`）である場合の最も一般的な構成です。

アプリに複雑なビュー階層がある場合は、`viewDidLoad`、`viewWillAppear:`、または `viewDidAppear:` で、アタッチ先のビューを `TEALConfiguration` インスタンスに構成します。

```obj-c
TEALConfiguration *tealConfig = [TEALConfiguration configurationWithAccount:@"ACCOUNT"
                                              profile:@"PROFILE"
                                              environment:@"ENVIRONMENT"
                                              datasource:@"DATASOURCE"];
tealConfig.view = <UIVIEW>; // For example, self.view in a UIViewController subclass
// Initialize with a unique key for this instance
Tealium *tealium = [Tealium newInstanceForKey:@"INSTANCE" configuration:tealConfig]; 
```

| パラメータ | 型 | 説明 | 例 |
|:--------------|:---------|:---------------------------------------------------|:---------------|
| `account`     | `String` | Tealium アカウント名 | `"companyXYZ"` |
| `profile`     | `String` | Tealium プロファイル名 | `"main" `      |
| `environment` | `String` | Tealium 環境名 | `"prod"`       |
| `datasource`  | `String` | （任意）データソースキー（ない場合は `null` に構成） | `"abc123"`     |

プッシュ通知を受信した際、アプリが `UIViewController` に遷移し、Tealium の初期化時とは異なるビュー階層になる場合は、古い Tealium インスタンスを削除し、アタッチ先のビューを指定して新しいインスタンスを作成する必要があります。サンプルアプリの [`GreenViewController.m`](https://github.com/Tealium/tealium-ios/blob/master/Samples/iOS_WKWebView%2BTealium_Objc/iOS_WKWebView%2BTealium_Objc/GreenViewController.m) および [TealiumHelper.m](https://github.com/Tealium/tealium-ios/blob/master/Samples/iOS_WKWebView%2BTealium_Objc/iOS_WKWebView%2BTealium_Objc/TealiumHelper.m) に、この実装例が示されています。

Objective-C SDK は現在クローズドソースですが、詳細なコンテキストを示すため、Web ビューがどのように作成されるかを以下のコードスニペットに示します。

```obj-c
- (UIView *_Nullable)webViewContainer {
    if (!_webViewContainer) {
        UIWindow *window = [[UIApplication sharedApplication] keyWindow];
        UIViewController *rootViewController = window.rootViewController;
        UIViewController *topViewController;

        if ([rootViewController isKindOfClass:[UINavigationController class]]) {
            topViewController = [((UINavigationController *)rootViewController).viewControllers lastObject];
        } else if ([rootViewController isKindOfClass:[UITabBarController class]]) {
            topViewController = ((UITabBarController *)rootViewController).selectedViewController;
        } else {
            topViewController = rootViewController;
        }

        UIView *view = topViewController.viewIfLoaded;
        if (view) {
            self.webViewContainer = view;
        }
    }
    return _webViewContainer;
}
```

このビューは、`WKWebView` の初期化時に一度だけ使用されます。

## `TealiumConfig`

### `WKProcessPool`

アプリで `WKWebView` Web ビューを使用する場合は、シングルトンの `WKProcessPool` インスタンスを作成して保持し、Tealium をインスタンス化する前に構成します。これにより、アプリに Tealium タグ管理 Web ビュー以外の Web ビューが含まれている場合の Cookie 同期の問題も防止できます。

```obj-c
WKProcessPool *wkProcessPool = [[WKProcessPool alloc] init];
```

例：

```obj-c
_configuration = [TEALConfiguration configurationWithAccount:@"ACCOUNT" profile:@"PROFILE" environment:@"ENV"];
_configuration.wkProcessPool = MyApp.wkProcessPool;

self.tealium = [Tealium newInstanceForKey:@"INSTANCE_KEY" configuration:_configuration];
```

### `WKWebviewConfiguration`

Tealium タグ管理 Web ビューで使用するカスタム `WKWebviewConfiguration` オブジェクトを渡すことができます。`webviewProcessPool` オプションの代わりにこのオプションを使用する場合は、カスタマイズ可能な `WKWebviewConfiguration` の `processPool` プロパティを通じて、シングルトンの `WKProcessPool` を構成します。


<blockquote>
今後 `WKWebView` の API が変更された場合に必要になる可能性があるため、このオプションの使用を推奨します。
</blockquote>


例：

```obj-c
_configuration = [TEALConfiguration configurationWithAccount:@"ACCOUNT" profile:@"PROFILE" environment:@"ENV"];

WKWebviewConfiguration *webviewConfiguration = [[WKWebViewConfiguration alloc] init];
webviewConfiguration.processPool = MyApp.wkProcessPool;
_configuration.wkWebViewConfig = webviewConfiguration

self.tealium = [Tealium newInstanceForKey:@"INSTANCE_KEY" configuration:_configuration];
```