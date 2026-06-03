---
title: EventStoreの構成
description: この記事では、EventStoreのイベントフィードを有効にする方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencestore-eventstore/configure-eventstore/
---
EventStoreをアカウントとプロフィールで有効にするには、アカウントマネージャーに連絡してください。

## EventStoreのイベントフィードを有効にする
1. **EventStream &gt; Live Events**に移動します。
1. イベントフィードを選択し、**編集**をクリックします。  
1. **Event Data Storage**を`EventStore`に構成します。
1. 保存して公開します。

プロフィールでEventStoreが無効になっている場合、すべてのイベントフィードでEventStoreが無効になります。EventStoreを再度有効にすると、イベントフィードは手動で再度有効にする必要があります。

イベントフィードを有効にした後、**DataAccess &gt; EventStore**に移動してJSONファイルを表示およびダウンロードします。各JSONファイルには、EventStreamからのイベントのリストが含まれています。また、サードパーティのツールを使用してファイルを表示することもできます。詳細については、[ファイルの表示]()を参照してください。
