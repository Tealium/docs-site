---
title: 接続性モジュール
description: デバイスがネットワーク接続を報告しない場合、自動的にディスパッチをキューに入れます。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/connectivity/
---
## 仕組み

接続性モジュールは、AppleのReachability APIを使用してネットワーク接続を監視し、デバイスがネットワーク接続を報告しない場合、自動的にディスパッチをキューに入れます。

トラッキングコールが送信されるたびに、モジュールは現在の接続状態を確認し、インターネットが到達不可能な場合はリクエストのキューを開始します。新しいトラッキングコールが受信されるたびに、再度接続状態を確認し、接続状態が再び到達可能に変わった場合は、以前にキューに入れられたリクエストがすべて送信され、キューがクリアされます。

さらに、1.6.5以降、接続状態はデフォルトで30秒ごとに自動的に確認されます（`TealiumConfig`で上書き可能）。状態が「到達不可能」から「到達可能」に変わった場合、キューは自動的にフラッシュされます（つまり、キュー内のすべてのトラッキングコールがディスパッチされます）。

自動接続チェックは、接続状態が「到達可能」に変わったときにキャンセルされ、状態が「到達不可能」に検出されたときに再開します。これにより、必要なときだけ接続の変更を監視することでリソースを節約します。

## 使用法
このモジュールの使用は強く推奨されます。これがないと、デバイスがオフラインの場合、ディスパッチが失敗し、ドロップされます。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* macOS
* watchOS

## 要件

* `SystemConfiguration`
* `TealiumDispatchQueue`. コンパイル時の依存関係ではないですが、このモジュールが含まれていない場合、ディスパッチは正常に保存されません。


## インストール

CocoaPodsまたはCarthageで接続性モジュールをインストールします。

### CocoaPods

CocoaPodsで接続性モジュールをインストールするには：

1. Podfileに以下のpodを追加します：  
    ```ruby
    pod 'tealium-swift/TealiumConnectivity'
    ```

2. ディスパッチを永続化するための接続性モジュールを使用する際に必要なpodを追加します：  
    ```ruby
    pod 'tealium-swift/TealiumDispatchQueue'
    ```

フレームワークは自動的にインスタンス化されます。`TealiumCore` podに依存しています。iOSのCocoaPodsインストールについては[こちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)をご覧ください。


### Carthage

Carthageで接続性モジュールをインストールするには、以下の手順を実行します：

1. Xcodeのアプリターゲットの一般構成ページに移動します。

2. 以下のフレームワークを**Embedded Binaries**セクションに追加します：  
    ```ruby
    TealiumConnectivity.framework
    TealiumDispatchQueue.framework
    ```

フレームワークは自動的にインスタンス化されます。`TealiumCore`に依存しています。追加のインポートステートメントは必要ありません。iOSのCarthageインストールについては[こちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)をご覧ください。


## データレイヤー
モジュールが有効な間、以下の変数が各トラッキングコールとともに送信されます：

| 変数   | 説明                                                                                                                      | 例  |
|------------|----------------------------------------------------------------------------------------------------------------------------------|---------------|
| `was_queued` | トラッキングコールが接続性がないためにキューに入れられたかどうかを示します。キューに入れられたイベントのみに存在し、他のすべてのイベントでは存在しません | [`"true"`, `"false"`]   |
| `queue_reason` | このイベントがキューに入れられた理由を示します（現在は`connectivity`または`consent`） | connectivity          |
| `network_connection_type`   | 現在の接続タイプ                                                               | [`"wifi"`, `"cellular"`]             |

