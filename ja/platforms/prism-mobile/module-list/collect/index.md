---
title: Collectモジュール
description: トラッキング呼び出しをTealium Collectサービスに送信します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/collect/
---
## 仕組み

Collectモジュールは、トラッキングイベントをTealium Collectサービスに送信するディスパッチャーです。単一イベントの送信とイベントのバッチ処理の両方に対応し、イベント数と訪問IDに基づいて配信を自動的に最適化します。エンドポイント、プロファイルのオーバーライド、ドメイン構成をカスタマイズできます。

## 構成

Collectモジュールでは、次の構成オプションを使用できます。

| 構成               | JSONキー             | 説明                                                                        | デフォルト値                                 |
|--------------------|----------------------|-----------------------------------------------------------------------------|----------------------------------------------|
| URL                | `url`                | 単一イベントの送信に使用するURL。                                           | `https://collect.tealiumiq.com/event`        |
| バッチURL          | `batch_url`          | イベントのバッチ送信に使用するURL。                                         | `https://collect.tealiumiq.com/bulk-event`   |
| プロファイルのオーバーライド | `override_profile`   | イベントデータ内の`TealiumConfig.profile`をオーバーライドするプロファイル。 | なし                                         |
| ドメインのオーバーライド | `override_domain`    | デフォルトURLのドメインを置き換えるドメイン（明示的なURLはオーバーライドしません）。 | なし                                         |

JSON構成ファイル、プログラム、またはその両方を組み合わせてモジュールを構成します。

### JSONファイルによる構成

ローカル構成ファイルを使用するには、`TealiumConfig`の`settingsFile`にファイル名を渡します。リモート構成を使用するには、`settingsUrl`にURLを渡します。両方を同時に使用することもできます。

次の例は、サポートされているJSON構造を示しています。

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

`TealiumConfig`のモジュールに追加することで、モジュールをプログラムで構成します。


<blockquote>
Programmatic settings always take precedence over local and remote settings.
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

異なる構成の異なるエンドポイントにイベントを送信する必要がある場合は、複数のCollectインスタンスを使用します。たとえば、すべてのイベントをプライマリエンドポイントに送信しながら、ルールでフィルタリングした一部のイベントをセカンダリエンドポイントにもルーティングできます。

各インスタンスには一意の`moduleId`が必要です。各インスタンスが処理するイベントを制御するには、ルールを使用します。



```kotlin
val config = TealiumConfig.Builder(
    application,
    "ACCOUNT",
    "PROFILE",
    Environment.DEV,
    emptyList()
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
                                             .setRules(.just("purchase_rule_id"))
                                  }
                              ),
                              // other modules...
                          ])
```



JSON形式での同等の構成は次のとおりです。

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
            "rules": "purchase_rule_id"
        }
    }
}
```
## 構成ビルダーのリファレンス

Collect モジュールの構成には `CollectSettingsBuilder` を使用します。次のメソッドを使用できます。



詳細については、[`CollectSettingsBuilder`](https://docs.tealium.com/tealium-prism-kotlin/core/com.tealium.prism.core.api.settings.modules/-collect-settings-builder/) を参照してください。


| メソッド | 説明 |
|---|---|
| `setUrl(url: String)` | 個々のイベントの送信に使用する URL を構成します。 |
| `setBatchUrl(url: String)` | イベントのバッチ送信に使用する URL を構成します。 |
| `setProfile(profile: String)` | イベントの送信時に使用する Tealium プロファイルを構成します。 |
| `setDomain(domain: String)` | デフォルトの個別送信 URL およびバッチ送信 URL の代わりに使用するドメインを構成します。 |
| `setModuleId(moduleId: String)` | このモジュールインスタンスの一意の識別子を構成します。 |
| `setEnabled(enabled: Boolean)` | モジュールを永続的に有効または無効にします。 |
| `setOrder(order: Int)` | モジュールを初期化する順序を構成します。 |
| `setRules(rules: Rule<String>)` | このモジュールがイベントを処理するために一致する必要があるルールを構成します。 |
| `setMappings(mappings: ...)` | このモジュールのマッピングを構成します。 |


詳細については、[`CollectSettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/CollectSettingsBuilder.html) を参照してください。

| メソッド | 説明 |
|---|---|
| `setUrl(_:)` | 個々のイベントの送信に使用する URL を構成します。 |
| `setBatchUrl(_:)` | イベントのバッチ送信に使用する URL を構成します。 |
| `setOverrideProfile(_:)` | イベントデータ内の `TealiumConfig.profile` をオーバーライドするプロファイルを構成します。 |
| `setOverrideDomain(_:)` | デフォルト URL のドメインを置き換えるドメインを構成します。 |
| `setModuleId(_:)` | このモジュールインスタンスの一意の識別子を構成します。 |
| `setEnabled(_:)` | モジュールを永続的に有効または無効にします。 |
| `setOrder(_:)` | モジュールを初期化する順序を構成します。 |
| `setRules(_:)` | このモジュールがイベントを処理するために一致する必要があるルールを構成します。 |
| `setMappings(_:)` | このモジュールのマッピングを構成します。 |

