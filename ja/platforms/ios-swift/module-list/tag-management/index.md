---
title: TagManagement モジュール
description: JavaScriptを実行するために非表示のWKWebViewインスタンスを使用するUniversal Tag（utag.js）のクライアントサイド実装。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/tag-management/
---
## 使用法

TagManagementモジュールは、JavaScriptを実行するために非表示の`WKWebView`インスタンスを使用するUniversal Tag（`utag.js`）のクライアントサイド実装です。このモジュールは、Tealium iQタグ管理を使用するアプリで必要とされます。CarthageとCocoaPodsフレームワークビルドに自動的に含まれています。

## サポートされているプラットフォーム

* iOS

## 必要条件

* WebKit（WKWebView）

## インストール

Swift Package Manager、CocoaPods、またはCarthageを使用してTagManagementモジュールをインストールします。

### Swift Package Manager（推奨）

バージョン1.9.0以降でサポートされているSwift Package Managerは、Tealium Swiftライブラリをインストールする最も簡単で推奨される方法です：

1. Xcodeプロジェクトで、**ファイル &gt; パッケージ依存関係を追加**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
1. バージョンルールを構成します。通常、`&#34;次のメジャーまで&#34;`が推奨されます。現在のTealium Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットします。
1. インストールするモジュールのリストから`TagManagement`モジュールを選択し、Xcodeプロジェクトの各アプリターゲットに追加します。**フレームワークとライブラリ**の下にあります。

### CocoaPods

CocoaPodsでTagManagementモジュールをインストールするには、以下のpodをPodfileに追加します：  
```perl
pod &#39;tealium-swift/TagManagement&#39;
```

[iOS向けのCocoaPodsインストール](/ja/platforms/ios-swift/install/#cocoapods)について詳しく学びましょう。

### Carthage

CarthageでTagManagementモジュールをインストールするには、以下の手順を実行します：

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 次のフレームワークを**組み込みバイナリ**セクションに追加します：  
      ```perl
      TealiumTagManagement.framework
      ```
[iOS向けのCarthageインストール](/ja/platforms/ios-swift/install/#carthage)について詳しく学びましょう。

## 初期化

モジュールを初期化するには、`TealiumConfig`の[`collectors`](/ja/platforms/ios-swift/api/tealium-config/#collectors)プロパティで指定されていることを確認します。

`config.dispatchers = [Dispatchers.TagManagement]`

## WebView構成のカスタマイズ

### アプリバウンドドメイン

アプリが[WKAppBoundDomains](https://webkit.org/blog/10882/app-bound-domains/)機能を使用して、アプリ内のwebviewsが通信できるドメインを制限している場合、カスタム`WKWebViewConfiguration`を渡し、その`limitsNavigationsToAppBoundDomains`プロパティを`true`に構成する必要があります。これを行わないと、すべてのトラッキング呼び出しがオペレーティングシステムによってドロップされます。また、`Info.plist`の`WKAppBoundDomains`リストに&#34;tags.tiqcdn.com&#34;を含め、Tealium iQで構成したタグのドメイン（例：&#34;google-analytics.com&#34;）も含める必要があります。複数のクライアントサイドタグを使用している場合、アプリ全体で構成できるドメインは最大10個までなので、この数を超える可能性があります。

```
 let config = TealiumConfig(account: &#34;ACCOUNT&#34;,
                               profile: &#34;PROFILE&#34;,
                               environment: &#34;ENVIRONMENT&#34;,
                               datasource: &#34;DATASOURCE&#34;)
 config.dispatchers = [Dispatchers.TagManagement]
 let wkWebViewConfiguration = WKWebViewConfiguration()
 wkWebViewConfiguration.limitsNavigationsToAppBoundDomains = true
 config.webviewConfig = wkWebViewConfiguration
 tealium = Tealium(config: config)
        
```

### プロセスプール

アプリが独自の`WKWebView`を使用している場合、クッキー同期の問題を避けるために、Tealiumのwebviewが使用するシングルトン`WKProcessPool`インスタンスを渡すか、アプリ内の他のwebviewsと共有するカスタム`WkWebViewConfiguration`を渡します。

[webviewProcessPool](/ja/platforms/ios-swift/api/tealium-config/#webviewprocesspool)と[webViewConfig](/ja/platforms/ios-swift/api/tealium-config/#webviewconfig)について学びましょう。

## データレイヤー
以下の変数は、各トラッキング呼び出しで送信されます：

| 変数         | タイプ | 説明                                                        | 例  |
|------------------|-------| -------------------------------------------------------------|---------------|
| `dispatch_service` | `String` | トラッキング呼び出しがどのモジュールから来たかを示す静的な文字列 | `&#34;tagmanagement&#34;` |


## WKWebViewについて

バージョン1.7.0以前、このモジュールは`UIWebView`を使用していましたが、現在は`WKWebView`に置き換えられています。OSは`WKWebView`が常に`UIView`に接続されていることを要求します。これが接続されていない場合、OSはパフォーマンスを大幅に制限し、JavaScriptが最適に実行されません。**これに対応するため、Tag Managementモジュールは非表示のWKWebViewをアプリのルートUIViewに接続しようとします。**

アプリが複雑なビュー階層を持っていて、モジュールが`rootViewController`を検出していない場合は、`viewDidLoad`、`viewWillAppear:`、または`viewDidAppear:`でビューを接続するために[TealiumConfig](/ja/platforms/ios-swift/api/tealium-config/)を初期化します。

リリース1.7.1では、ビューの自動検出が大幅に改善され、ほとんどのシナリオでビューを指定する必要がなくなりました。ただし、トラッキング呼び出しが正しく送信されていることを確認するために、アプリでこれをテストする必要があります。詳細は[リリースノート](/ja/platforms/ios-swift/release-notes)をご覧ください。

アプリがプッシュ通知を受け取った際に`UIViewController`にジャンプし、Tealiumが初期化されたときとは異なるビュー階層を持っている場合、以下のAPIメソッドを使用して現在の`UIView`を更新する必要があります。

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

完全な例については、サンプルアプリ[Swift-WKWebView](https://github.com/Tealium/tealium-swift/tree/master/samples/Swift-WKWebView)をご覧ください。

[`shouldAddCookieObserver`](/ja/platforms/ios-swift/api/tealium-config/#shouldaddcookieobserver)メソッドを使用すると、クッキー同期に必要なクッキーオブザーバーを使用して、構成後にメインスレッドでクッキーを取得できます。この問題は`WKWebView`のバグによるもので、自分のオブザーバーが呼び出されないように防ぎます。  
