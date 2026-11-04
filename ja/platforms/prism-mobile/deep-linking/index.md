---
title: ディープリンク
description: アトリビューショントラッキングとトレース管理のために、Tealium Prism SDK でディープリンクを処理する方法について説明します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/deep-linking/
---
DeepLink モジュールは、アトリビューショントラッキングとトレース管理のために、受信したディープリンクを自動的に処理します。ディープリンク URL の取得、クエリパラメータの抽出、リファラー情報の管理を行い、デバッグ用の Trace モジュールと連携します。

iOS と Android では、明示的に無効にしない限り、モジュールがディープリンクイベントを自動的にリッスンします。このモジュールは、`modules` リストに追加するか、ローカルまたはリモート構成 JSON で構成を指定した場合にのみ実行されます。

## 収集されるデータポイント

ディープリンクが処理されると、DeepLink モジュールは次のデータを収集します。

| データポイント | キー | 説明 |
|:-----------|:----|:------------|
| ディープリンク URL | `deep_link_url` | ディープリンクの完全な URL |
| クエリパラメータ | `deep_link_param_*` | `deep_link_param_` というプレフィックスが付いた各クエリパラメータ |
| リファラー URL | `deep_link_referrer_url` | このディープリンクへの参照元となった URL |
| リファラーアプリ | `deep_link_referrer_app` | このディープリンクを開いたアプリの識別子 |

## インストール

DeepLink モジュールは、プログラムによる構成、リモート JSON、またはローカル JSON の構成を使用して構成できます。


<blockquote>
React Native では DeepLink モジュールを構成できません。ネイティブ Prism SDK が iOS と Android の両方でディープリンクを自動的に処理します。
</blockquote>




Tealium 構成に DeepLink モジュールを追加します。

```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "tealiummobile",
    profileName = "your-profile",
    environment = "dev",
    modules = listOf(Modules.deepLink())
).build()
```

強制構成を使用して構成するには、次のようにします。

```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "tealiummobile",
    profileName = "your-profile",
    environment = "dev",
    modules = listOf(Modules.deepLink {
        it.setEnabled(true)
            .setDeepLinkTraceEnabled(true)
            .setSendDeepLinkEventEnabled(false)
    })
).build()
```


Tealium 構成に DeepLink モジュールを追加します。

```swift
let config = TealiumConfig(account: "tealiummobile",
                          profile: "your-profile",
                          environment: "dev",
                          modules: [
                              Modules.deepLink(),
                              // other modules...
                          ])
```

強制構成を使用して構成するには、次のようにします。

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
                              // other modules...
                          ])
```



### JSON 構成

ローカルまたはリモートの構成 JSON ファイルで DeepLink モジュールを構成します。

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
| ディープリンクトレースの有効化 | `deep_link_trace_enabled` | ディープリンクからのトレースを有効または無効にします。有効にすると、QR Trace ツールの QR コードが自動的にトレースへ参加します。 | `true` |
| ディープリンクイベントの送信 | `send_deep_link_event` | ディープリンクイベントの送信を有効または無効にします。有効にすると、ディープリンクイベントが自動的にトラッキングされます。 | `false` |

## ディープリンクの手動処理


<blockquote>
`tealium.deepLink.handle()` は React Native では使用できません。ディープリンクはネイティブ SDK によって自動的に処理されます。
</blockquote>




```kotlin
tealium.deepLink.handle(url, referrer)
    .subscribe { result ->
        // Optionally handle result here
    }
```


```swift
tealium.deepLink.handle(link: url, referrer: .fromUrl(referrerUrl)).subscribe { result in
    // Optionally handle result here
}
```



### 自動トラッキングの無効化（iOS）

iOS では、デフォルトでディープリンクが自動的にトラッキングされます。ディープリンクの自動トラッキングを無効にするには、`Info.plist` で `TealiumAutotrackingDeepLinkEnabled` キーを `false` に構成します。

## API リファレンス

クラスとメソッドの詳細なシグネチャについては、API リファレンスドキュメントを参照してください。

* [DeepLinkHandler（Swift）](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Protocols/DeepLinkHandler.html)
* [DeepLinkSettingsBuilder（Swift）](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/DeepLinkSettingsBuilder.html)
* [DeepLink（Kotlin）](https://docs.tealium.com/tealium-prism-kotlin/)