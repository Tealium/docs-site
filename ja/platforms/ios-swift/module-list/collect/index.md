---
title: コレクトモジュール
description: トラッキングコールをTealium Customer Data Hubサーバーサイド製品にディスパッチします。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/collect/
---
## 使用法

コレクトモジュールは、トラッキングコールをTealium Customer Data Hubにディスパッチします。このモジュールは、Customer Data Hubサーバーサイドを使用している場合に強く推奨されます。

代わりに、Tag Managementモジュールを使用している場合は、Tealium iQ経由でCollectタグを使用することもできます。これにより、データとイベントのディスパッチに対する制御がエンリッチメントされ、ロードルールや拡張機能を使用してデータをディスパッチする前に操作することができます。Tealium iQ経由でCollectタグを使用している場合は、重複したトラッキングリクエストを避けるために、Collectモジュールが_無効化_されていることを確認してください。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* watchOS
* macOS

## インストール

Swift Package Manager、CocoaPods、またはCarthageを使用してCollectモジュールをインストールします。

### Swift Package Manager（推奨）

バージョン1.9.0+でサポートされているSwift Package Managerは、Tealium Swiftライブラリをインストールする最も簡単で推奨される方法です：

1. Xcodeプロジェクトで、**File > Add Package Dependencies**を選択します。
1. リポジトリURLを入力します：`https://github.com/tealium/tealium-swift`
1. バージョンルールを構成します。通常、`"Up to next major"`が推奨されます。現在のTealium Swiftライブラリのバージョンがリストに表示されない場合は、Swiftパッケージキャッシュをリセットします。
1. インストールするモジュールのリストから`Collect`モジュールを選択し、Xcodeプロジェクトの各アプリターゲットに追加します。**Frameworks and Libraries**の下にあります。

[iOS向けのSwift Package Managerインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)について詳しく学びましょう。

### CocoaPods

CocoaPodsでCollectモジュールをインストールするには、以下のpodをPodfileに追加します：  
```perl
pod 'tealium-swift/Collect'
```

[iOS向けのCocoaPodsインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#cocoapods)について詳しく学びましょう。

### Carthage

CarthageでCollectモジュールをインストールするには、以下の手順を実行します：

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 次のフレームワークを**Embedded Binaries**セクションに追加します：  
      ```perl
      TealiumCollect.framework
      ```

[iOS向けのCarthageインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#carthage)について詳しく学びましょう。

## 初期化

モジュールを初期化するには、`TealiumConfig`の`dispatchers`プロパティで指定されていることを確認します：

`config.dispatchers = [Dispatchers.Collect]`

## データレイヤー

モジュールが有効な間、各トラッキングコールで以下の変数が送信されます：

| 変数         | 説明                                                        | 例  |
|------------------|--------------------------------------------------------------------|---------------|
| `dispatch_service` | トラッキングコールがどのモジュールから来たかを示す静的な文字列 | `"collect"`       |
