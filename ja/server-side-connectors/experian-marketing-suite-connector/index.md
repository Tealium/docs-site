---
title: Experian Marketing Suiteコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでExperian Marketing Suiteを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/experian-marketing-suite-connector/
---Experian Marketing Suiteのクロスチャネルマーケティングプラットフォームを使用すると、ブランドはすべての顧客インタラクションを単一のシステム内でリアルタイムに管理および実行できるため、複数の異なるプラットフォームやチャネルごとのベンダーが不要になります。

## 要件

* Experian Marketing Servicesアカウント
* Consumer Key（API ACCESS画面に表示）
* Consumer Secret（API ACCESS画面に表示）

## サポートされているアクション

|**アクション名**| **オーディエンスでトリガー**| **ストリームでトリガー**|
|---| ---| ---|
|テーブルへのデータ挿入| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

ベンダーを構成するには、次の手順に従います。

1. **Configure**タブで、コネクタインスタンスのタイトルを指定します。
1. （任意）Experianから受け取ったClient IDを入力します。
1. ExperianのAPI ACCESS画面で取得したConsumer Keyを入力します。
1. ExperianのAPI ACCESS画面で取得したConsumer Secretを入力します。
1. 実装に関する追加のメモを入力します。
1. **Test Connection**をクリックして、キーを検証します。

## アクション構成 - パラメータとオプション

**Continue**をクリックして、コネクタのアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション：テーブルへのデータ挿入

#### パラメータ

| パラメータ | 説明 |
|---|---|
| Table | （必須）更新するテーブルを指定します。 |
| Table Entry Data | （必須）値をテーブル内の列にマッピングします。 |
| Upward Relations | このテーブルエントリを他のテーブルにリンクします。 |
| Date Formats | 特定の形式を使用して受信データをフォーマットします。 |
| Import Options | データ挿入に関する追加オプションを指定します。 |

#### オプション：Upward Relations

Upward Relationsを使用すると、テーブルデータ同士をリンクできます。たとえば、`order_item`と`order`という2つのテーブルがあるとします。

|**order_item**| **order**|
|---| ---|
|item_id| id|
|quantity| date|
|order|

**Order_item**の`item_id`と`quantity`は、Table Entry Dataセクションでマッピングします。**Order_item**の`order`と、**order**の`item_id`および`quantity`は、Upward Relationsセクションでマッピングする必要があります。マッピング結果は次のようになります。

|**属性**| **パス**|
|---| ---|
|event_order_id| `order/id`|
|event_timestamp| `order/date`|

ここで「eventorder_id」と「event_timestamp」は、単一エントリのイベント／オーディエンス配列属性であり、複数のUpward Relationsを指定できます。

#### オプション：Date Formats

テーブルフィールドごとに日付形式を指定します（Upward Relationのパスにも適用されます）。形式は[Javaのテンプレート標準](https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html)に従う必要があります。

一般的な形式には、次のものがあります。

|**形式**| **結果**|
|---| ---|
|MM/DD/YYYY| 05/25/1977|
|MM/dd/yyyy hh:mm a| 05/25/1977 07:15 PM|
|yyyy/MM/dd HH:mm:ss| 1977/05/25 19:15:37|
|yyyy/MM/dd HH:mm:ss x| 1977/05/25 19:15:37 +0000|

カスタム日付または受信した日付は、1970年1月1日UTC（エポック）からの経過ミリ秒として扱われます。

#### オプション：Import Options

|**オプション**| **値**| **説明**|
|---| ---| ---|
|Do Not Update Existing| `true`または`false`| 一致するレコードを更新する代わりに新しいレコードを挿入する場合は`true`|

上記に記載されていないインポートオプションについては、CustomValueを指定できます。