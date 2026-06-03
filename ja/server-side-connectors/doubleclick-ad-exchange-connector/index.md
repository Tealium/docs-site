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
* APIエンドポイント：`&lt;https://ddp.googleapis.com/&gt;`
* ドキュメンテーション：[Authorized Buyer (formerly DoubleClick Ad Exchange) API](https://developers.google.com/authorized-buyers/)

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[About Connectors]()の記事を参照してください。

このコネクタを追加すると、ベンダーのデータプラットフォームポリシーを受け入れるように求められます。

コネクタを追加した後、以下の構成を構成します：

* **クライアントの顧客ID（必須）**
  * 選択した製品でのあなた（DoubleClickの顧客）の識別子。

* **ターゲット製品の選択（必須）**
  * ターゲット製品、**DoubleClick AdExhchange - Buyer**または**DoubleClick AdExchange - Publisher**のいずれか。

## 新しいセグメントの作成

AudienceStreamで新しいセグメントを作成するには、以下の手順を使用します：

1. アクション選択のドロップダウン画面の上部から**新しいセグメントを作成**をクリックします。
2. **セグメント名**、**セグメントメンバーの寿命**、**統合コード**、および**セグメントの説明**を入力します。  [DataAccess]()製品（EventStore、AudienceStore、EventDB、またはAudienceDB）を使用する場合、セグメント名は128文字未満でなければなりません。それ以外の場合、DataAccessはセグメント名をトリムし、エラーが発生する可能性があります。
![](/images/server-side-connectors/audiencestream-create-segment.jpg)
3. **セグメントを作成**をクリックします。  
統合コードは、ユーザーリストの販売者が自分のシステム上のIDを相関させるために使用するIDです。IDが利用できない場合は、1から1,000までのランダムな数値を手動で入力できます。セグメントが作成されたことを確認するために、セグメント作成ボタンの隣にチェックマークが表示されます。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ユーザーリストまたはセグメントに訪問を追加

#### パラメータ

|**パラメータ**|  * **説明** |
|---| ---|
|ターゲットユーザーリスト/セグメントの選択|  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;ユーザーマップ識別子。&lt;/li&gt;&lt;li&gt;この操作が適用されるユーザーを指定します。&lt;/li&gt;&lt;li&gt;これは、ユーザーが追加されるターゲットのユーザーリスト/セグメントです。&lt;/li&gt;&lt;/ul&gt; |
|GoogleユーザーID|  &lt;ul&gt;&lt;li&gt;GoogleユーザーID&lt;/li&gt;&lt;li&gt;ADXクッキーマッチングサービスによって提供されます。&lt;/li&gt;&lt;/ul&gt; |
|iOS広告ID|  &lt;ul&gt;&lt;li&gt;iOS広告ID&lt;/li&gt;&lt;/ul&gt; |
|Android広告ID|  &lt;ul&gt;&lt;li&gt;Android広告ID&lt;/li&gt;&lt;/ul&gt; |
|RIDA|  &lt;ul&gt;&lt;li&gt;Roku ID&lt;/li&gt;&lt;/ul&gt; |
|AFAI|  &lt;ul&gt;&lt;li&gt;Amazon Fire TV ID&lt;/li&gt;&lt;/ul&gt; |
|MSAI|  &lt;ul&gt;&lt;li&gt;Xbox/Microsoft ID&lt;/li&gt;&lt;/ul&gt; |
|データソースID|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;このメンバーシップに貢献したデータソースを示すID。&lt;/li&gt;&lt;li&gt;1から1,000の範囲内であることが必要。&lt;/li&gt;&lt;li&gt;1,000を超えるIDはBAD_DATA_SOURCE_IDエラーを引き起こします。&lt;/li&gt;&lt;li&gt;これらのIDはGoogleにとって参照や意味を持たず、レポートのラベルとしてのみ使用されます。&lt;/li&gt;&lt;/ul&gt; |

### アクション - ユーザーリストまたはセグメントから訪問を削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ターゲットユーザーリスト/セグメントの選択|  &lt;ul&gt;&lt;li&gt;必須、これはユーザーが削除されるターゲットのユーザーリスト/セグメントです。&lt;/li&gt;&lt;/ul&gt; |
|GoogleユーザーID|  &lt;ul&gt;&lt;li&gt;GoogleユーザーID&lt;/li&gt;&lt;li&gt;ADXクッキーマッチングサービスによって提供されます。&lt;/li&gt;&lt;/ul&gt; |
|iOS広告ID|  &lt;ul&gt;&lt;li&gt;iOS広告ID&lt;/li&gt;&lt;/ul&gt; |
|Android広告ID|  &lt;ul&gt;&lt;li&gt;Android広告ID&lt;/li&gt;&lt;/ul&gt; |
|RIDA|  &lt;ul&gt;&lt;li&gt;Roku ID&lt;/li&gt;&lt;/ul&gt; |
|AFAI|  &lt;ul&gt;&lt;li&gt;Amazon Fire TV ID&lt;/li&gt;&lt;/ul&gt; |
|MSAI|  &lt;ul&gt;&lt;li&gt;Xbox/Microsoft ID&lt;/li&gt;&lt;/ul&gt; |
|データソースID|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;このメンバーシップに貢献したデータソースを示すID。&lt;/li&gt;&lt;li&gt;1から1,000の範囲内であることが必要。&lt;/li&gt;&lt;li&gt;1,000を超えるIDはBAD_DATA_SOURCE_IDエラーを引き起こします。&lt;/li&gt;&lt;li&gt;これらのIDはGoogleにとって参照や意味を持たず、レポートのラベルとしてのみ使用されます。&lt;/li&gt;&lt;/ul&gt; |

