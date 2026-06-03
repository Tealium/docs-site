---
title: ロガーモジュール
description: LLDBコンソールへのデバッグ情報のロギングを可能にします。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/logger/
---
## 使用法

ロガーモジュールは、LLDBコンソールへのデバッグ情報のロギングを可能にします。

このモジュールの使用は推奨されています。有効にしない場合、Tealiumライブラリからのロギングはありません。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* watchOS
* macOS

## インストール

CocoaPodsまたはCarthageでロガーモジュールをインストールします。

### CocoaPods

CocoaPodsでロガーモジュールをインストールするには、以下のpodをPodfileに追加します：  
```ruby
pod &#39;tealium-swift/TealiumLogger&#39;
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` podに依存性があります。iOSのCocoaPodsインストールについては[こちら](/ja/platforms/ios-swift-v1/install/#cocoapods)をご覧ください。

### Carthage

Carthageでロガーモジュールをインストールするには、以下の手順を実行します：

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 次のフレームワークを**Embedded Binaries**セクションに追加します：  
      ```ruby
      TealiumLogger.framework
      ```

フレームワークは自動的にインスタンス化されます。`TealiumCore`に依存性があります。追加のインポートステートメントは必要ありません。iOSのCarthageインストールについては[こちら](/ja/platforms/ios-swift-v1/install/#carthage)をご覧ください。

## データレイヤー
このモジュールによって新たな変数は導入されません。

## APIリファレンス
このモジュールには公開APIメソッドはありません。`TealiumConfig`オブジェクトで利用可能な構成を使用してモジュールを制御します。

## ログレベル

以下のログレベルが利用可能です：

| ログレベル | 説明                                                                         | Enum値                    |
|-----------|-------------------------------------------------------------------------------------|-------------------------------|
| `None`      | ロギングは無効化されます。                                                                | `TealiumLogLevelValue.none`    |
| `Errors`    | エラーのみが報告されます。                                                        | `TealiumLogLevelValue.errors`   |
| `Warnings`  | エラーと警告のみが報告されます。                                           | `TealiumLogLevelValue.warnings` |
| `Verbose`   | すべてのログ出力が報告されます、各トラッキング呼び出し/ディスパッチに対するエントリを含む。 | `TealiumLogLevelValue.verbose`  |
