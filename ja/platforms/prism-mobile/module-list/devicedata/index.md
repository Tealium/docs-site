---
title: DeviceDataモジュール
description: すべてのトラッキングイベントにデバイス情報を自動的に追加します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/devicedata/
---
DeviceDataモジュールは、モデル、CPUタイプ、OSバージョンなどの静的なデバイス特性と、バッテリー状態や画面の向きなどの動的情報を収集し、すべてのトラッキングイベントで利用可能にします。

## データレイヤー

### デバイス

モジュールが有効な間、以下のデバイス属性が各トラッキングコールに追加されます：

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `device` | 消費者デバイス名 | `"iPhone 13 Pro Max"` |
| `device_architecture` | CPUアーキテクチャ | `"64"` |
| `device_cputype` | 詳細なCPUタイプ | `"ARM64e"` |
| `device_language` | 主要デバイス言語 | `"en-US"` |
| `device_manufacturer` | デバイス製造者 | `"Apple"` |
| `device_model` | 消費者デバイス名 | `"iPhone 13 Pro Max"` |
| `device_os_build` | OSビルド番号 | `"20A372"` |
| `device_os_version` | オペレーティングシステムバージョン | `"17.0"` |
| `device_type` | プラットフォームモデル識別子 | `"iPhone14,3"` |
| `model_variant` | モデルバリアント識別子 | `"A2484"` |
| `origin` | デバイスカテゴリ | `"mobile"` |
| `os_name` | オペレーティングシステム名 | `"iOS"` |
| `platform` | 小文字のOS名 | `"ios"` |


### バッテリーと画面

以下のバッテリーと画面の属性は、ビルダー構成に基づいて有効または無効にすることができます。詳細は[初期化](#initialize)を参照してください。

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `device_battery_percent` | (iOSのみ) バッテリー充電率 | `"58"` |
| `device_ischarging` | (iOSのみ) デバイスが充電中かどうか | `"true"` |
| `device_logical_resolution` | 論理画面解像度 | `"390x844"` |
| `device_orientation` | デバイスの向き | `"Portrait"` |
| `device_orientation_extended` | 詳細な向き | `"Face Up"` |
| `device_resolution` | 物理画面解像度 | `"1170x2532"` |

### メモリー (iOSのみ)

iOSアプリは、メモリ使用量を追跡するための属性を有効にすることができます。これらのメモリ属性はデフォルトでは無効です。詳細は[初期化](#initialize)を参照してください。

| 変数 | 説明 |
| :--- | :--- |
| `memory_active` | アクティブメモリ |
| `memory_compressed` | 圧縮メモリ |
| `memory_free` | 空きメモリ |
| `memory_inactive` | 非アクティブメモリ |
| `memory_physical` | 総物理メモリ（RAM） |
| `memory_wired` | ワイヤードメモリ |

## インストール



`build.gradle`ファイルに`prism-device-data`依存関係を追加します：

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-device-data")
```


Swift Package Managerの依存関係として`TealiumPrismDeviceData`を追加するか、CocoaPods用にPodfileに追加します：

```ruby
pod 'tealium-prism/DeviceData'
```



## 初期化

DeviceDataモジュールは構成時に自動的に初期化されます。ほとんどの統合ではコード変更は必要ありません。TealiumプラットフォームUIでモジュールを構成するか、アプリにローカルJSON構成ファイルをバンドルします。



```kotlin
val config = TealiumConfig.Builder(
    accountName = "ACCOUNT",
    profileName = "PROFILE",
    environment = Environment.PROD,
    modules = listOf(
        Modules.deviceData(),
        // その他のモジュール...
    )
).build()
```


`DeviceDataSettingsBuilder`を使用してデバイスデータタイプを有効または無効にします。
詳細は[`DeviceDataSettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/DeviceDataSettingsBuilder.html)を参照してください。
```swift
let config = TealiumConfig(account: "ACCOUNT",
                          profile: "PROFILE", 
                          environment: "dev",
                          modules: [
                              Modules.deviceData(forcingSettings: { builder in
                                  builder.setDeviceNamesUrl("https://custom-endpoint.example.com/device_names.json")
                                         .setMemoryReportingEnabled(true)
                                         .setBatteryReportingEnabled(false)
                                         .setScreenReportingEnabled(true)
                                         .setEnabled(true)
                                         .setOrder(1)
                                        .setRules(.just("rule_id_from_settings"))
                              }),
                              // その他のモジュール...
                          ])
```

