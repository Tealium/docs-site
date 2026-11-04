---
title: Collectモジュール
description: トラッキング呼び出しをTealium Customer Data Hubのサーバーサイド製品に送信します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/collect/
---
## 使用方法

Collectモジュールは、トラッキング呼び出しをTealium Customer Data Hubに送信します。Customer Data Hubをサーバーサイドで使用している場合は、このモジュールを使用することを強く推奨します。

代わりに、Tag Managementモジュールを使用している場合は、Tag ManagementでCollectタグを使用できます。これにより、送信前にロードルールと拡張機能を使用してデータを操作できるため、Customer Data Hubに送信するデータとイベントをより細かく制御できます。Tag ManagementでCollectタグを使用する場合は、トラッキングリクエストが重複しないように、Collectモジュールが無効になっていることを確認してください。

次のプラットフォームがサポートされています。

* iOS
* tvOS
* watchOS
* macOS

## インストール

Swift Package Manager、CocoaPods、またはCarthageを使用してCollectモジュールをインストールします。

### Swift Package Manager（推奨）

バージョン1.9.0以降でサポートされているSwift Package Managerは、Tealium Swiftライブラリをインストールするための最も簡単な推奨方法です。

1. Xcodeプロジェクトで、**File > Add Package Dependencies**を選択します。
1. リポジトリURLとして`https://github.com/tealium/tealium-swift`を入力します。
1. バージョンルールを構成します。通常は`"Up to next major"`を推奨します。現在のTealium Swiftライブラリのバージョンがリストに表示されない場合は、Swiftパッケージのキャッシュをリセットしてください。
1. インストールするモジュールのリストから`Collect`モジュールを選択し、Xcodeプロジェクトの各アプリターゲットにある**Frameworks and Libraries**に追加します。

詳しくは、[iOS向けSwift Package Managerのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#swift-package-manager-recommended)を参照してください。

### CocoaPods

CocoaPodsを使用してCollectモジュールをインストールするには、Podfileに次のpodを追加します。  
```perl
pod 'tealium-swift/Collect'
```

詳しくは、[iOS向けCocoaPodsのインストール](https://docs.tealium.com/ja/platforms/ios-swift/install/#cocoapods)を参照してください。

### Carthage

Carthageを使用してCollectモジュールをインストールするには、次の手順に従います。

1. XcodeでアプリターゲットのGeneral構成ページに移動します。

2. **Embedded Binaries**セクションに次のフレームワークを追加します。  
      ```perl
      TealiumCollect.framework
      ```

iOS向けCarthageのインストールについては、[詳細はこちら](https://docs.tealium.com/ja/platforms/ios-swift/install/#carthage)を参照してください。

## 初期化

モジュールを初期化するには、`TealiumConfig`の`dispatchers`プロパティに指定されていることを確認します。

`config.dispatchers = [Dispatchers.Collect]`

## データレイヤー

モジュールが有効になっている間、トラッキング呼び出しのたびに次の変数が送信されます。

| 変数 | 説明 | 例 |
|------------------|--------------------------------------------------------------------|---------------|
| `dispatch_service` | トラッキング呼び出しの送信元モジュールを示す静的な文字列 | `"collect"` |