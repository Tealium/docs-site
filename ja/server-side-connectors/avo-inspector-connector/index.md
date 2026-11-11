---
title: Avo Inspectorコネクタ構成ガイド
description: この記事では、Avo Inspectorコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/avo-inspector-connector/
---
## API情報

このコネクタは、次のベンダーAPIを使用します。

* API名：Avo Inspector
* APIバージョン：v1.0.2
* APIエンドポイント：`https://api.avo.app/inspector/tealium/v1/track`
* ドキュメント：[Avo Inspector API](https://avohq.notion.site/Avo-Tealium-Inspector-API-destination-1-ce5d8dda46fd49bd8cfbaf45a4df3619)

## バッチ制限

このコネクタは、ベンダーへの大量のデータ転送に対応するため、バッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに保持されます。

* リクエストの最大数：30
* 最も古いリクエストからの最大経過時間：5分
* リクエストの最大サイズ：1 MB

## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| イベントデータを送信（リアルタイム） | ✗ | ✓ |
| イベントデータを送信（バッチ） | ✗ | ✓ |

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の構成を構成します。

* **APIキー**  
 （必須）このAPIキーは、AvoでInspectorソースを有効化するときに作成されます。InspectorソースごとにTealium内に個別のAvo送信先が必要です。これにより、Avoはイベントの送信元を特定できます。
* **環境**  
 （必須）現在の環境：**Prod**、**Dev**、または**Staging**。
* **送信元（文字列）**  
 （任意）呼び出しの送信元。

## アクション

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

以下のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### イベントデータを送信（リアルタイム）

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| イベントタイプ | イベントのタイプ。`event`または`sessionStarted`のいずれかです。 |
| テンプレート変数 | **テンプレート**へのデータ入力としてテンプレート変数を指定します。詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<br>ネストされたテンプレート変数には、ドット表記で名前を付けます。例：`items.name.`<br>通常、ネストされたテンプレート変数は、データレイヤーのリスト属性から作成されます。 |
| テンプレート | イベントパラメータで参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。<br>テンプレートは、サポートされているフィールドに二重波括弧で囲んだ名前を使用して挿入されます。例：`{{SomeTemplateName}}`。|

### イベントデータを送信（バッチ）

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| イベントタイプ | イベントのタイプ。`event`または`sessionStarted`のいずれかです。 |
| テンプレート変数 | **テンプレート**へのデータ入力としてテンプレート変数を指定します。詳細および使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<br>ネストされたテンプレート変数には、ドット表記で名前を付けます。例：`items.name.`<br>通常、ネストされたテンプレート変数は、データレイヤーのリスト属性から作成されます。 |
| テンプレート | イベントパラメータで参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。<br>テンプレートは、サポートされているフィールドに二重波括弧で囲んだ名前を使用して挿入されます。例：`{{SomeTemplateName}}`。|