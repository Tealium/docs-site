---
title: TagManagementモジュール
description: JavaScriptを実行するために、レンダリングされないWKWebViewインスタンスを使用するUniversal Tag（utag.js）のクライアント側実装です。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/tag-management/
---
## 使用方法

TagManagementモジュールは、JavaScriptを実行するために、レンダリングされない`WKWebView`インスタンスを使用するUniversal Tag（`utag.js`）のクライアント側実装です。このモジュールは、タグマネジメントを使用するアプリで必要です。CarthageおよびCocoaPodsのフレームワークビルドには自動的に含まれます。

## サポート対象プラットフォーム

* iOS

## 要件

* WebKit（WKWebView）

## インストール

CocoaPodsまたはCarthageを使用してTagManagementモジュールをインストールします。

### CocoaPods

CocoaPodsでTagManagementモジュールをインストールするには、Podfileに次のPodを追加します。  
```ruby
pod 'tealium-swift/TealiumTagManagement'
```

フレームワークは自動的にインスタンス化されます。このフレームワークは`TealiumCore` Podに依存します。iOS向けのCocoaPodsによるインストールについては、[詳細をご覧ください](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)。

### Carthage

CarthageでTagManagementモジュールをインストールするには、次の手順に従います。

1. Xcodeでアプリターゲットの「General」構成ページに移動します。

2. **Embedded Binaries**セクションに次のフレームワークを追加します。  
      ```ruby
      TealiumTagManagement.framework
      ```

フレームワークは自動的にインスタンス化されます。このフレームワークは`TealiumCore`に依存します。追加のimport文は必要ありません。iOS向けのCarthageによるインストールについては、[詳細をご覧ください](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)。

## データレイヤー

トラッキング呼び出しのたびに、次の変数が送信されます。

| 変数 | 型 | 説明 | 例 |
|------------------|-------| -------------------------------------------------------------|---------------|
| `dispatch_service` | `String` | トラッキング呼び出しの送信元モジュールを示す静的文字列 | `"tagmanagement"` |

## パブリックAPI

`WKWebView`デリゲートに準拠する別のオブジェクトをモジュールのマルチキャストデリゲートに追加することで、WKWebViewプロトコルにアクセスできます。

```swift
tealium.tagManagement()?.delegates.add(MY_OBJECT)
```

## WKWebViewについて

バージョン1.7.0より前では、このモジュールは`UIWebView`を使用していましたが、現在は非推奨となり、`WKWebView`に置き換えられています。OSでは、`WKWebView`がレンダリングされない場合でも、常に`UIView`にアタッチされている必要があります。UIViewにアタッチされていない場合、OSによってパフォーマンスが大幅に制限され、JavaScriptが最適に実行されません。**これに対応するため、Tag Managementモジュールは、レンダリングされないWKWebViewをアプリのルートUIViewにアタッチしようとします。**

アプリのビュー階層が複雑で、モジュールが`rootViewController`を検出できない場合は、`viewDidLoad`、`viewWillAppear:`、または`viewDidAppear:`で、アタッチ先となるビューを指定して[TealiumConfig](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/)を初期化してください。


<blockquote>
リリース1.7.1ではビューの自動検出機能が大幅に改善され、ほとんどの場合、ビューを指定する必要がなくなりました。ただし、トラッキング呼び出しが正しく送信されることを確認するため、アプリでテストする必要があります。詳細については、[リリースノート](https://docs.tealium.com/ja/platforms/ios-swift-v1/release-notes/)を参照してください。
</blockquote>


プッシュ通知の受信時にアプリが`UIViewController`へ遷移し、そのビュー階層がTealiumの初期化時とは異なる場合は、次のAPIメソッドを使用して現在の`UIView`を更新する必要があります。

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

完全な例については、サンプルアプリの[Swift-WKWebView](https://github.com/Tealium/tealium-swift/tree/master/samples/Swift-WKWebView)を参照してください。

`WKWebView`と`UIWebView`ではCookieを保存する方法が異なるため（それぞれ`WKHTTPCookieStore`と`HTTPCookieStorage`）、モジュールはWKWebViewの初回起動時にCookieを自動的に同期します。`HTTPCookieStorage`内のCookieは削除されませんが、最終的には自然に期限切れになります。


<blockquote>
[`shouldAddCookieObserver`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#shouldaddcookieobserver)メソッドを使用すると、Cookieの同期中に独自のCookieオブザーバーを使用できます。この同期では、Cookieの構成後にメインスレッドでCookieを取得するためのCookieオブザーバーが必要です。この問題は`WKWebView`のバグによって発生し、独自のオブザーバーが呼び出されなくなります。
</blockquote>
