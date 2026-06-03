---
title: AppDataモジュール
description: アプリバンドルに関する重要な情報を収集します。
url: https://docs.tealium.com/ja/platforms/ios-swift-v1/module-list/appdata/
---
## 使用法
AppDataモジュールは、アプリバンドルに関する重要な情報を収集します。このモジュールの使用は推奨されますが、必須ではありません。除外することを選択した場合、データレイヤー変数はトラッキングコールに含まれません。

以下のプラットフォームがサポートされています：

* iOS
* macOS
* watchOS
* tvOS

## インストール

CocoaPodsまたはCarthageでAppDataモジュールをインストールします。

### CocoaPods

CocoaPodsでAppDataモジュールをインストールするには、以下のpodをPodfileに追加します：  
```ruby
pod &#39;tealium-swift/TealiumAppData&#39;
```

フレームワークは自動的にインスタンス化されます。`TealiumCore` podに依存性があります。iOSのCocoaPodsインストールについて[詳しくはこちら](/ja/platforms/ios-swift-v1/install/#cocoapods)をご覧ください。

### Carthage

CarthageでAppDataモジュールをインストールするには、以下の手順を実行します：

1. Xcodeでアプリターゲットの一般構成ページに移動します。

2. 以下のフレームワークを**Embedded Binaries**セクションに追加します：  
    ```ruby
    TealiumAppData.framework
    ```

フレームワークは自動的にインスタンス化されます。`TealiumCore`に依存性があります。追加のインポートステートメントは必要ありません。iOSのCarthageインストールについて[詳しくはこちら](/ja/platforms/ios-swift-v1/install/#carthage)をご覧ください。

## データレイヤー
モジュールが有効な間、以下の変数が各トラッキングコールで送信されます：

| 変数         | 説明                              | 例                         |
|----------------------|--------------------------------------|---------------------------------|
| `app_build`           | アプリのマイナービルドバージョン| `&#34;2213&#34;`                                 |
| `app_name`            | アプリの名前（通常はApp Storeの名前と同じ）| `&#34;Digital Velocity&#34;`   |
| `app_rdns`            | アプリバンドルの完全修飾名| `&#34;com.tealium.digitalvelocity&#34;`          |
| `app_uuid`            | ランダムなuuid。永続保存モジュールのいずれかが有効である限り、アプリのインストール期間中に持続します。アプリがアンインストールされるとリセットされます。  | `123e4567-e89b-12d3-a456-&#34;426655440000&#34;` |
| `app_version`         | アプリバンドルのバージョン                                                                                                                                   | `&#34;1.0&#34;`                                  |
| `tealium_visitor_id`         | 永続的なTealium訪問ID                                                                                                                               | `&#34;123e4567e89b12d3a456426655440000&#34;`     |
