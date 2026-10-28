---
title: DeepLinkHandlerモジュール
description: ディープリンクを追跡し、キャンペーンまたは参照元にアトリビューションします。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/deep-link/
---
DeepLinkHandlerモジュールは、アトリビューションとトレース管理のために受信したディープリンクを追跡します。アプリがディープリンクから起動されると、モジュールはURLを取得し、そのクエリパラメータをデータレイヤーに抽出します。デフォルトでは、ディープリンクの処理は自動的に実行されます。

## 仕組み

ディープリンクによってアプリが開かれると、モジュールは完全なURLを`deep_link_url`としてデータレイヤーに追加します。各クエリパラメータは抽出され、接頭辞`deep_link_param_`を使用して個別に追加されます。たとえば、`https://example.com/?campaign_code=SUMMER`の場合、次の値が生成されます。

```
deep_link_url = "https://example.com/?campaign_code=SUMMER"
deep_link_param_campaign_code = "SUMMER"
```


<blockquote>
ディープリンクのデータレイヤー属性は、セッション中のみ保存されます。
</blockquote>


## データレイヤー

ディープリンクが処理されると、次の属性がデータレイヤーに追加されます。

| 属性 | 型 | 説明 |
| :--- | :--- | :--- |
| `deep_link_url` | `String` | クエリパラメータを含む、ディープリンクの完全なURL。 |
| `deep_link_param_X` | `String` | ディープリンクURLの各クエリパラメータ。`X`はパラメータ名です。 |
| `deep_link_referrer_url` | `String` | このディープリンクの参照元となったページまたはリソースのURL。 |
| `deep_link_referrer_app`（iOSのみ） | `String` | カスタムURLスキームを介してこのディープリンクを開いたアプリのバンドル識別子。 |

## インストール



DeepLinkHandlerモジュールは`prism-core`に含まれています。`prism-core`は、他のすべてのPrismモジュールの推移的依存関係です。


DeepLinkHandlerモジュールは`TealiumPrismCore`に含まれています。リポジトリURL `https://github.com/Tealium/tealium-prism-swift`を使用してSwift Package Managerの依存関係として追加するか、CocoaPods用のPodfileに追加します。

```ruby
pod 'tealium-prism/Core'
```

代わりにPrismライブラリ全体をインストールするには、次のようにします。

```ruby
pod 'tealium-prism'
```



## 初期化

`TealiumConfig`の`modules`リストにモジュールを追加します。



```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "ACCOUNT",
    profileName = "PROFILE",
    environment = Environment.PROD,
    modules = listOf(
        Modules.deepLink(),
        // other modules...
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
        // other modules...
    ]
)
```



## ディープリンクの手動処理

ディープリンクを手動で処理するには、`Tealium`インスタンスのディープリンクプロパティで`handle`を呼び出します。



```kotlin
tealium.deepLink.handle(uri).subscribe { result ->
    // Optionally handle result here
}

// With a referrer URL:
tealium.deepLink.handle(uri, referrerUri).subscribe { result ->
    // Optionally handle result here
}
```


```swift
tealium.deepLink.handle(link: url, referrer: .fromUrl(referrerUrl)).subscribe { result in
    // Optionally handle result here
}
```



## 構成

### ディープリンクの自動追跡を無効にする

デフォルトでは、アプリがディープリンクから起動されると、モジュールがディープリンクを自動的に処理します。

ディープリンクの自動追跡を無効にするには、次のようにします。



```kotlin
Modules.deepLink { settings ->
    settings.setAutomaticDeepLinkTrackingEnabled(false)
}
```


アプリの`Info.plist`ファイルに、値を`false`に構成したキー`TealiumAutotrackingDeepLinkEnabled`を追加します。



### ディープリンクイベントを有効にする

デフォルトでは、ディープリンクが処理されても、モジュールは個別の追跡イベントを送信しません。ディープリンクイベントを有効にすると、ディープリンクが開かれるたびに、モジュールは`deep_link`イベントも追跡します。



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



### ディープリンク経由のトレースを有効にする

デフォルトでは、Tealium QR TraceツールからQRコードをスキャンすると、トレースセッションに自動的に参加します。

ディープリンクを使用してトレースに参加する機能を無効にするには、次のようにします。



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

ローカルまたはリモートの構成JSONファイルでモジュールを構成します。

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

## Settings Builderリファレンス



詳細については、[`DeepLinkSettingsBuilder`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.settings.modules/-deep-link-settings-builder/)を参照してください。

| メソッド | 説明 |
| :--- | :--- |
| `setAutomaticDeepLinkTrackingEnabled(enabled: Boolean)` | ディープリンクの自動処理を有効または無効にします。 |
| `setDeepLinkTraceEnabled(enabled: Boolean)` | ディープリンクからのトレース機能を有効または無効にします。デフォルト：`true`。 |
| `setSendDeepLinkEventEnabled(enabled: Boolean)` | ディープリンクが開かれたときの`deep_link`イベントの送信を有効または無効にします。デフォルト：`false`。 |
| `setEnabled(enabled: Boolean)` | モジュールを永続的に有効または無効にします。 |
| `setOrder(order: Int)` | モジュールを初期化する順序を構成します。 |


詳細については、[`DeepLinkSettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/DeepLinkSettingsBuilder.html)を参照してください。

| メソッド | 説明 |
| :--- | :--- |
| `setDeepLinkTraceEnabled(_:)` | ディープリンクからのトレース機能を有効または無効にします。デフォルト：`true`。 |
| `setSendDeepLinkEvent(_:)` | ディープリンクが開かれたときの`deep_link`イベントの送信を有効または無効にします。デフォルト：`false`。 |
| `setEnabled(_:)` | モジュールを永続的に有効または無効にします。 |
| `setOrder(_:)` | モジュールを初期化する順序を構成します。 |
| `setRules(_:)` | モジュールを実行するタイミングを決定するルールを構成します。 |

