---
title: Avo Inspectorコネクタ構成ガイド
description: この記事では、Avo Inspectorコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/avo-inspector-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Avo Inspector
* APIバージョン：v1.0.2
* APIエンドポイント：`https://api.avo.app/inspector/tealium/v1/track`
* ドキュメント：[Avo Inspector API](https://avohq.notion.site/Avo-Tealium-Inspector-API-destination-1-ce5d8dda46fd49bd8cfbaf45a4df3619)

## バッチ制限

このコネクタは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：30
* 最古のリクエストからの最大時間：5分
* リクエストの最大サイズ：1 MB

## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| イベントデータ送信（リアルタイム） | ✗ | ✓ |
| イベントデータ送信（バッチ） | ✗ | ✓ |

## 構成の構成

コネクタマーケットプレイスに移動して、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIキー**  
 必須。このAPIキーは、Avoでインスペクタソースをアクティブ化するときに作成されます。各インスペクタソースには、イベントのソースをAvoが特定できるように、Tealium内に別のAvoデスティネーションが必要です。
* **環境**  
 必須。現在の環境：**Prod**、**Dev**、または**Staging**。
* **発信元（文字列）**  
 オプション。呼び出しの発信元。

## アクション

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### イベントデータ送信（リアルタイム）

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| イベントタイプ | イベントのタイプ。`event`または`sessionStarted`のいずれか。 |
| テンプレート変数 | **テンプレート**のデータ入力としてテンプレート変数を提供します。詳細と使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<br>ドット表記でネストされたテンプレート変数を名前付けします。例：`items.name.`<br>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。 |
| テンプレート | イベントパラメータで参照されるテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。<br>テンプレートは、サポートされるフィールドに名前で二重中括弧で注入されます。例：`{{SomeTemplateName}}`。|

### イベントデータ送信（バッチ）

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| イベントタイプ | イベントのタイプ。`event`または`sessionStarted`のいずれか。 |
| テンプレート変数 | **テンプレート**のデータ入力としてテンプレート変数を提供します。詳細と使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<br>ドット表記でネストされたテンプレート変数を名前付けします。例：`items.name.`<br>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。 |
| テンプレート | イベントパラメータで参照されるテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。<br>テンプレートは、サポートされるフィールドに名前で二重中括弧で注入されます。例：`{{SomeTemplateName}}`。|
