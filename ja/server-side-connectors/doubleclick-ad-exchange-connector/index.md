---
title: DoubleClick Ad Exchange コネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでDoubleClick for Ad Exchangeコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/doubleclick-ad-exchange-connector/
---

## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ユーザーリストまたはセグメントに訪問を追加| ✓| ✓|
|ユーザーリストまたはセグメントから訪問を削除| ✓| ✓|

## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Google Audience Partner API DmpUserListService
* APIバージョン：v201809
* APIエンドポイント：`<https://ddp.googleapis.com/>`
* ドキュメンテーション：[Authorized Buyer (formerly DoubleClick Ad Exchange) API](https://developers.google.com/authorized-buyers/)

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[About Connectors](https://docs.tealium.com/about-connectors/)の記事を参照してください。


<blockquote>
このコネクタを追加すると、ベンダーのデータプラットフォームポリシーを受け入れるように求められます。
</blockquote>


コネクタを追加した後、以下の構成を構成します：

* **クライアントの顧客ID（必須）**
  * 選択した製品でのあなた（DoubleClickの顧客）の識別子。

* **ターゲット製品の選択（必須）**
  * ターゲット製品、**DoubleClick AdExhchange - Buyer**または**DoubleClick AdExchange - Publisher**のいずれか。

## 新しいセグメントの作成

AudienceStreamで新しいセグメントを作成するには、以下の手順を使用します：

1. アクション選択のドロップダウン画面の上部から**新しいセグメントを作成**をクリックします。
2. **セグメント名**、**セグメントメンバーの寿命**、**統合コード**、および**セグメントの説明**を入力します。  
<blockquote>
[DataAccess](https://docs.tealium.com/about-dataaccess/)製品（EventStore、AudienceStore、EventDB、またはAudienceDB）を使用する場合、セグメント名は128文字未満でなければなりません。それ以外の場合、DataAccessはセグメント名をトリムし、エラーが発生する可能性があります。
</blockquote>

![](https://docs.tealium.com/images/server-side-connectors/audiencestream-create-segment.jpg)
3. **セグメントを作成**をクリックします。  
統合コードは、ユーザーリストの販売者が自分のシステム上のIDを相関させるために使用するIDです。IDが利用できない場合は、1から1,000までのランダムな数値を手動で入力できます。セグメントが作成されたことを確認するために、セグメント作成ボタンの隣にチェックマークが表示されます。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ユーザーリストまたはセグメントに訪問を追加

#### パラメータ

|**パラメータ**|  * **説明** |
|---| ---|
|ターゲットユーザーリスト/セグメントの選択|  <ul><li>必須</li><li>ユーザーマップ識別子。</li><li>この操作が適用されるユーザーを指定します。</li><li>これは、ユーザーが追加されるターゲットのユーザーリスト/セグメントです。</li></ul> |
|GoogleユーザーID|  <ul><li>GoogleユーザーID</li><li>ADXクッキーマッチングサービスによって提供されます。</li></ul> |
|iOS広告ID|  <ul><li>iOS広告ID</li></ul> |
|Android広告ID|  <ul><li>Android広告ID</li></ul> |
|RIDA|  <ul><li>Roku ID</li></ul> |
|AFAI|  <ul><li>Amazon Fire TV ID</li></ul> |
|MSAI|  <ul><li>Xbox/Microsoft ID</li></ul> |
|データソースID|  <ul><li>オプション</li><li>このメンバーシップに貢献したデータソースを示すID。</li><li>1から1,000の範囲内であることが必要。</li><li>1,000を超えるIDはBAD_DATA_SOURCE_IDエラーを引き起こします。</li><li>これらのIDはGoogleにとって参照や意味を持たず、レポートのラベルとしてのみ使用されます。</li></ul> |

### アクション - ユーザーリストまたはセグメントから訪問を削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ターゲットユーザーリスト/セグメントの選択|  <ul><li>必須、これはユーザーが削除されるターゲットのユーザーリスト/セグメントです。</li></ul> |
|GoogleユーザーID|  <ul><li>GoogleユーザーID</li><li>ADXクッキーマッチングサービスによって提供されます。</li></ul> |
|iOS広告ID|  <ul><li>iOS広告ID</li></ul> |
|Android広告ID|  <ul><li>Android広告ID</li></ul> |
|RIDA|  <ul><li>Roku ID</li></ul> |
|AFAI|  <ul><li>Amazon Fire TV ID</li></ul> |
|MSAI|  <ul><li>Xbox/Microsoft ID</li></ul> |
|データソースID|  <ul><li>オプション</li><li>このメンバーシップに貢献したデータソースを示すID。</li><li>1から1,000の範囲内であることが必要。</li><li>1,000を超えるIDはBAD_DATA_SOURCE_IDエラーを引き起こします。</li><li>これらのIDはGoogleにとって参照や意味を持たず、レポートのラベルとしてのみ使用されます。</li></ul> |

