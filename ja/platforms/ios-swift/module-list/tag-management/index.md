---
title: TagManagementモジュール
description: JavaScriptを実行するために、レンダリングされないWKWebViewインスタンスを使用するUniversal Tag（utag.js）のクライアント側実装です。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/tag-management/
---
## 使用方法

TagManagementモジュールは、レンダリングされない`WKWebView`インスタンスを使用してJavaScriptを実行するUniversal Tag（`utag.js`）のクライアント側実装です。このモジュールは、Tag Managementを使用するアプリで必要です。CarthageおよびCocoaPodsのフレームワークビルドには自動的に含まれます。

## サポート対象プラットフォーム

* iOS

## 要件

* WebKit（WKWebView）

## インストール

Swift Package Manager、CocoaPods、またはCarthageを使用してTagManagementモジュールをインストールします。

### Swift Package Manager（推奨）

バージョン1.9.0以降でサポートされているSwift Package Managerは、Tealium Swiftライブラリをインストールするための推奨かつ最も簡単な方法です。

1. Xcodeプロジェクトで、**File > Add Package Dependencies**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
1. バージョンルールを構成します。通常は`"Up to next major"`を推奨します。現在のTealium Swiftライブラリのバージョンがリストに表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
1. インストールするモジュールのリストから`TagManagement`モジュールを選択し、Xcodeプロジェクトの**Frameworks and Libraries**で各アプリターゲットに追加します。

### CocoaPods

CocoaPodsでTagManagementモジュールをインストールするには、Podfileに次のPodを追加します。  
```perl
pod 'tealium-swift/TagManagement'
```

詳しくは、[iOS向けCocoaPodsのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#cocoapods)を参照してください。

### Carthage

CarthageでTagManagementモジュールをインストールするには、次の手順に従います。

1. XcodeでアプリターゲットのGeneral構成ページに移動します。

2. **Embedded Binaries**セクションに次のフレームワークを追加します。  
      ```perl
      TealiumTagManagement.framework
      ```
詳しくは、[iOS向けCarthageのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#carthage)を参照してください。

## 初期化

モジュールを初期化するには、`TealiumConfig`の[`collectors`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#collectors)プロパティに指定されていることを確認します。

`config.dispatchers = [Dispatchers.TagManagement]`

## WebView構成のカスタマイズ

### App Bound Domains

アプリが[WKAppBoundDomains](https://webkit.org/blog/10882/app-bound-domains/)機能を使用して、アプリ内のWebViewが通信できるドメインを制限している場合は、カスタム`WKWebViewConfiguration`を渡し、その`limitsNavigationsToAppBoundDomains`プロパティを`true`に構成する必要があります。これを行わない場合、すべてのトラッキング呼び出しがオペレーティングシステムによって破棄されます。また、`Info.plist`の`WKAppBoundDomains`リストに「tags.tiqcdn.com」を含めるとともに、Tag Managementで構成したすべてのタグのドメイン（例：「google-analytics.com」）も含める必要があります。アプリ全体で構成できるドメインは最大10個であるため、複数のクライアント側タグを使用すると、この上限を簡単に超える可能性があることに注意してください。

```
 let config = TealiumConfig(account: "ACCOUNT",
                               profile: "PROFILE",
                               environment: "ENVIRONMENT",
                               datasource: "DATASOURCE")
 config.dispatchers = [Dispatchers.TagManagement]
 let wkWebViewConfiguration = WKWebViewConfiguration()
 wkWebViewConfiguration.limitsNavigationsToAppBoundDomains = true
 config.webviewConfig = wkWebViewConfiguration
 tealium = Tealium(config: config)
        
```

### プロセスプール

アプリで独自の`WKWebView`を使用している場合は、Cookieの同期に関する問題を回避するため、Tealium WebViewで使用するシングルトンの`WKProcessPool`インスタンス、またはアプリ内の他のWebViewと共有されるカスタム`WkWebViewConfiguration`を渡します。

[webviewProcessPool](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#webviewprocesspool)および[webViewConfig](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#webviewconfig)についてご確認ください。

## データレイヤー

各トラッキング呼び出しでは、次の変数が送信されます。

| 変数 | 型 | 説明 | 例 |
|------------------|-------| -------------------------------------------------------------|---------------|
| `dispatch_service` | `String` | トラッキング呼び出しの送信元モジュールを示す固定文字列 | `"tagmanagement"` |

## WKWebViewについて

バージョン1.7.0より前では、このモジュールは`UIWebView`を使用していましたが、現在は`WKWebView`が推奨され、`UIWebView`は非推奨になっています。OSでは、レンダリングされない場合でも、`WKWebView`を常に`UIView`にアタッチする必要があります。UIViewにアタッチされていない場合、OSによってパフォーマンスが大幅に抑制され、JavaScriptの実行が最適化されません。**これに対応するため、Tag Managementモジュールは、レンダリングされないWKWebViewをアプリのルートUIViewにアタッチしようとします。**

アプリのビュー階層が複雑で、モジュールが`rootViewController`を検出できない場合は、`viewDidLoad`、`viewWillAppear:`、または`viewDidAppear:`で、アタッチ先のビューを指定して[TealiumConfig](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/)を初期化します。


<blockquote>
リリース1.7.1ではビューの自動検出が大幅に改善され、ほとんどのシナリオでビューを指定する必要がなくなりました。ただし、トラッキング呼び出しが正しく送信されることをアプリでテストして確認する必要があります。詳細については、[リリースノート](https://docs.tealium.com/ja/platforms/ios-swift/release-notes)を参照してください。
</blockquote>


プッシュ通知の受信時にアプリが`UIViewController`へ遷移し、Tealiumの初期化時とは異なるビュー階層になる場合は、次のAPIメソッドを使用して現在の`UIView`を更新する必要があります。

```swift
override func viewDidLoad() {
    super.viewDidLoad()
    // this view does not have a navigation controller
    if self.navigationController == nil {
          // update the current root UIView on the Tealium instance
        tealium?.updateRootView(self.view)
    }
    // Do any additional setup after loading the view.
}
```

完全な例については、サンプルアプリ[Swift-WKWebView](https://github.com/Tealium/tealium-swift/tree/master/samples/Swift-WKWebView)を参照してください。


<blockquote>
[`shouldAddCookieObserver`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#shouldaddcookieobserver)メソッドを使用すると、Cookieの同期中に独自のCookieオブザーバーを使用できます。この同期では、Cookieを構成した後にメインスレッドでCookieを取得するためのCookieオブザーバーが必要です。この問題は`WKWebView`のバグが原因であり、このバグによって独自のオブザーバーが呼び出されなくなります。
</blockquote>
