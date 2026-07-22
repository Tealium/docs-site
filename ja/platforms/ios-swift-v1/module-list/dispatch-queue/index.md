---
title: DispatchQueue モジュール
description: このモジュールは、デバイスがオフラインの間に保留中のディスパッチをディスクに保存するために、Connectivityモジュールと連携して動作します。接続が回復すると、イベントのキューが送信されます。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/dispatch-queue/
---
## 使用法

DispatchQueueモジュールは、ConnectivityモジュールおよびConsent Managerモジュールと連携して、デバイスがオフラインであるか、ユーザーがまだトラッキングに同意していない間、保留中のディスパッチをディスクに保存します。接続が回復した場合、またはユーザーがトラッキングに同意した場合、ディスパッチのキューが送信されます。キューにはディスパッチが20件までデフォルトで制限されており、これを超えると最も古いディスパッチが最新のものに取って代わるためにクリアされます。データはUserDefaultsに保存されます。

このモジュールの使用は、Consent ManagerまたはConnectivityモジュールを使用している場合に必要です。それ以外の場合でも、TealiumCoreモジュールによるイベントの事前初期化キューイングを支援するために強く推奨されています。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* watchOS
* macOS

## インストール

DispatchQueueモジュールは、CocoaPodsまたはCarthageでインストールします。

### CocoaPods

CocoaPodsでDispatchQueueモジュールをインストールするには、以下のpodをPodfileに追加します：  
```ruby
pod 'tealium-swift/TealiumDispatchQueue'
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` podに依存性があります。iOSのCocoaPodsインストールについては[こちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)をご覧ください。

### Carthage

CarthageでDispatchQueueモジュールをインストールするには、以下の手順を実行します：

1. Xcodeのアプリターゲットの一般構成ページに移動します。

2. 次のフレームワークを**Embedded Binaries**セクションに追加します：  
      ```ruby
      TealiumDispatchQueue.framework
      ```

フレームワークは自動的にインスタンス化されます。`TealiumCore`に依存性があります。追加のインポートステートメントは必要ありません。iOSのCarthageインストールについては[こちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)をご覧ください。

## データレイヤー
モジュールが有効な間、以下の変数が各トラッキング呼び出しで送信されます：

| 変数| 説明| 例の値|
|-----------------------------------|--------------------------------|--------------------------------------|
|`was_queued`|ディスパッチがキューに入れられたことを示す|[`"true"`, `"false"`]|

## API リファレンス

このモジュールには公開APIメソッドはありません。成功と失敗はDelegateモジュールを通じて監視することができます。

以下の追加メソッドは[`TealiumConfig`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/)クラスによって提供されます：

### `setMaxQueueSize()`

ディスパッチの保存用の最大永続キューサイズを構成します。デフォルトは20イベントです。

```swift
tealConfig.setMaxQueueSize(size)
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `size` | `Int` | ディスパッチの保存用の最大永続キューサイズ（デフォルト：`20`）| `50` |

### `getMaxQueueSize()`

最大キューサイズを取得します。

```swift
tealConfig.getMaxQueueSize();
```

| 戻り値 | 戻り値のタイプ |
| --- | --- |
| ディスパッチの保存用の最大永続キューサイズ | `Int` |

