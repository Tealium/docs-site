---
title: コレクトモジュール
description: トラッキングコールをTealium Customer Data Hubにディスパッチします。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/collect/
---
## 使用法
コレクトモジュールは、トラッキングコールをTealium Customer Data Hubにディスパッチします。Customer Data Hubを使用している場合、このモジュールの使用を強く推奨します。

代わりに、Tag Managementモジュールを使用している場合は、Tealium iQ経由でCollectタグを使用することもできます。これにより、Customer Data Hubにディスパッチされるデータとイベントの制御がより大きくなり、ロードルールや拡張機能を使用してディスパッチ前のデータを操作することができます。Tealium iQ経由でCollectタグを使用している場合は、重複したトラッキングリクエストを避けるために、Collectモジュールが_無効化_されていることを確認してください。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* watchOS
* macOS

## インストール

CocoaPodsまたはCarthageでCollectモジュールをインストールします。

### CocoaPods

CocoaPodsでCollectモジュールをインストールするには、以下のpodをPodfileに追加します：  
```ruby
pod &#39;tealium-swift/TealiumCollect&#39;
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` podに依存しています。[詳細を学ぶ](/ja/platforms/ios-swift-v1/install/#cocoapods) iOSのCocoaPodsインストールについて。

### Carthage

CarthageでCollectモジュールをインストールするには、以下の手順を実行します：

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 次のフレームワークを**Embedded Binaries**セクションに追加します：  
    ```ruby
    TealiumCollect.framework
    ```

フレームワークは自動的にインスタンス化されます。`TealiumCore`に依存しています。追加のインポートステートメントは必要ありません。[詳細を学ぶ](/ja/platforms/ios-swift-v1/install/#carthage) iOSのCarthageインストールについて。

## データレイヤー
モジュールが有効な間、以下の変数が各トラッキングコールで送信されます：

| 変数         | 説明                                                        | 例  |
|------------------|--------------------------------------------------------------------|---------------|
| `dispatch_service` | トラッキングコールがどのモジュールから来たかを示す静的な文字列 | `&#34;collect&#34;`       |

