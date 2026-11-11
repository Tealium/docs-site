---
title: ObservePoint Data Layer Validatorタグ構成ガイド
description: この記事では、タグ管理アカウントでObservePoint Data Layer Validatorタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/observepoint-data-layer-validator-tag/
---
## 仕組み

ObservePoint Mobile Data Layerを使用して、ObservePoint内でデータレイヤーを検証します。これにより、ObservePointモバイルアプリのテスト機能がエンリッチメントされ、データレイヤーの確認においてWebテストと同等の機能を利用できるようになります。

## タグに関するヒント

* このタグは本番環境で実行しないでください。
* ObservePointオブジェクト名のデフォルト値は`utagdata`です。
* Data Layerオブジェクトのデフォルト値は`b`です。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **ObservePointオブジェクト名**  
ObservePointのユーザーインターフェイスに表示される名前です。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
| `op_object_name` | ObservePointオブジェクト名|
| `op_object` | Data Layerオブジェクト|