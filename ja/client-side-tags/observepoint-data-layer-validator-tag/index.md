---
title: ObservePointデータレイヤーバリデータタグ構成ガイド
description: この記事では、iQタグ管理（TiQ）アカウントでObservePointデータレイヤーバリデータタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/observepoint-data-layer-validator-tag/
---
## 仕組み

ObservePoint Mobile Data Layerを使用して、ObservePoint内のデータレイヤーを検証します。これにより、ObservePointのモバイルアプリテストが、データレイヤーのレビューにおけるウェブテストの機能と一致するようにエンリッチメントされます。

## タグのヒント

* このタグは本番環境で実行すべきではありません
* ObservePointオブジェクト名はデフォルトで`utagdata`という値になります。
* データレイヤーオブジェクトはデフォルトで`b`という値になります。

## タグの構成

まず、Tealiumのタグマーケットプレイスに行き、ObservePoint Data Layer Validatorタグを追加します（[タグの追加方法]()について詳しくはこちら）。

タグを追加した後、以下の構成を行います：

* **ObservePointオブジェクト名**  
これはObservePointユーザーインターフェースに表示される名前です。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

|変数| 説明|
|---| ---|
| `op_object_name` | ObservePointオブジェクト名|
| `op_object` | データレイヤーオブジェクト|
