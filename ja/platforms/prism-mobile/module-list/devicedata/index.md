---
title: DeviceDataモジュール
description: すべてのトラッキングイベントにデバイス情報を自動的に追加します。
url: https://docs.tealium.com/ja/platforms/prism-mobile/module-list/devicedata/
---
DeviceDataモジュールは、モデル、CPUタイプ、OSバージョンなどの静的なデバイス特性と、バッテリー状態や画面の向きなどの動的な情報を収集し、すべてのトラッキングイベントで利用できるようにします。

## データレイヤー

### デバイス

モジュールが有効な間、各トラッキング呼び出しに以下のデバイス属性が追加されます。

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `device` | 一般向けデバイス名 | `"iPhone 13 Pro Max"` |
| `device_architecture` | CPUアーキテクチャ | `"64"` |
| `device_cputype` | 詳細なCPUタイプ | `"ARM64e"` |
| `device_language` | デバイスの優先言語 | `"en-US"` |
| `device_manufacturer` | デバイスの製造元 | `"Apple"` |
| `device_model` | 一般向けデバイス名 | `"iPhone 13 Pro Max"` |
| `device_os_build` | OSビルド番号 | `"20A372"` |
| `device_os_version` | オペレーティングシステムのバージョン | `"17.0"` |
| `device_type` | プラットフォームのモデル識別子 | `"iPhone14,3"` |
| `model_variant` | モデルバリアント識別子 | `"A2484"` |
| `origin` | デバイスカテゴリー | `"mobile"` |
| `os_name` | オペレーティングシステム名 | `"iOS"` |
| `platform` | 小文字のOS名 | `"ios"` |


### バッテリーと画面

iOSでは、ビルダー構成に基づいて以下のバッテリー属性と画面属性を有効または無効にできます。Androidでは、これらの属性は常に送信されます。詳細については、[初期化](#initialize)を参照してください。

| 変数 | 説明 | 例 |
| :--- | :--- | :--- |
| `device_battery_percent` | バッテリー充電率 | `"58"` |
| `device_ischarging` | デバイスが充電中かどうか | `"true"` |
| `device_logical_resolution` | 論理画面解像度 | `"390x844"` |
| `device_orientation` | デバイスの向き | `"Portrait"` |
| `device_orientation_extended` | （iOSのみ）詳細な向き | `"Face Up"` |
| `device_resolution` | 物理画面解像度 | `"1170x2532"` |

### メモリ（iOSのみ）

iOSアプリでは、メモリ使用量をトラッキングする属性を有効にできます。これらのメモリ属性はデフォルトで無効になっています。詳細については、[初期化](#initialize)を参照してください。

| 変数 | 説明 |
| :--- | :--- |
| `memory_active` | アクティブメモリ |
| `memory_compressed` | 圧縮メモリ |
| `memory_free` | 空きメモリ |
| `memory_inactive` | 非アクティブメモリ |
| `memory_physical` | 物理メモリ（RAM）の合計 |
| `memory_wired` | Wiredメモリ |

## インストール



DeviceDataモジュールは`prism-core`に含まれています。`build.gradle`ファイルに以下を追加します。

```kotlin
implementation(platform("com.tealium.prism:prism-bom:0.7.0"))
implementation("com.tealium.prism:prism-core")
```


DeviceDataモジュールは`TealiumPrismCore`に含まれています。リポジトリURL `https://github.com/Tealium/tealium-prism-swift`を使用してSwift Package Managerの依存関係として追加するか、CocoaPods用のPodfileに追加します。

```ruby
pod 'tealium-prism/Core'
```



## 初期化

DeviceDataモジュールは、構成されると自動的に初期化されます。ほとんどの統合では、コードを変更する必要はありません。TealiumプラットフォームのUIでモジュールを構成するか、ローカルのJSON構成ファイルをアプリにバンドルします。



```kotlin
val config = TealiumConfig.Builder(
    application = application,
    accountName = "ACCOUNT",
    profileName = "PROFILE",
    environment = Environment.PROD,
    modules = listOf(
        Modules.deviceData(),
        // other modules...
    )
).build()
```


デバイスデータの種類を有効または無効にするには、`DeviceDataSettingsBuilder`を使用します。
詳細については、[`DeviceDataSettingsBuilder`](https://docs.tealium.com/tealium-prism-swift/TealiumPrismCore/Classes/DeviceDataSettingsBuilder.html)を参照してください。
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
                              // other modules...
                          ])
```

