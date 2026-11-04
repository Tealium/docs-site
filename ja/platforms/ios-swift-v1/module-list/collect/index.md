---
title: Collectモジュール
description: Tealium Customer Data Hubにトラッキングコールを送信します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/collect/
---
## 使用方法
Collectモジュールは、トラッキングコールをTealium Customer Data Hubに送信します。Customer Data Hubを使用している場合は、このモジュールを使用することを強く推奨します。

別の方法として、Tag Managementモジュールを使用している場合は、Tag ManagementでCollectタグを使用できます。この方法では、ロードルールと拡張機能を使用して送信前にデータを操作できるため、Customer Data Hubに送信するデータやイベントをより細かく制御できます。Tag ManagementでCollectタグを使用する場合は、トラッキングリクエストの重複を避けるため、Collectモジュールが無効になっていることを確認してください。

次のプラットフォームがサポートされています。

* iOS
* tvOS
* watchOS
* macOS

## インストール

CocoaPodsまたはCarthageを使用してCollectモジュールをインストールします。

### CocoaPods

CocoaPodsを使用してCollectモジュールをインストールするには、Podfileに次のpodを追加します。  
```ruby
pod 'tealium-swift/TealiumCollect'
```

フレームワークは自動的にインスタンス化されます。このフレームワークは`TealiumCore` podに依存しています。iOSへのCocoaPodsのインストールについては、[詳細はこちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)を参照してください。


### Carthage

Carthageを使用してCollectモジュールをインストールするには、次の手順を実行します。

1. Xcodeで、アプリターゲットの「General」構成ページに移動します。

2. **Embedded Binaries**セクションに次のフレームワークを追加します。  
    ```ruby
    TealiumCollect.framework
    ```

フレームワークは自動的にインスタンス化されます。このフレームワークは`TealiumCore`に依存しています。追加のimport文は必要ありません。iOSへのCarthageのインストールについては、[詳細はこちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)を参照してください。

## データレイヤー
モジュールが有効になっている間、トラッキングコールごとに次の変数が送信されます。

| 変数         | 説明                                                        | 例  |
|------------------|--------------------------------------------------------------------|---------------|
| `dispatch_service` | トラッキングコールの送信元モジュールを示す固定文字列 | `"collect"`       |