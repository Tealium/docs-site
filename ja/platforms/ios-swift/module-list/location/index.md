---
title: ロケーションモジュール
description: イベントのためのデバイスの位置情報を提供し、興味のあるポイントの周りにジオフェンスを追加する機能を提供します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/location/
---
ロケーションモジュールは、iOSアプリが位置情報を受け取り、ジオフェンスを構成および監視する機能を有効にします。[詳細はこちら](https://docs.tealium.com/ja/platforms/getting-started-mobile/location/)で位置追跡とジオフェンシングについて学びましょう。

## 対応プラットフォーム

以下のプラットフォームが対応しています：

* [iOS](https://docs.tealium.com/ja/platforms/ios-swift/)

## 要件

* [Tealium for Swift](https://docs.tealium.com/ja/platforms/ios-swift/) (1.9.0+)

## サンプルアプリ

[IOSのサンプルアプリ](https://github.com/Tealium/tealium-swift/tree/master/samples/TealiumSwiftExample)を探索して、当社のライブラリ、追跡方法、およびベストプラクティスの実装に慣れましょう。メインのサンプルアプリにはロケーションモジュールとジオフェンシング機能の例が含まれています。

## インストール

Swift Package Manager、CocoaPods、またはCarthageでロケーションモジュールをインストールします。ロケーションモジュールは、位置イベントを送信するためのディスパッチャー（`TealiumCollect`または`TealiumTagManagement`）を必要とします。

### Swift Package Manager（推奨）

バージョン1.9.0+でサポートされているSwift Package Managerは、Tealium Swiftライブラリをインストールするための推奨される最も簡単な方法です：

1. Xcodeプロジェクトで**ファイル > パッケージ依存関係を追加**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
1. バージョンルールを構成します。通常は`次のメジャーまで`が推奨されます。現在のTealium Swiftライブラリバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットしてください。
1. インストールするモジュールのリストから`ロケーション`モジュールを選択し、Xcodeプロジェクトの**フレームワークとライブラリ**の下にあるアプリターゲットごとに追加します。

[iOSのSwift Package Managerインストールについてもっと学ぶ](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)。

### CocoaPods

CocoaPodsでロケーションモジュールをインストールするには、Podfileに次のポッドを追加します：

```perl
pod 'tealium-swift/Location'
```

[iOSのCocoaPodsインストールについてもっと学ぶ](https://docs.tealium.com/ja/platforms/ios-swift/install/#cocoapods)。

### Carthage

Carthageでロケーションモジュールをインストールするには：

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 次のフレームワークを**組み込みバイナリ**セクションに追加します：
      ```perl
      TealiumLocation.framework
      ```

[iOSのCarthageインストールについてもっと学ぶ](https://docs.tealium.com/ja/platforms/ios-swift/install/#carthage)。

## 初期化

モジュールを初期化するには、`TealiumConfig`の[`collectors`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#collectors)プロパティに指定されていることを確認してください。

`config.collectors = [Collectors.Location]`

`TealiumConfig`インスタンスの[位置精度](#location-tracking)および[ジオフェンシング](#geofencing)の追加オプションも構成可能です。


<blockquote>
[Collectors](https://docs.tealium.com/ja/platforms/ios-swift/modules/#collectors)のドキュメントを確認して、必要なコレクターを正しく指定する方法を理解してください。
</blockquote>


### 認証

アプリが位置情報を収集するための認証を行うには、アプリの`Info.plist`ファイルに次のキーを追加します：

- `Privacy - Location When In Use Usage Description`
- `Privacy - Location Always and When In Use Usage Description`

キーが存在しない場合、位置情報のリクエストは即座に失敗します。[位置情報サービスの認証リクエストについてもっと学ぶ](https://developer.apple.com/documentation/corelocation/requesting_authorization_for_location_services)。

現在の実装内で位置情報の認証をすでにリクエストしていない場合、Tealiumの完了コールバックでロケーションモジュールのAPIメソッド`requestAuthorization()`を使用できます：

```swift
func start() {
      //...
      tealium = Tealium(config: config) { _ in
      		self.tealium?.location?.requestAuthorization()
      }
  }
```
## ジオフェンシング

ジオフェンシングはデフォルトで有効になっており、ジオフェンスを構成するには、以下の方法のいずれかを使用して[ジオフェンス JSON ファイル](https://docs.tealium.com/ja/platforms/getting-started-mobile/location/#json-file)を提供します：

* **ホストされた URL**  
自分のホストされたジオフェンスファイルをURLとして提供します。プロパティ[`geofenceUrl`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#geofenceurl)を使用します。  
このオプションは、公開構成のURLを上書きした場合や[ホストされたデータレイヤー](https://docs.tealium.com/use-case-supplementing-product-data/)を使用したい場合に推奨されます。  
```swift
config.geofenceUrl = "https://example.com/geofences.json"
```
* **ローカルファイル**  
アプリ内に保存されているジオフェンスファイルを使用するには、プロパティ[`geofenceFileName`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#geofencefilename)を構成します。ファイル拡張子は省略します。
```swift
config.geofenceFileName = "geofences" // geofences.json
```

ジオフェンシングを無効にするには、プロパティ[`geofenceTrackingEnabled`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#geofencetrackingenabled)を構成します：

```swift
config.geofenceTrackingEnabled = false
```

## 追加の考慮事項

**アクティブなジオフェンスの数**  
ジオフェンスは動的に追加および削除され、可能な限り少ないリソースを使用します。定義されるジオフェンスの数に制限はありませんが、アクティブなジオフェンスの数はデバイスユーザーごとに20個に制限されています。

**ジオフェンスの初期化**  
作成時にユーザーがジオフェンス内にいる場合、`enter` トランジションイベントは発火しません。これは、`exit` および `enter` トランジションイベントが境界を越えるときに発火され、内部に現れたときには発火されないためです。

## データレイヤー

以下の変数は、モバイルデータレイヤーの一部としてロケーションモジュールによって構成されます。これらの変数はライブラリからの各トラッキングコールに自動的に含まれます。

| 変数名 | タイプ | 説明 | 例 |
|---------------|-----|-------------|----------------------|
| `latitude`     | `String` | ユーザーの最新の記録された位置の緯度 | `32.906119` |
| `longitude`    | `String` |ユーザーの最新の記録された位置の経度 | `-117.2367` |
| `location_accuracy` | `String` | 位置情報の更新が要求される頻度、例えば `high` または `low` | `high`|
| `location_accuracy_extended` | `String` | ロケーションモジュールの精度構成、例えば `best` または `reduced` | `reduced`|

ジオフェンシング中、ユーザーの遷移状態が変化すると、位置データを含むトラッキングコールが送信されます。遷移状態の変化には、ユーザーがジオフェンスに入るか出ることが含まれます。以下の追加変数がデータレイヤーに送信されます：

| 変数名 | タイプ | 説明 | 例 |
|---------------|-----|-------------|----------------------|
| `tealium_event`            | `String` | Tealium によってトラッキングされたジオフェンスイベント | `geofence_entered` または `geofence_exited` |
| `geofence_name`            | `String` | ジオフェンス領域の名前 | `Tealium_San_Diego` |
| `geofence_transition_type` | `String` | ジオフェンス遷移イベントのタイプ | `geofence_entered` または `geofence_exited` |
| `movement_speed`           | `String` | デバイスの瞬間速度、メートル毎秒で測定 | `1.0` |
| `location_timestamp`       | `String` | ユーザーがジオフェンス領域に入った/出た時の記録された日時（GMT） | `2020-01-28 16:29:46 +0000`|

## API リファレンス

ロケーションモジュールで使用されるメソッドのリファレンスについては、iOS APIのTealium SDKの[`LocationModule`](https://docs.tealium.com/ja/platforms/ios-swift/api/location-module/)クラスを参照してください。