---
title: PersistentData モジュール
description: データ変数をディスクに保存し、それらを各ディスパッチ/トラッキングコールに自動的に追加します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/persistent-data/
---
## 使用法

PersistentData モジュールは、ディスク上に変数を保存し、それらを各トラッキングコールに自動的に含めます。このモジュールの使用が推奨されます。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* watchOS
* macOS

## インストール

CocoaPods または Carthage を使用して PersistentData モジュールをインストールします。

### CocoaPods

CocoaPods を使用して PersistentData モジュールをインストールするには、以下を Podfile に追加します：

```ruby
pod 'tealium-swift/TealiumPersistentData'
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` pod に依存性があります。iOS の CocoaPods インストールについては[こちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)をご覧ください。



### Carthage

Carthage を使用して PersistentData モジュールをインストールするには、以下の手順を実行します：

1. Xcode のアプリターゲットの General 構成ページに移動します。

2. 次のフレームワークを **Embedded Binaries** セクションに追加します：

      ```ruby
      TealiumPersistentData.framework
      ```  
3. 次のインポートステートメントをヘルパーファイルに追加します：  

      ```swift  
      import TealiumPersistentData
      ```

フレームワークは自動的にインスタンス化されます。`TealiumCore` に依存性があります。iOS の Carthage インストールについては[こちら](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)をご覧ください。

## API リファレンス

iOS (Swift) API の [`TealiumPersistentData`](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-persistent-data/) クラスを参照してください。
