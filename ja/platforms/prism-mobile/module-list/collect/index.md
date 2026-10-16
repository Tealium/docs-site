---
title: コレクトモジュール
description: Tealium Collectサービスへのトラッキングコールをディスパッチします。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/collect/
---
## 動作原理

Collectモジュールは、トラッキングイベントをTealium Collectサービスに送信するディスパッチャーです。単一イベントのディスパッチとバッチイベント処理の両方を処理し、イベント数と訪問IDに基づいて配信を自動的に最適化します。カスタマイズ可能なエンドポイント、プロファイルのオーバーライド、ドメイン構成をサポートしています。

## 構成

Collectモジュールは以下の構成オプションを提供します：

| 構成                | JSONキー             | 説明                                                                         | デフォルト値                                  |
|--------------------|----------------------|------------------------------------------------------------------------------|----------------------------------------------|
| URL                | `url`                | 単一イベントを送信するためのURL。                                             | `https://collect.tealiumiq.com/event`        |
| バッチURL          | `batch_url`          | イベントのバッチを送信するためのURL。                                         | `https://collect.tealiumiq.com/bulk-event`   |
| プロファイルの上書き | `override_profile`   | イベントデータの`TealiumConfig.profile`を上書きするプロファイル。              | なし                                         |
| ドメインの上書き    | `override_domain`    | デフォルトURLドメインを置き換える（明示的なURLは上書きしない）。                | なし                                         |

モジュールはJSON構成ファイル、プログラムによる構成、またはその両方を使用して構成します。

### JSONファイル構成

ローカル構成ファイルを使用する場合は、`settingsFile`にファイル名を`TealiumConfig`に渡します。リモート構成を使用する場合は、URLを`settingsUrl`に渡します。両方を同時に使用することもできます。

以下の例はサポートされているJSON構造を示しています。

**デフォルト構成：**
```json
{
    "modules": {
        "Collect": {
            "module_type": "Collect"
        }
    }
}
```

**カスタム構成：**
```json
{
    "modules": {
        "Collect": {
            "module_type": "Collect",
            "enabled": true,
            "order": 1,
            "configuration": {
                "url": "https://custom.collect.example.com/event",
                "batch_url": "https://custom.collect.example.com/bulk-event",
                "override_profile": "custom-profile",
                "override_domain": "custom-domain.example.com"
            }
        }
    }
}
```

### プログラムによる構成

`TealiumConfig`のモジュールに追加することでプログラムによりモジュールを構成します。


<blockquote>
プログラムによる構成は常にローカルおよびリモート構成より優先されます。
</blockquote>




```kotlin
val config = TealiumConfig.Builder(
    application,
    "ACCOUNT",
    "PROFILE",
    Environment.DEV,
    listOf(Modules.collect { builder ->
        builder.setUrl("https://custom.collect.example.com/event")
              .setBatchUrl("https://custom.collect.example.com/bulk-event")
              .setProfile("custom-profile")
              .setDomain("custom-domain.example.com")
              .setEnabled(true)
              .setOrder(1)
    })
).build()
```


```swift
let config = TealiumConfig(account: "ACCOUNT",
                          profile: "PROFILE",
                          environment: "dev",
                          modules: [
                              Modules.collect(forcingSettings: { builder in
                                  builder.setUrl("https://custom.collect.example.com/event")
                                         .setBatchUrl("https://custom.collect.example.com/bulk-event")
                                         .setOverrideProfile("custom-profile")
                                         .setOverrideDomain("custom-domain.example.com")
                                         .setEnabled(true)
                                         .setOrder(1)
                              }),
                              // other modules...
                          ])
```



### 複数のインスタンス

異なるエンドポイントに異なる構成でイベントを送信する必要がある場合は、複数のCollectインスタンスを使用します。たとえば、すべてのイベントをプライマリエンドポイントに送信し、ルールによってフィルタリングされたイベントのサブセットをセカンダリエンドポイントにルーティングします。

