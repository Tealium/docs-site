---
title: TimeDataモジュール
description: すべてのトラッキング呼び出しにタイムスタンプデータを追加します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/timedata/
---
TimeDataモジュールは、すべてのトラッキング呼び出しにタイムスタンプとタイムゾーンの情報を追加します。

## データレイヤー

モジュールが有効な間、各トラッキング呼び出しに次の変数が追加されます。

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `tealium_timestamp_epoch` | 秒単位のUnixタイムスタンプ | `1746547200` |
| `tealium_timestamp_epoch_milliseconds` | ミリ秒単位のUnixタイムスタンプ | `1746547200000` |
| `tealium_timestamp_local` | ISO 8601形式のローカル時刻 | `"2025-05-06T07:30:45"` |
| `tealium_timestamp_local_with_offset` | タイムゾーンオフセットを含むISO 8601形式のローカル時刻 | `"2025-05-06T07:30:45-07:00"` |
| `tealium_timestamp_offset` | 10進数の時間単位で表したタイムゾーンオフセット | `-7` |
| `tealium_timestamp_timezone` | タイムゾーン識別子 | `"America/Los_Angeles"` |
| `tealium_timestamp_utc` | ISO 8601形式のUTC時刻 | `"2025-05-06T14:30:45Z"` |

## インストール



TimeDataモジュールは`prism-core`に含まれています。`build.gradle`ファイルに追加します。

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-core")
```


TimeDataモジュールは`TealiumPrismCore`に含まれています。リポジトリURL `https://github.com/Tealium/tealium-prism-swift`を使用してSwift Package Managerの依存関係として追加するか、CocoaPods用のPodfileに追加します。

```ruby
pod 'tealium-prism/Core'
```



## 初期化



```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "ACCOUNT",
    profileName = "PROFILE",
    environment = Environment.PROD,
    modules = listOf(
        Modules.timeData(),
        // other modules...
    )
).build()
```


`TealiumConfig`のmodulesパラメータにモジュールを追加して、プログラムで構成します。

モジュール構成の詳細については、[`TimeDataSettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/timedata.html)を参照してください。

```swift
let config = TealiumConfig(account: "ACCOUNT",
                           profile: "PROFILE",
                           environment: "dev",
                           modules: [
                               Modules.timeData(forcingSettings: { builder in
                                   builder.setEnabled(true)
                                          .setOrder(1)
                                          .setRules(.just("rule_id_from_settings"))
                               }),
                               // other modules...
                           ])
```

