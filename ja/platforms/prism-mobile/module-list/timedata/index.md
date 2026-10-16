---
title: TimeDataモジュール
description: すべてのトラッキングコールにタイムスタンプデータを追加します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/timedata/
---
TimeDataモジュールは、すべてのトラッキングコールにタイムスタンプとタイムゾーン情報を追加します。

## データレイヤー

このモジュールが有効な間、各トラッキングコールに以下の変数が追加されます：

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `tealium_timestamp_epoch` | 秒単位のUnixタイムスタンプ | `1746547200` |
| `tealium_timestamp_epoch_milliseconds` | ミリ秒単位のUnixタイムスタンプ | `1746547200000` |
| `tealium_timestamp_local` | ISO 8601形式のローカル時間 | `"2025-05-06T07:30:45"` |
| `tealium_timestamp_local_with_offset` | タイムゾーンオフセット付きのISO 8601形式のローカル時間 | `"2025-05-06T07:30:45-07:00"` |
| `tealium_timestamp_offset` | タイムゾーンオフセット（小数時間） | `-7` |
| `tealium_timestamp_timezone` | タイムゾーン識別子 | `"America/Los_Angeles"` |
| `tealium_timestamp_utc` | ISO 8601形式のUTC時間 | `"2025-05-06T14:30:45Z"` |

## インストール



`build.gradle`ファイルに`prism-time-data`依存関係を追加します：

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-time-data")
```


Swift Package Managerを使用して`TealiumPrismTimeData`を依存関係に追加するか、CocoaPods用にPodfileに追加します：

```ruby
pod 'tealium-prism/TimeData'
```



## 初期化



```kotlin
val config = TealiumConfig.Builder(
    accountName = "ACCOUNT",
    profileName = "PROFILE",
    environment = Environment.PROD,
    modules = listOf(
        Modules.timeData(),
        // 他のモジュール...
    )
).build()
```


プログラムでモジュールを構成し、`TealiumConfig`のmodulesパラメータに追加します。

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
                               // 他のモジュール...
                           ])
```

