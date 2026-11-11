---
title: DoubleClick Ad Exchangeコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでDoubleClick for Ad Exchangeコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/doubleclick-ad-exchange-connector/
---
## コネクタアクション

| アクション名 | ビジタープロファイル | イベントデータ |
| --- | :---: | :---: |
|ユーザーリストまたはセグメントにビジターを追加| ✓| ✓|
|ユーザーリストまたはセグメントからビジターを削除| ✓| ✓|

## API情報

このコネクタでは、以下のベンダーAPIを使用します。

* API名：Google Audience Partner API DmpUserListService
* APIバージョン：v201809
* APIエンドポイント：`<https://ddp.googleapis.com/>`
* ドキュメント：[Authorized Buyer（旧DoubleClick Ad Exchange）API](https://developers.google.com/authorized-buyers/)

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。


<blockquote>
このコネクタを追加すると、ベンダーのデータプラットフォームポリシーへの同意を求められます。
</blockquote>


コネクタを追加した後、以下の構成を構成します。

* **クライアント顧客ID（必須）**
  * 選択した製品におけるお客様（DoubleClick顧客）の識別子。

* **対象製品を選択（必須）**
  * 対象製品として、**DoubleClick AdExhchange - Buyer**または**DoubleClick AdExchange - Publisher**を選択します。

## 新しいセグメントの作成

Customer Data Platform（CDP）で新しいセグメントを作成するには、以下の手順を実行します。

1. ［Actions］選択ドロップダウン画面の上部にある**［Create a New Segment］**をクリックします。
2. **［Segment Name］**、**［Segment Member Lifespan］**、**［Integration Code］**、**［Segment Description］**を入力します。
<blockquote>
[DataAccess](https://docs.tealium.com/about-dataaccess/)製品（EventStore、AudienceStore、EventDB、またはAudienceDB）を使用する場合、セグメント名は128文字未満にする必要があります。そうしないと、DataAccessによってセグメント名が切り詰められ、エラーが発生する可能性があります。
</blockquote>

![](https://docs.tealium.com/images/server-side-connectors/audiencestream-create-segment.jpg)
3. **［Create Segment］**をクリックします。  
Integration Codeは、ユーザーリストの販売者が自社システム上のIDを関連付けるために使用するIDです。使用できるIDがない場合は、1～1,000の範囲でランダムな数値を手動で入力できます。セグメントが作成されたことを確認するため、［Create Segment］ボタンの横にチェックマークが表示されます。

## アクション構成 - パラメータとオプション

**［Continue］**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - ユーザーリストまたはセグメントにビジターを追加

#### パラメータ

|**パラメータ**| **説明** |
|---| ---|
|対象のユーザーリスト／セグメントを選択| <ul><li>（必須）ユーザーマップ識別子。</li><li>この操作の対象となるユーザーを指定します。</li><li>ユーザーの追加先となる対象のユーザーリスト／セグメントです。</li></ul> |
|GoogleユーザーID| <ul><li>GoogleユーザーID</li><li>ADX Cookie Matchingサービスによって提供されます。</li></ul> |
|iOS広告ID| <ul><li>iOS広告ID</li></ul> |
|Android広告ID| <ul><li>Android広告ID</li></ul> |
|RIDA| <ul><li>Roku ID</li></ul> |
|AFAI| <ul><li>Amazon Fire TV ID</li></ul> |
|MSAI| <ul><li>Xbox/Microsoft ID</li></ul> |
|データソースID| <ul><li>（任意）このメンバーシップに寄与したデータソースを示すID。</li><li>1～1,000の範囲内である必要があります。</li><li>1,000を超えるIDを指定すると、BAD_DATA_SOURCE_IDエラーが発生します。</li><li>これらのIDはGoogleにとって参照情報や意味を持つものではなく、レポート目的のラベルとしてのみ使用されます。</li></ul> |

### アクション - ユーザーリストまたはセグメントからビジターを削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|対象のユーザーリスト／セグメントを選択| <ul><li>必須。ユーザーの削除元となる対象のユーザーリスト／セグメントです。</li></ul> |
|GoogleユーザーID| <ul><li>GoogleユーザーID</li><li>ADX Cookie Matchingサービスによって提供されます。</li></ul> |
|iOS広告ID| <ul><li>iOS広告ID</li></ul> |
|Android広告ID| <ul><li>Android広告ID</li></ul> |
|RIDA| <ul><li>Roku ID</li></ul> |
|AFAI| <ul><li>Amazon Fire TV ID</li></ul> |
|MSAI| <ul><li>Xbox/Microsoft ID</li></ul> |
|データソースID| <ul><li>（任意）このメンバーシップに寄与したデータソースを示すID。</li><li>1～1,000の範囲内である必要があります。</li><li>1,000を超えるIDを指定すると、BAD_DATA_SOURCE_IDエラーが発生します。</li><li>これらのIDはGoogleにとって参照情報や意味を持つものではなく、レポート目的のラベルとしてのみ使用されます。</li></ul> |