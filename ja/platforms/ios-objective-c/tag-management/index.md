---
title: タグ管理
description: Universal Tag (utag.js) JavaScriptクライアントサイドを実行するための非レンダリングWKWebViewインスタンスとしてのタグ管理の実装方法を学びます。
url: https://docs.tealium.com/ja/platforms/ios-objective-c/tag-management/
---
このタグ管理機能により、JavaScriptベースのベンダータグをアプリに統合し、Tealium iQを使用してリモートで管理することができます。これはウェブサイトと同様の方法です。

## 仕組み

タグ管理が有効になっているTealium iQで[モバイルプロファイルを作成]()した後、アプリでTealiumインスタンスを初期化すると、非レンダリングのウェブビューが作成され、TealiumからシンプルなHTMLファイルをロードし、その中でUniversal Tag `utag.js`をロードします。このウェブビューはユーザーには表示されません。

* バージョン5.5.0以降、およびiOS 11.0以降を実行している場合は、[WKWebView](https://developer.apple.com/documentation/webkit/wkwebview?language=objc)を使用します。
* バージョン5.4.x以前、またはiOS 10.0以前を実行している場合は、[UIWebView](https://developer.apple.com/documentation/uikit/uiwebview)を使用します。

iOS 11.0より低いバージョンをサポートしていてもWKWebViewを使用したい場合は、バージョン5.5.0以降にアップグレードしてください。ただし、visitor_idやその他のクッキーがリセットされるというデメリットがあります。これは、[WKHTTPCookieStore](https://developer.apple.com/documentation/webkit/wkhttpcookiestore)がiOS 11.0でのみサポートされているためです。

### サンプル

Tealiumの`WKWebView`についてより詳しく知るために、[WKWebViewサンプル](https://github.com/Tealium/tealium-ios/tree/master/Samples/iOS_WKWebView%2BTealium_Objc)を探索してみてください。

### 使用法

`WKWebView`は、レンダリングされない場合でも`UIView`にアタッチする必要があります。これを実現するために、Tealium SDKは非レンダリングの`WKWebView`を`rootViewController.view`にアタッチしようとします。これは、ウィンドウの`rootViewController`が`UIViewController`のサブクラスまたはAppleのコンテナビューコントローラ(`UINavigationController`または`UITabBarController`)の一つである場合の最も一般的なシナリオです。

アプリが複雑なビュー階層を持っている場合は、`viewDidLoad`、`viewWillAppear:`、または`viewDidAppear:`で`TEALConfiguration`インスタンスにアタッチするビューを構成します。

```obj-c
TEALConfiguration *tealConfig = [TEALConfiguration configurationWithAccount:@&#34;ACCOUNT&#34;
                                              profile:@&#34;PROFILE&#34;
                                              environment:@&#34;ENVIRONMENT&#34;
                                              datasource:@&#34;DATASOURCE&#34;];
tealConfig.view = &lt;UIVIEW&gt;; // 例えば、UIViewControllerのサブクラスのself.view
// このインスタンスの一意のキーで初期化
Tealium *tealium = [Tealium newInstanceForKey:@&#34;INSTANCE&#34; configuration:tealConfig]; 
```

| パラメータ    | タイプ     | 説明                                        | 例        |
|:--------------|:---------|:---------------------------------------------------|:---------------|
| `account`     | `String` | Tealiumのアカウント名                               | `&#34;companyXYZ&#34;` |
| `profile`     | `String` | Tealiumのプロファイル名                               | `&#34;main&#34; `      |
| `environment` | `String` | Tealiumの環境名                           | `&#34;prod&#34;`       |
| `datasource`  | `String` | (オプション) データソースキー (ない場合は`null`に構成) | `&#34;abc123&#34;`     |


プッシュ通知を受け取った後、アプリが`UIViewController`にジャンプし、Tealiumが初期化されたときとビュー階層が異なる場合は、古いTealiumのインスタンスを削除し、アタッチするビューで新しいインスタンスを作成する必要があります。この例は、サンプルアプリの[`GreenViewController.m`](https://github.com/Tealium/tealium-ios/blob/master/Samples/iOS_WKWebView%2BTealium_Objc/iOS_WKWebView%2BTealium_Objc/GreenViewController.m)と[TealiumHelper.m](https://github.com/Tealium/tealium-ios/blob/master/Samples/iOS_WKWebView%2BTealium_Objc/iOS_WKWebView%2BTealium_Objc/TealiumHelper.m)で示されています。

Objective-C SDKは現在クローズドソースですが、より多くのコンテキストを提供するために、以下のコードスニペットはウェブビューがどのように作成されるかを示しています。

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

ビューは`WKWebView`を初期化するために一度だけ使用されます。

## `TealiumConfig`

### `WKProcessPool`

アプリで`WKWebView`ウェブビューを使用する場合は、シングルトンの`WKProcessPool`インスタンスを作成し、Tealiumをインスタンス化する前に構成します。これにより、アプリがTealium Tag Managementウェブビュー以外のウェブビューを含む場合のクッキー同期問題も防ぎます。

```obj-c
WKProcessPool *wkProcessPool = [[WKProcessPool alloc] init];
```

例:   

```obj-c
_configuration = [TEALConfiguration configurationWithAccount:@&#34;ACCOUNT&#34; profile:@&#34;PROFILE&#34; environment:@&#34;ENV&#34;];
_configuration.wkProcessPool = MyApp.wkProcessPool;

self.tealium = [Tealium newInstanceForKey:@&#34;INSTANCE_KEY&#34; configuration:_configuration];
```

### `WKWebviewConfiguration`

カスタムの`WKWebviewConfiguration`オブジェクトを渡すことを許可し、これはTealium Tag Managementウェブビューによって使用されます。`webviewProcessPool`オプションの代わりにこのオプションを使用する場合は、カスタマイズ可能な`WKWebviewConfiguration`の`processPool`プロパティを通じてシングルトンの`WKProcessPool`を構成します。

`WKWebView`に対する将来のAPI変更が必要になる場合、このオプションを使用することを推奨します。

例:   

```obj-c
_configuration = [TEALConfiguration configurationWithAccount:@&#34;ACCOUNT&#34; profile:@&#34;PROFILE&#34; environment:@&#34;ENV&#34;];

WKWebviewConfiguration *webviewConfiguration = [[WKWebViewConfiguration alloc] init];
webviewConfiguration.processPool = MyApp.wkProcessPool;
_configuration.wkWebViewConfig = webviewConfiguration

self.tealium = [Tealium newInstanceForKey:@&#34;INSTANCE_KEY&#34; configuration:_configuration];
```