各インスタンスには一意の`moduleId`が必要です。ルールを使用して、各インスタンスが処理するイベントを制御します。



```kotlin
val config = TealiumConfig.Builder(
    application,
    "ACCOUNT",
    "PROFILE",
    Environment.DEV
).addModule(Modules.collect(
    { builder ->
        builder.setModuleId("PrimaryCollect")
              .setUrl("https://primary.collect.example.com/event")
    },
    { builder ->
        builder.setModuleId("SecondaryCollect")
              .setUrl("https://secondary.collect.example.com/event")
              .setRules(Rule.just("purchase_rule_id"))
    }
)).build()
```


```swift
let config = TealiumConfig(account: "ACCOUNT",
                          profile: "PROFILE",
                          environment: "dev",
                          modules: [
                              Modules.collect(
                                  forcingSettings: { builder in
                                      builder.setModuleId("PrimaryCollect")
                                             .setUrl("https://primary.collect.example.com/event")
                                  },
                                  { builder in
                                      builder.setModuleId("SecondaryCollect")
                                             .setUrl("https://secondary.collect.example.com/event")
                                             .setRules(.just(["purchase_rule_id"]))
                                  }
                              ),
                              // other modules...
                          ])
```



JSON形式での同等の構成：

```json
{
    "modules": {
        "PrimaryCollect": {
            "module_type": "Collect",
            "module_id": "PrimaryCollect",
            "configuration": {
                "url": "https://primary.collect.example.com/event"
            }
        },
        "SecondaryCollect": {
            "module_type": "Collect",
            "module_id": "SecondaryCollect",
            "configuration": {
                "url": "https://secondary.collect.example.com/event"
            },
            "rules": {
                "operator": "just",
                "children": [
                    "purchase_rule_id"
                ]
            }
        }
    }
}
```
## 構成ビルダーのリファレンス

Collectモジュールは、構成のために`CollectSettingsBuilder`を使用します。以下のメソッドが利用可能です：



詳細については、[`CollectSettingsBuilder`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.settings.modules/-collect-settings-builder/)を参照してください。


| メソッド | 説明 |
|---|---|
| `setUrl(url: String)` | 個々のイベントを送信するためのURLを構成します。 |
| `setBatchUrl(url: String)` | イベントのバッチを送信するためのURLを構成します。 |
| `setProfile(profile: String)` | イベント送信時に使用するTealiumプロファイルを構成します。 |
| `setDomain(domain: String)` | デフォルトの単一およびバッチURLの代わりに使用するドメインを構成します。 |
| `setModuleId(moduleId: String)` | このモジュールインスタンスのユニークな識別子を構成します。 |
| `setEnabled(enabled: Boolean)` | モジュールを永久に有効または無効にします。 |
| `setOrder(order: Int)` | モジュールが初期化される順序を構成します。 |
| `setRules(rules: Rule<String>)` | このモジュールがイベントを処理するために一致する必要があるルールを構成します。 |
| `setMappings(mappings: ...)` | このモジュールのマッピングを構成します。 |


詳細については、[`CollectSettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/CollectSettingsBuilder.html)を参照してください。

| メソッド | 説明 |
|---|---|
| `setUrl(_:)` | 個々のイベントを送信するためのURLを構成します。 |
| `setBatchUrl(_:)` | イベントのバッチを送信するためのURLを構成します。 |
| `setOverrideProfile(_:)` | イベントデータの`TealiumConfig.profile`を上書きするプロファイルを構成します。 |
| `setOverrideDomain(_:)` | デフォルトURLドメインを置き換えるドメインを構成します。 |
| `setModuleId(_:)` | このモジュールインスタンスのユニークな識別子を構成します。 |
| `setEnabled(_:)` | モジュールを永久に有効または無効にします。 |
| `setOrder(_:)` | モジュールが初期化される順序を構成します。 |
| `setRules(_:)` | このモジュールがイベントを処理するために一致する必要があるルールを構成します。 |
| `setMappings(_:)` | このモジュールのマッピングを構成します。 |

