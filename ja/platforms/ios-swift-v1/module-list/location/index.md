---
title: ロケーションモジュール
description: イベントのデバイス位置情報と、関心のあるポイント周辺にジオフェンスを追加する機能を提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/location/
---
ロケーションモジュールを使用すると、iOSアプリが位置情報を受け取り、ジオフェンスを構成および監視することができます。[詳細を学ぶ](https://docs.tealium.com/ja/platforms/getting-started-mobile/location/) 位置追跡とジオフェンシングについて。

## サポートされているプラットフォーム

以下のプラットフォームがサポートされています：

* [iOS](https://docs.tealium.com/ja/platforms/ios-swift-v1/)

## 要件

* [Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift-v1/) (1.9.0+)

## サンプルアプリ

[ iOSサンプルアプリ](https://github.com/Tealium/tealium-swift/tree/master/samples/TealiumSwiftExample)を探索して、ライブラリ、トラッキング方法、ベストプラクティスの実装に慣れてください。メインのサンプルアプリにはロケーションモジュールが含まれています。

## インストール

Swift Package Manager、CocoaPods、またはCarthageを使用してロケーションモジュールをインストールします。

### Swift Package Manager (推奨)

SPMでロケーションモジュールをインストールするには：

1. リポジトリ：https://www.github.com/Tealium/tealium-swift を使用してXcodeまたはコマンドラインツール内にSwiftパッケージを追加します。

2. Xcodeを使用している場合は、インストールプロセスで `TealiumLocation` ターゲットを選択します。コマンドラインを使用している場合は、 `Package.swift` ファイル内の依存関係リストに `TealiumLocation` モジュールを追加します。

フレームワークは自動的にインスタンス化されます。 `TealiumCore` に依存性があり、ディスパッチャー（ `TealiumCollect` または `TealiumTagManagement` ）が必要です。追加のインポートステートメントは必要ありません。

[詳細を学ぶ](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#swift-package-manager-recommended) iOSのSPMインストールについて。

### CocoaPods

CocoaPodsでロケーションモジュールをインストールするには、次のポッドをPodfileに追加します：

```ruby
pod 'tealium-swift/TealiumLocation'
```

フレームワークは自動的にインスタンス化されます。 `TealiumCore` ポッドに依存性があり、ディスパッチャー（ `TealiumCollect` または `TealiumTagManagement` ）が必要です。[詳細を学ぶ](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods) iOSのCocoaPodsインストールについて。

### Carthage

Carthageでロケーションモジュールをインストールするには：

1. Xcodeのアプリターゲットの一般構成ページに移動します。

2. 次のフレームワークを **Embedded Binaries** セクションに追加します：  
    ```ruby
    TealiumLocation.framework
    ```
フレームワークは自動的にインスタンス化されます。 `TealiumCore` に依存性があり、ディスパッチャー（ `TealiumCollect` または `TealiumTagManagement` ）が必要です。追加のインポートステートメントは必要ありません。[詳細を学ぶ](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage) iOSのCarthageインストールについて。

## 初期化

モジュールがアプリに追加されると、ロケーショントラッキングがデフォルトで有効になります。 [位置精度](#location-tracking) と [ジオフェンシング](#geofencing) の構成オプションは、 `TealiumConfig` のインスタンスのプロパティを使用して構成されます。

### 権限

アプリが位置情報を収集するための権限を与えるには、次のキーをアプリの `Info.plist` ファイルに追加します：

- `Privacy - Location When In Use Usage Description`
- `Privacy - Location Always and When In Use Usage Description`

キーが存在しない場合、位置情報のリクエストはすぐに失敗します。 [詳細を学ぶ](https://developer.apple.com/documentation/corelocation/requesting_authorization_for_location_services) 位置情報サービスの承認をリクエストする方法について。

## 位置追跡

ロケーションモジュールは連続的な位置追跡を行います。位置の更新は精度と距離の2つの構成に基づいています。

デフォルトでは、重要な位置の更新のみが監視されます。これにより、更新が少なくなり、バッテリーの消費が少なくなります。

より高精度の更新を有効にするには、 [`useHighAccuracy`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#usehighaccuracy) プロパティを `true` に構成し、 [`updateDistance`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#updatedistance) プロパティを更新をトリガーするメートル単位の値に構成します。

```swift
func start() {
      let config = TealiumConfig(account: "ACCOUNT",
                                 profile: "PROFILE",
                                 environment: "ENVIRONMENT",
                                 datasource: "DATASOURCE",
                                 optionalData: nil)
      config.useHighAccuracy = true
      config.updateDistance = 150
      //...
  }
```

## ジオフェンシング

ジオフェンシングを有効にするには、次のいずれかの方法を使用して、[ジオフェンスJSONファイル](https://docs.tealium.com/ja/platforms/getting-started-mobile/location/#json-file)を提供します：

* **ホストされたURL**  
自分でホストしたジオフェンスファイルを使用し、プロパティ [`geofenceUrl`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#geofenceurl) にURLを提供します。   
パブリッシュ構成のURLを上書きした場合や、[ホストされたデータレイヤー](https://docs.tealium.com/use-case-supplementing-product-data/)を使用したい場合に推奨されます。    
```swift
config.geofenceUrl = "https://example.com/geofences.json"
```
* **ローカルファイル**  
アプリに保存されたジオフェンスファイルを使用し、プロパティ [`geofenceFileName`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/#geofencefilename) を構成します。ファイル拡張子は省略します。
```swift
config.geofenceFileName = "geofences" // geofences.json
```

## 追加の考慮事項

**アクティブなジオフェンスの数**  
ジオフェンスは動的に追加および削除され、可能な限り少ないリソースを使用します。ジオフェンスの定義数には制限がありませんが、アクティブなジオフェンスの数は、_すべての_ 実行中のアプリケーションを通じてデバイスユーザーごとに20に制限されています。

**ジオフェンスの初期化**  
ユーザーがジオフェンスの作成時にジオフェンス内にいる場合、 `"enter"` トランジションイベントは発生しません。これは、 `"exit"` と `"enter"` トランジションイベントは、境界を越えるときに発生し、内部に現れるときではないためです。

## データレイヤー

以下の変数は、ロケーションモジュールによってモバイルデータレイヤーの一部として構成されます。これらの変数は、ライブラリからの各トラッキング呼び出しに自動的に含まれます。

| 変数名 | タイプ | 説明 | 例             |
|---------------|-----|-------------|----------------------|
| `latitude`     | `String` | ユーザーの最近記録された位置の緯度 | `"32.906119"` |
| `longitude`    | `String` |ユーザーの最近記録された位置の経度 | `"-117.2367"` |
| `location_accuracy` | `String` | ロケーションモジュールの精度構成、例えば `"high"` または `"low"` | `"high"`|

ジオフェンシング中に、ユーザーの遷移状態が変化すると、位置データを含むトラッキング呼び出しが送信されます。遷移状態の変化には、ユーザーがジオフェンスに入るか出ることが含まれます。次の追加の変数がデータレイヤーに送信されます：

| 変数名 | タイプ | 説明 | 例             |
|---------------|-----|-------------|----------------------|
| `tealium_event`            | `String` | Tealiumが追跡したジオフェンスイベント | `"geofence_entered"` または `"geofence_exited"` |
| `geofence_name`            | `String` | ジオフェンス領域の名前 | `"Tealium_San_Diego"` |
| `geofence_transition_type` | `String` | ジオフェンス遷移イベントのタイプ | `"geofence_entered"` または `"geofence_exited"` |
| `movement_speed`           | `String` | デバイスの瞬間速度、メートル/秒で測定 | `"1.0"` |
| `location_timestamp`       | `String` | ユーザーがジオフェンス領域に入った/出た日時（GMT）を記録 | `"2020-01-28 16:29:46 +0000"`|

## APIリファレンス

ロケーションモジュールで使用されるメソッドのリファレンスについては、iOS APIのTealium SDKの [`TealiumConfig`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/) クラスを参照してください。
