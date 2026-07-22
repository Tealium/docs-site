---
title: DeviceDataモジュール
description: データレイヤーにデバイスに関する情報を追加します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/device-data/
---
## 使用方法
DeviceDataモジュールは、現在のデバイスに関する情報を収集し、データレイヤーに追加します。このモジュールの使用を推奨します。

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

このモジュールはCoreライブラリに含まれており、別途インストールの必要はありません。

## 初期化

モジュールを初期化するには、`TealiumConfig`の[`collectors`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#collectors)プロパティに指定されていることを確認してください。

```swift
config.collectors = [Collectors.DeviceData]
```


<blockquote>
[Collectors](https://docs.tealium.com/ja/platforms/ios-swift/modules/#collectors)のドキュメントを確認し、必要なコレクターを正しく指定する方法を理解してください。
</blockquote>


## データレイヤー
モジュールが有効な間に各トラッキングコールで送信される変数は以下の通りです：

| 変数名 | 説明  | 例 |
|---|---| --- |
| `app_memory_usage`   | 現在のプロセス/アプリが使用しているメモリ（メガバイト）| `35.75MB`|
| `carrier`                    | モバイルネットワークキャリア名| `EE`|
| `carrier_iso`                | モバイルキャリアISO| `gb`|
| `carrier_mcc`                | キャリアのモバイル国コード| `234`|
| `carrier_mnc`                | キャリアのモバイルネットワークコード| `34`|
| `connection_type`            | 現在の接続タイプ| `wifi`, `cellular`|
| `device`                     | 消費者デバイス名| `iPhone 7 Plus`|
| `device_architecture`        | デバイスアーキテクチャ| `64`|
| `device_battery_percent`     | トラックコール時の現在のバッテリー残量| `58`|
| `device_cputype`             | デバイスCPUタイプ| `ARM64v8`|
| `device_ischarging`          | トラックコール時にデバイスが充電中であるかどうかを示すブール値| `true`|
| `device_language`            | 現在のデバイス言語| `en-US`|
| `device_logical_resolution`            | ポイント（ピクセルではない）での画面寸法| `430x932`|
| `device_manufacturer`            | 製品/ハードウェアメーカー| `Apple`|
| `device_orientation`         | シンプルな方向| `Portrait`, `Landscape`|
| `device_orientation_extended`| 完全な方向| `Face Up`|
| `device_os_build`          | オペレーティングシステムビルド| `20A372`|
| `device_os_version`          | オペレーティングシステムバージョン| `11.1`|
| `device_resolution`          | 画面解像度| `1080x1920`|
| `device_type`            | Apple内部デバイス識別子| `iPhone8,4`|
| `memory_active*`             | デバイス上のアクティブメモリの合計| `997.78MB`|
| `memory_compressed*`         | デバイス上の圧縮メモリの合計| `153.39MB`|
| `memory_free*`               | デバイス上の空きメモリの合計| `120.81MB`|
| `memory_inactive*`           | デバイス上の非アクティブメモリの合計| `441.83MB`|
| `memory_physical*`           | デバイス上の物理メモリ（RAM）の合計（メガバイト）| `2013.50MB`|
| `memory_wired*`              | デバイス上のワイヤードメモリの合計| `207.12MB`|
| `model_name`                 | モデル名| `iPhone 7 Plus`|
| `model_variant`              | モデルバリアント（通常、デバイスで利用可能な無線技術を示します）| `CDMA`, `GSM`, `WiFi`, `Cellular`|
| `network_iso_country_code`   | モバイルネットワークISO国コード| `gb`|
| `os_name`                    | オペレーティングシステム名| `iOS`, `tvOS`, `watchOS`, `macOS`|
| `platform`                   | オペレーティングシステム名（小文字）| `ios`, `tvos`, `watchos`, `macos`|

\* これらの変数は、`TealiumConfig`オブジェクトを介してメモリデータ収集を明示的に有効にした場合にのみ送信されます。デフォルトでは無効になっています。
