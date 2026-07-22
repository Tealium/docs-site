---
title: TagManagement モジュール
description: JavaScriptを実行するためにレンダリングされていないWKWebViewインスタンスを使用するUniversal Tag（utag.js）のクライアントサイド実装。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/tag-management/
---
## 使用法

TagManagementモジュールは、レンダリングされていない`WKWebView`インスタンスを使用してJavaScriptを実行するUniversal Tag（`utag.js`）のクライアントサイド実装です。このモジュールは、Tealium iQタグ管理を使用するアプリで必要です。CarthageおよびCocoaPodsフレームワークビルドに自動的に含まれます。

## サポートされているプラットフォーム

* iOS


## 必要条件

* WebKit（WKWebView）

## インストール

CocoaPodsまたはCarthageでTagManagementモジュールをインストールします。

### CocoaPods

CocoaPodsでTagManagementモジュールをインストールするには、次のpodをPodfileに追加します：  
```ruby
pod 'tealium-swift/TealiumTagManagement'
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` podに依存性があります。iOSのCocoaPodsインストールについては[こちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)をご覧ください。

### Carthage

CarthageでTagManagementモジュールをインストールするには、次の手順に従います：

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 次のフレームワークを**Embedded Binaries**セクションに追加します：  
      ```ruby
      TealiumTagManagement.framework
      ```

フレームワークは自動的にインスタンス化されます。`TealiumCore`に依存性があります。追加のインポートステートメントは必要ありません。iOSのCarthageインストールについては[こちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)をご覧ください。

## データレイヤー
次の変数は、各トラッキング呼び出しで送信されます：

| 変数         | タイプ | 説明                                                        | 例  |
|------------------|-------| -------------------------------------------------------------|---------------|
| `dispatch_service` | `String` | トラッキング呼び出しがどのモジュールから来たかを示す静的な文字列 | `"tagmanagement"` |

## Public API
WKWebViewプロトコルは、モジュールのマルチキャストデリゲートに`WKWebView`デリゲートを準拠する別のオブジェクトを追加することでアクセス可能です：

```swift
tealium.tagManagement()?.delegates.add(MY_OBJECT)
```

## WKWebViewについて

バージョン1.7.0以前、このモジュールは現在`WKWebView`に置き換えられて非推奨となっている`UIWebView`を使用していました。OSは`WKWebView`が常に`UIView`に接続されていることを要求します。これが`UIView`に接続されていない場合、OSはパフォーマンスを大幅に制限し、JavaScriptが最適に実行されません。**これに対応するため、Tag ManagementモジュールはレンダリングされていないWKWebViewをアプリのルートUIViewに接続しようとします。**

アプリが複雑なビュー階層を持っていて、モジュールが`rootViewController`を検出できない場合は、`viewDidLoad`、`viewWillAppear:`、または`viewDidAppear:`でビューを接続するための[TealiumConfig](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/)を初期化します。


<blockquote>
リリース1.7.1はビューの自動検出を大幅に改善し、ほとんどのシナリオでビューを指定する必要をなくします。ただし、トラッキング呼び出しが正しく送信されていることを確認するために、アプリでこれをテストする必要があります。詳細は[リリースノート](https://docs.tealium.com/ja/platforms/ios-swift-v1/release-notes/)をご覧ください。
</blockquote>


アプリがプッシュ通知を受け取ったときに`UIViewController`にジャンプし、Tealiumが初期化されたときとは異なるビュー階層を持っている場合は、次のAPIメソッドを使用して現在の`UIView`を更新する必要があります。

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

`WKWebView`と`UIWebView`は、クッキーを保存するために異なる方法（`WKHTTPCookieStore`と`HTTPCookieStorage`）を使用するため、モジュールはWKWebViewが初めて起動されたときにクッキーを自動的に同期します。`HTTPCookieStorage`のクッキーは削除されませんが、最終的に自己満了します。


<blockquote>
[`shouldAddCookieObserver`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#shouldaddcookieobserver)メソッドを使用すると、クッキーの同期中に自分のクッキーオブザーバーを使用できます。これには、クッキーを構成した後にメインスレッドでクッキーを取得するためのクッキーオブザーバーが必要です。この問題は`WKWebView`のバグによって引き起こされ、自分のオブザーバーが呼び出されるのを防ぎます。
</blockquote>
  

