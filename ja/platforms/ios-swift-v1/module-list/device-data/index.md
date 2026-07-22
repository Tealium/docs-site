---
title: DeviceData モジュール
description: 現在のデバイスに関する情報を収集し、トラッキングコール/ディスパッチに追加します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/device-data/
---## 使用法
DeviceData モジュールは、現在のデバイスに関する情報を収集し、トラッキングコール/ディスパッチに追加します。このモジュールの使用を推奨します。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* watchOS
* macOS

## 必要条件

* UIKit
* Darwin
* CoreTelephony
* WatchKit

## インストール

CocoaPods または Carthage を使用して DeviceData モジュールをインストールします。

### CocoaPods

CocoaPods を使用して DeviceData モジュールをインストールするには、以下の pod を Podfile に追加します：  
```ruby
pod 'tealium-swift/TealiumDeviceData'
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` pod に依存性があります。iOS の CocoaPods インストールについては[こちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)をご覧ください。


### Carthage

Carthage を使用して DeviceData モジュールをインストールするには、以下の手順を実行します：

1. Xcode のアプリターゲットの General 構成ページに移動します。

2. 以下のフレームワークを **Embedded Binaries** セクションに追加します：  
      ```ruby
      TealiumDeviceData.framework
      ```

フレームワークは自動的にインスタンス化されます。`TealiumCore` に依存性があります。追加のインポートステートメントは必要ありません。iOS の Carthage インストールについては[こちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)をご覧ください。

## データレイヤー
モジュールが有効な間、以下の変数が各トラッキングコールで送信されます：

| 変数名 | 説明  | 例 |
|---|---| --- |
| `app_memory_usage`   | 現在のプロセス/アプリが使用しているメモリ（メガバイト）| `35.75MB`          |
| `app_orientation`    | アプリの向き（statusBarOrientation から取得；アプリが特定の向きに固定されている場合、デバイスの向きと異なる場合があります）| `Portrait`       |
| `app_orientation_ extended` | アプリの拡張向き（statusBarOrientation から取得；アプリが特定の向きに固定されている場合、デバイスの向きと異なる場合があります）| `Portrait Upside Down` |
| `battery_percent`            | トラックコール時の現在のバッテリー残量（パーセンテージ）| `58`|
| `carrier`                    | モバイルネットワークキャリア名| `EE`|
| `carrier_iso`                | モバイルネットワークのISO国コード| `gb`|
| `carrier_mcc`                | [モバイルネットワークの国コード](https://en.wikipedia.org/wiki/Mobilecountrycode)| `234`|
| `carrier_mnc`                | [モバイルネットワークコード](https://en.wikipedia.org/wiki/Mobilecountrycode)| `34`|
| `connection_type`           | 現在の接続タイプ| [`wifi`, `cellular`]|
| `cpu_architecture`           | CPU アーキテクチャ| `64`|
| `cpu_type`                   | CPU タイプ| `ARM64v8`|
| `device_battery_percent`     | トラックコール時の現在のバッテリー残量（パーセンテージ）| `58`|
| `device_architecture`        | CPU アーキテクチャ| `64`|
| `device`                     | 消費者デバイス名| `iPhone 7 Plus`|
| `device_cputype`             | CPU タイプ| `ARM64v8`|
| `device_is_charging`         | トラックコール時にデバイスが現在充電中であることを示すブール値| [`true`, `false`]|
| `device_language`            | 現在のデバイス言語| `en`|
| `device_orientation`         | シンプルな向き| [`Portrait`, `Landscape`]|
| `device_orientation_ extended`| フル向き| `Face Up`|
| `device_os_version`          | オペレーティングシステムのバージョン| `11.1`|
| `device_resolution`          | 画面解像度| `1080x1920`|
| `device_type`            | Apple の内部デバイス識別子| `iPhone8,4`|
| `memory_active*`             | デバイス上の合計アクティブメモリ| `997.78MB`|
| `memory_compressed*`         | デバイス上の合計圧縮メモリ| `153.39MB`|
| `memory_free*`               | デバイス上の合計空きメモリ| `120.81MB`|
| `memory_inactive*`           | デバイス上の合計非アクティブメモリ| `441.83MB`|
| `memory_physical*`           | デバイス上の合計物理メモリ（RAM）（メガバイト）| `2013.50MB`|
| `memory_wired*`              | デバイス上の合計ワイヤードメモリ| `207.12MB`|
| `model_name`                 | 消費者デバイス名| `iPhone 7 Plus`|
| `model_variant`              | モデルバリアント（一般的にデバイスで利用可能な無線技術を示します）| [`CDMA`, `GSM`, `WiFi`, `Cellular`]|
| `network_connection_ type`    | 現在の接続タイプ| [`wifi`, `cellular`]|
| `network_iso_ country_code`   | モバイルネットワークのISO国コード| `gb`|
| `network_mcc`                | [モバイルネットワークの国コード](https://en.wikipedia.org/wiki/Mobilecountrycode)| `234`|
| `network_mnc`                | [モバイルネットワークコード](https://en.wikipedia.org/wiki/Mobilecountrycode)| `34`|
| `network_name`               | モバイルネットワークキャリア名| `EE`|
| `os_build`                   | オペレーティングシステムビルドバージョン| `15J580`|
| `os_name`                    | オペレーティングシステム名| [`iOS`, `tvOS`, `watchOS`, `macOS`]|
| `os_version`                 | オペレーティングシステムのバージョン| `11.1`|
| `platform`                   | オペレーティングシステム名| [`iOS`, `tvOS`, `watchOS`, `macOS`]|
| `user_locale`                | 現在のデバイス言語| `en`|

* これらの変数は、`TealiumConfig` オブジェクトを介して明示的にメモリデータ収集を有効にした場合にのみ送信されます。デフォルトでは無効になっています。
* これらの変数は、以前のリリースとの後方互換性のために複製されています。

