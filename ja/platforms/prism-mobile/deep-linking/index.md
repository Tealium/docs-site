---
title: ディープリンキング
description: Tealium Prism SDKを使用してアトリビューション追跡とトレース管理のためのディープリンクを処理する方法を学びます。
url: https://docs.tealium.com/ja/platforms/prism-mobile/deep-linking/
---
DeepLinkモジュールは、アトリビューション追跡とトレース管理のために受信するディープリンクを自動的に処理します。ディープリンクURLをキャプチャし、クエリパラメータを抽出し、リファラー情報を管理し、デバッグのためにTraceモジュールと統合します。

iOSでは、明示的に無効にされない限り、モジュールは自動的にディープリンクイベントをリッスンします。

## 収集されるデータポイント

ディープリンクが処理されると、DeepLinkモジュールは以下のデータを収集します：

| データポイント | キー | 説明 |
|:-----------|:----|:------------|
| ディープリンクURL | `deep_link_url` | ディープリンクの完全なURL |
| クエリパラメータ | `deep_link_param_*` | `deep_link_param_`で始まる各クエリパラメータ |
| リファラーURL | `deep_link_referrer_url` | このディープリンクを参照したURL |
| リファラーアプリ | `deep_link_referrer_app` | このディープリンクを開いたアプリの識別子 |

## インストール

DeepLinkモジュールは、プログラム、リモートJSON、またはローカルJSON構成を使用して構成できます。


<blockquote>
DeepLinkモジュールはReact Nativeでは構成できません。ネイティブのPrism SDKがiOSとAndroidの両方でディープリンクを自動的に処理します。
</blockquote>




Tealium構成にDeepLinkモジュールを追加します：

```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "tealiummobile",
    profileName = "your-profile",
    environment = "dev"
)
.addModule(Modules.deepLink())
.build()
```

強制構成で構成する場合：

```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "tealiummobile",
    profileName = "your-profile",
    environment = "dev"
)
.addModule(Modules.deepLink {
    setEnabled(true)
    setDeepLinkTraceEnabled(true)
    setSendDeepLinkEvent(false)
})
.build()
```


Tealium構成にDeepLinkモジュールを追加します：

```swift
let config = TealiumConfig(account: "tealiummobile",
                          profile: "your-profile",
                          environment: "dev",
                          modules: [
                              Modules.deepLink(),
                              // 他のモジュール...
                          ])
```

強制構成で構成する場合：

```swift
let config = TealiumConfig(account: "tealiummobile",
                          profile: "your-profile",
                          environment: "dev",
                          modules: [
                              Modules.deepLink(forcingSettings: { builder in
                                  builder.setEnabled(true)
                                         .setDeepLinkTraceEnabled(true)
                                         .setSendDeepLinkEvent(false)
                              }),
                              // 他のモジュール...
                          ])
```



### JSON構成

ローカルまたはリモートの構成JSONファイルでDeepLinkモジュールを構成します：

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

## 構成オプション

| 構成 | キー | 説明 | デフォルト |
|:--------|:----|:------------|:--------|
| ディープリンクトレース有効 | `deep_link_trace_enabled` | ディープリンクからのトレースを有効または無効にします。有効にすると、QR TraceツールのQRコードが自動的にトレースに参加します。 | `true` |
| ディープリンクイベントの送信 | `send_deep_link_event` | ディープリンクイベントの送信を有効または無効にします。有効にすると、ディープリンクイベントが自動的に追跡されます。 | `false` |

## ディープリンクを手動で処理


<blockquote>
`tealium.deepLink.handle()`はReact Nativeでは使用できません。ディープリンクはネイティブSDKによって自動的に処理されます。
</blockquote>




```kotlin
tealium.deepLink.handle(url, referrer)
    .subscribe { result ->
        // 必要に応じてここで結果を処理します
    }
```


```swift
tealium.deepLink.handle(link: url, referrer: .fromUrl(referrerUrl)).subscribe { result in
    // 必要に応じてここで結果を処理します
}
```



### 自動追跡の無効化（iOS）

iOSでは、ディープリンクはデフォルトで自動的に追跡されます。自動ディープリンク追跡を無効にするには、`Info.plist`で`TealiumAutotrackingDeepLinkEnabled`キーを`false`に構成します。

## APIリファレンス

詳細なクラスとメソッドの署名については、APIリファレンスドキュメントを参照してください：

* [DeepLinkHandler (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DeepLinkHandler.html)
* [DeepLinkSettingsBuilder (Swift)](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/DeepLinkSettingsBuilder.html)
* [DeepLink (Kotlin)](https://docs.tealium.com/tealium-prism-kotlin/)