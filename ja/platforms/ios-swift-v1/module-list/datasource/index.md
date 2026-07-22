---
title: DataSourceモジュール
description: それぞれのディスパッチにデータソース変数を追加します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/datasource/
---
## 使用法


<blockquote>
Swift 1.8.0+を使用している場合、このモジュールはすでにCoreに含まれており、インストールする必要はありません。それ以前のバージョンでは、このガイドに従ってモジュールをインストールしてください。
</blockquote>


DataSourceモジュールは、各ディスパッチにデータソース変数を追加します。

このモジュールの使用は、Tealium Customer Data Hubを使用している場合に推奨されます。Customer Data Hubのユーザーインターフェースでデータソースキーを生成します。Tag Managementのみを使用している場合、現在は新しい変数を各ディスパッチに追加する以外の効果はありません。データソースについて[詳しく学ぶ](https://docs.tealium.com/about-data-sources/)。

以下のプラットフォームがサポートされています：

* iOS
* tvOS
* watchOS
* macOS

## インストール

CocoaPodsまたはCarthageでDataSourceモジュールをインストールします。

### CocoaPods

CocoaPodsでDataSourceモジュールをインストールするには、以下のpodをPodfileに追加します：  
```ruby
pod 'tealium-swift/TealiumDataSource'
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` podに依存性があります。iOSのCocoaPodsインストールについて[詳しく学ぶ](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#cocoapods)。



### Carthage

CarthageでDataSourceモジュールをインストールするには、以下の手順を実行します：

1. Xcodeのアプリターゲットの一般構成ページに移動します。

2. 次のフレームワークを**Embedded Binaries**セクションに追加します：  
      ```ruby
      TealiumDataSource.framework
      ```
3. `TealiumConfig`クラスのインスタンスにデータソースパラメータを構成するために、プロジェクトに以下の必要なインポート文を追加します：   
      ```swift
      import TealiumDataSource
      ```

フレームワークは自動的にインスタンス化されます。`TealiumCore`に依存性があります。追加のインポート文は必要ありません。iOSのCarthageインストールについて[詳しく学ぶ](https://docs.tealium.com/ja/platforms/ios-swift-v1/install/#carthage)。


## データレイヤー
モジュールが有効な間、以下の変数が各トラッキングコールで送信されます：

| 変数           | タイプ | 説明                                          | 例  |
|--------------------|-------|---------------------------------------------------|---------------|
| `tealium_datasource` | `String` | データソース名を指定します。各ディスパッチに追加されます。 | `"abc123"`      |

## APIリファレンス
公開APIメソッドはありません。データソース変数はTealiumConfigオブジェクトを介して構成されます（[Swift Class: TealiumConfig](https://docs.tealium.com/ja/platforms/ios-swift-v1/api/tealium-config/)を参照）


## リリースノート

ビルド1

* 初回リリース

