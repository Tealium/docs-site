---
title: 接続性モジュール
description: デバイスのネットワーク接続に関する情報を収集し、各イベントのデータレイヤーに追加します。
url: https://docs.tealium.com/ja/platforms/ios-swift/module-list/connectivity/
---
## 使用法
このモジュールの使用が推奨されています。

以下のプラットフォームがサポートされています:

* iOS
* tvOS
* macOS
* watchOS

## インストール

このモジュールはCoreライブラリの一部として含まれており、別途インストールは必要ありません。

## 初期化

モジュールを初期化するには、`TealiumConfig` [`collectors`](/ja/platforms/ios-swift/api/tealium-config/#collectors) プロパティで指定されていることを確認します。

`config.collectors = [Collectors.Connectivity]`

必要なコレクターを正しく指定する方法については、[Collectors](/ja/platforms/ios-swift/modules/#collectors)のドキュメンテーションを参照してください。

## データレイヤー
モジュールが有効な間、以下の変数が各トラッキング呼び出しで送信されます:

| 変数   | 説明                                                                                                                      | 例  |
|------------|----------------------------------------------------------------------------------------------------------------------------------|---------------|
| `connection_type`   | 現在の接続タイプ                                                               | [`&#34;wifi&#34;`, `&#34;cellular&#34;`]             |
