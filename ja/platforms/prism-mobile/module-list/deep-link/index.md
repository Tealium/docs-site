---
title: DeepLinkHandlerモジュール
description: ディープリンクを追跡し、キャンペーンやリファラーに帰属します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/deep-link/
---
DeepLinkHandlerモジュールは、帰属とトレース管理のために受信ディープリンクを追跡します。アプリがディープリンクから起動されたとき、このモジュールはURLをキャプチャし、そのクエリパラメータをデータレイヤーに抽出します。ディープリンクの処理はデフォルトで自動的に実行されます。

## 動作方法

ディープリンクでアプリが開かれると、モジュールはデータレイヤーに完全なURLを `deep_link_url` として追加します。各クエリパラメータは `deep_link_param_` のプレフィックスを使用して個別に抽出され、追加されます。例えば、`https://example.com/?campaign_code=SUMMER` は以下を生成します：

```
deep_link_url = "https://example.com/?campaign_code=SUMMER"
deep_link_param_campaign_code = "SUMMER"
```


<blockquote>
ディープリンクのデータレイヤー属性はセッション中のみ保存されます。
</blockquote>


## データレイヤー

ディープリンクが処理されると、以下の属性がデータレイヤーに追加されます：

| 属性 | タイプ | 説明 |
| :--- | :--- | :--- |
| `deep_link_url` | `String` | クエリパラメータを含むディープリンクの完全なURL。 |
| `deep_link_param_X` | `String` | ディープリンクURLの各クエリパラメータで、`X`はパラメータ名です。 |
| `deep_link_referrer_url` | `String` | このディープリンクを参照したページまたはリソースのURL。 |
| `deep_link_referrer_app` (iOSのみ) | `String` | このディープリンクをカスタムURLスキームを介して開いたアプリのバンドル識別子。 |

## インストール



DeepLinkHandlerモジュールは `prism-core` に含まれており、これは他のすべてのPrismモジュールの推移的依存関係です。


DeepLinkHandlerモジュールは `TealiumPrismCore` に含まれています。リポジトリURL `https://github.com/Tealium/tealium-prism-swift` を使用してSwift Package Managerの依存関係として追加するか、CocoaPodsのためにPodfileに追加してください：

```ruby
pod 'tealium-prism/Core'
```

代わりに完全なPrismライブラリをインストールする場合：

```ruby
pod 'tealium-prism'
```



## 初期化

`TealiumConfig`の `modules` リストにモジュールを追加します。



```kotlin
val config = TealiumConfig.Builder(
    accountName = "ACCOUNT",
    profileName = "PROFILE",
    environment = Environment.PROD,
    modules = listOf(
        Modules.deepLink(),
        // 他のモジュール...
    )
).build()
```


```swift
let config = TealiumConfig(
    account: "ACCOUNT",
    profile: "PROFILE",
    environment: "prod",
    modules: [
        Modules.deepLink(),
        // 他のモジュール...
    ]
)
```



## ディープリンクを手動で処理

ディープリンクを手動で処理するには、`Tealium`インスタンスのディープリンクプロパティで `handle` を呼び出します。



```kotlin
tealium.deeplink.handle(uri).subscribe { result ->
    // ここで結果をオプションで処理します
}

// リファラーURL付き：
tealium.deeplink.handle(uri, referrerUri).subscribe { result ->
    // ここで結果をオプションで処理します
}
```


```swift
tealium.deepLink.handle(link: url, referrer: .fromUrl(referrerUrl)).subscribe { result in
    // ここで結果をオプションで処理します
}
```



## 構成

### 自動ディープリンク追跡を無効にする

デフォルトでは、モジュールはアプリがディープリンクから起動されたときに自動的にディープリンクを処理します。

自動ディープリンク追跡を無効にするには：



```kotlin
Modules.deepLink { settings ->
    settings.setAutomaticDeepLinkTrackingEnabled(false)
}
```


アプリの `Info.plist` ファイルにキー `TealiumAutotrackingDeepLinkEnabled` と値 `false` を追加します。



### ディープリンクイベントを有効にする

デフォルトでは、モジュールはディープリンクが処理されたときに別のトラッキングイベントを送信しません。ディープリンクイベントを有効にすると、モジュールはディープリンクが開かれるたびに `deep_link` イベントも追跡します。



```kotlin
Modules.deepLink { settings ->
    settings.setSendDeepLinkEventEnabled(true)
}
```


```swift
Modules.deepLink(forcingSettings: { builder in
    builder.setSendDeepLinkEvent(true)
})
```



### ディープリンクを介したトレースを有効にする

デフォルトでは、Tealium QR TraceツールからのQRコードをスキャンすると、自動的にトレースセッションに参加します。

ディープリンクを使用してトレースに参加する機能を無効にするには：



```kotlin
Modules.deepLink { settings ->
    settings.setDeepLinkTraceEnabled(false)
}
```


```swift
Modules.deepLink(forcingSettings: { builder in
    builder.setDeepLinkTraceEnabled(false)
})
```



### JSON構成

ローカルまたはリモートの構成JSONファイルでモジュールを構成します：

```json
{
    "modules": {
        "DeepLink": {
            "module_type": "DeepLink",
            "enabled": true,
            "configuration": {
                "deep_link_trace_enabled": true,
                "send_deep_link_event": false
            }
        }
    }
}
```

## 構成ビルダー参照



詳細については、[`DeepLinkSettingsBuilder`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.settings.modules/-deep-link-settings-builder/)を参照してください。

| メソッド | 説明 |
| :--- | :--- |
| `setAutomaticDeepLinkTrackingEnabled(enabled: Boolean)` | 自動ディープリンク処理を有効または無効にします。 |
| `setDeepLinkTraceEnabled(enabled: Boolean)` | ディープリンクからのトレース機能を有効または無効にします。デフォルト：`true`。 |
| `setSendDeepLinkEventEnabled(enabled: Boolean)` | ディープリンクが開かれたときに `deep_link` イベントを送信することを有効または無効にします。デフォルト：`false`。 |
| `setEnabled(enabled: Boolean)` | モジュールを永久に有効または無効にします。 |
| `setOrder(order: Int)` | モジュールが初期化される順序を構成します。 |


詳細については、[`DeepLinkSettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/DeepLinkSettingsBuilder.html)を参照してください。

| メソッド | 説明 |
| :--- | :--- |
| `setDeepLinkTraceEnabled(_:)` | ディープリンクからのトレース機能を有効または無効にします。デフォルト：`true`。 |
| `setSendDeepLinkEvent(_:)` | ディープリンクが開かれたときに `deep_link` イベントを送信することを有効または無効にします。デフォルト：`false`。 |
| `setEnabled(_:)` | モジュールを永久に有効または無効にします。 |
| `setOrder(_:)` | モジュールが初期化される順序を構成します。 |
| `setRules(_:)` | モジュールが実行されるタイミングを決定するルールを構成します。 |

