---
title: AppDataモジュール
description: データレイヤーにアプリバンドルに関する情報を追加します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/appdata/
---
## 使用法
AppDataモジュールは、アプリバンドルに関する重要な情報を収集します。このモジュールの使用は推奨されますが、必須ではありません。除外することを選択した場合、データレイヤー変数はトラッキング呼び出しに含まれません。`tealium_visitor_id`は、必須の変数であるため、モジュールが無効でも常に送信されます。

以下のプラットフォームがサポートされています：

* iOS
* macOS
* watchOS
* tvOS

## インストール

このモジュールはCoreライブラリの一部として含まれており、別途インストールは必要ありません。

## 初期化

モジュールを初期化するには、`TealiumConfig`の[`collectors`](https://docs.tealium.com/ja/platforms/ios-swift/api/tealium-config/#collectors)プロパティで指定されていることを確認します：

```swift
config.collectors = [Collectors.AppData]
```


<blockquote>
[Collectors](https://docs.tealium.com/ja/platforms/ios-swift/modules/#collectors)のドキュメンテーションを確認し、必要なコレクターを正しく指定する方法を理解してください。
</blockquote>


## データレイヤー
モジュールが有効な間、以下の変数が各トラッキング呼び出しで送信されます：

| 変数                 | 説明                                                                                                                                                | 例                                       |
|:---------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------|
| `app_build`          | アプリのマイナービルドバージョン                                                                                                                             | `"2213"`                                 |
| `app_name`           | アプリの名前（通常はApp Storeの名前と同じ）                                                                                                           | `"Digital Velocity"`                     |
| `app_rdns`           | アプリバンドルの完全修飾名                                                                                                                     | `"com.tealium.digitalvelocity"`          |
| `app_uuid`           | ランダムなuuid。アプリのインストール期間中に持続し、永続的な保存モジュールのいずれかが有効になっている限り。アプリがアンインストールされるとリセットされます。 | `123e4567-e89b-12d3-a456-"426655440000"` |
| `app_version`        | アプリバンドルのバージョン                                                                                                                                  | `"1.0"`                                  |
| `tealium_visitor_id` | 永続的なTealium訪問ID                                                                                                                              | `"123e4567e89b12d3a456426655440000"`     |
