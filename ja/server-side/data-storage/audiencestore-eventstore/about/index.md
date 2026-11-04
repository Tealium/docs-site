---
title: AudienceStore と EventStore について
description: この記事では、AudienceStore および EventStore サービスにアクセスする方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencestore-eventstore/about/
---

<blockquote>
AudienceStore および EventStore サービスをアカウントで有効にするには、[サポートにお問い合わせください](https://docs.tealium.com/support/)。
</blockquote>


## 前提条件

* Tealium DataAccess が有効になっている必要があります。
* 訪問プロファイルデータを Tealium S3 バケットに送信するには、有効な AudienceStore コネクタが必要です。詳細については、[AudienceStore コネクタ構成ガイド](https://docs.tealium.com/audiencestore-connector/)を参照してください。  
* イベントデータを Tealium S3 バケットに送信するには、少なくとも 1 つの有効なイベントフィードが必要です。
* オーディエンス名は 128 文字未満にする必要があります。これより長いオーディエンス名は切り詰められ、エラーが発生する可能性があります。

## 仕組み

AudienceStore と EventStore は、Tealium が提供する、顧客がアクセス可能な Amazon S3 バケットに半構造化された訪問データとイベントデータを保存するサービスです。データは、次の表に示す形式で保存されます。

| **サービス** | **保存形式** |
|---|---|
| EventStore | JSON |
| AudienceStore | JSON または CSV |

どちらのサービスも、ファイルが 100 MB（圧縮前）に達するか、1 時間が経過するたびに、いずれか早い方のタイミングで新しいファイルを S3 に書き込みます。ほとんどの場合、ファイルはこれよりも大幅に高い頻度で書き込まれます。

### データ保持

EventStore と AudienceStore は、データを 30 日間保持します。イベント、訪問、または訪問レコードが有効期限に達すると、そのレコードは自動的に削除されます。訪問レコードが更新された場合でも有効期限は変わらず、レコードは引き続き削除されます。

詳細については、[サーバーサイドのアカウント構成]()を参照してください。

### EventStore の有効化

イベントデータを EventStore に保存するには、1 つ以上のイベントフィードに対して EventStore を有効にします。詳細については、[EventStore の構成]()を参照してください。

イベントフィードに対して EventStore を有効にすると、EventDB は EventStore をデータソースとして使用し、EventStore の S3 バケットから Tealium が提供する Amazon Redshift データベースにデータをインポートします。

### AudienceStore の有効化

オーディエンスデータを AudienceStore に保存するには、そのオーディエンスに AudienceStore コネクタを追加します。詳細については、[AudienceStore の構成]()を参照してください。

AudienceStore は AudienceDB を有効にするための前提条件ではありません。これらのサービスはそれぞれ独立して動作します。詳細については、[AudienceDB と EventDB について]()を参照してください。

### AudienceStore のファイルパス

AudienceStore のデータファイルは、アカウント名、プロファイル名、および AudienceStore コネクタのアクション ID に対応する次のパス構造で S3 バケットに保存されます。

```
{ACCOUNT}/{PROFILE}/audiences/{ACTION_ID}
```

アクション ID は、次に示すように、AudienceStore コネクタアクションの **詳細** で確認できます。

![](https://docs.tealium.com/images/server-side/actionid-asactiondetails.png)

AudienceStore ファイルへのパスの例：

```
my-account/main/audiences/bafc28ca-9542-3929-3b94-577a84f3d672
```

### EventStore のファイルパス

EventStore のデータファイルは、次のパスで S3 バケットに保存されます。

```
{ACCOUNT}/{PROFILE}/events/{EVENT_FEED_ID}
```

イベントフィード ID は、イベントフィードの URL で確認できます。**ライブイベント**に移動し、フィードをクリックして選択します。次に示すように、URL を調べてフィード ID を取得します。

![](https://docs.tealium.com/images/server-side/eventstore-id-in-url-highlighted.png)

EventStore ファイルへのパスの例：

```
my-account/main/events/bafc28ca-9542-3929-3b94-577a84f3d672
```