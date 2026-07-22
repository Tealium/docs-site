---
title: AudienceStoreとEventStoreについて
description: この記事では、AudienceStoreとEventStoreサービスにアクセスする方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencestore-eventstore/about/
---

<blockquote>
AudienceStoreおよびEventStoreサービスをアカウントで有効にするには、[サポートにお問い合わせください](https://docs.tealium.com/support/)。
</blockquote>


## 前提条件

* Tealium DataAccessが有効である必要があります。
* TealiumのS3バケットに訪問プロファイルデータを送信するには、有効なAudienceStoreコネクタが必要です。詳細については、[AudienceStoreコネクタ構成ガイド](https://docs.tealium.com/audiencestore-connector/)を参照してください。
* TealiumのS3バケットにイベントデータを送信するには、少なくとも1つの有効なイベントフィードが必要です。
* オーディエンス名は128文字未満である必要があります。より長いオーディエンス名は切り捨てられ、エラーが発生する可能性があります。

## 動作原理

AudienceStoreとEventStoreは、Tealiumが提供する顧客アクセス可能なAmazon S3バケットに半構造化された訪問およびイベントデータを保存するサービスです。データは以下の表に示すように保存されます：

| **サービス** | **保存形式** |
|---|---|
| EventStore | JSON |
| AudienceStore | JSONまたはCSV |

どちらのサービスも、ファイルが100MB（圧縮前）に達するか、1時間が経過するか、どちらか早い方が発生した時点でS3に新しいファイルを書き込みます。ほとんどの場合、それよりもはるかに頻繁にファイルが書き込まれます。

### データ保持

EventStoreおよびAudienceStoreに保存された半構造化データは、契約で指定された期間、Amazon S3に保持されます。イベント、訪問、または訪問レコードがその有効期限に達すると、そのレコードは自動的に削除されます。訪問レコードが更新された場合でも、有効期限は変わらず、レコードは削除されます。

詳細については、[サーバーサイドアカウント構成]()を参照してください。

### EventStoreの有効化

イベントデータをEventStoreに保存するには、1つ以上のイベントフィードでEventStoreを有効にします。詳細については、[EventStoreの構成]()を参照してください。

イベントフィードでEventStoreが有効になると、EventDBはEventStoreをデータソースとして使用し、Tealiumが提供するAmazon RedshiftデータベースにEventStore S3バケットからデータをインポートします。

### AudienceStoreの有効化

オーディエンスデータをAudienceStoreに保存するには、オーディエンスのAudienceStoreコネクタを追加します。詳細については、[AudienceStoreの構成]()を参照してください。

AudienceStoreはAudienceDBを有効にするための前提条件ではありません。これらのサービスは独立して運用されます。詳細については、[AudienceDBとEventDBについて]()を参照してください。

### AudienceStoreファイルパス

AudienceStoreのデータファイルは、アカウント名、プロファイル名、およびAudienceStoreコネクタのアクションIDに一致するパス構造でS3バケットに保存されます：

```
{ACCOUNT}/{PROFILE}/audiences/{ACTION_ID}
```

アクションIDは、AudienceStoreコネクタアクションの**詳細**で見ることができます：

![](https://docs.tealium.com/images/server-side/actionid-asactiondetails.png)

AudienceStoreファイルへの例示パス：

```
my-account/main/audiences/bafc28ca-9542-3929-3b94-577a84f3d672
```

### EventStoreファイルパス

EventStoreのデータファイルは、次のようにS3バケットに保存されます：

```
{ACCOUNT}/{PROFILE}/events/{EVENT_FEED_ID}
```

イベントフィードIDは、イベントフィードのURLで見ることができます。**ライブイベント**にアクセスし、フィードをクリックして選択します。URLを調べてフィードIDを取得します。以下に示すように：

![](https://docs.tealium.com/images/server-side/eventstore-id-in-url-highlighted.png)

EventStoreファイルへの例示パス：

```
my-account/main/events/bafc28ca-9542-3929-3b94-577a84f3d672
```