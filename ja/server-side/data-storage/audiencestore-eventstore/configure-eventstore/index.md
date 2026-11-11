---
title: EventStore の構成
description: この記事では、EventStore のイベントフィードを有効にする方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencestore-eventstore/configure-eventstore/
---

<blockquote>
アカウントとプロファイルで EventStore を有効にするには、アカウントマネージャーにお問い合わせください。
</blockquote>


## EventStore のイベントフィードを有効にする
1. **Validate > Live Events** に移動します。
1. イベントフィードを選択し、**Edit** をクリックします。  
1. **Event Data Storage** を `EventStore` に構成します。
1. 保存して公開します。


<blockquote>
プロファイルで EventStore が無効になっている場合、すべてのイベントフィードで EventStore が無効になります。EventStore を再度有効にした場合は、イベントフィードも手動で再度有効にする必要があります。
</blockquote>


イベントフィードを有効にした後、**Store > EventStore** に移動して JSON ファイルを表示およびダウンロードします。各 JSON ファイルには、Event Streaming のイベントのリストが含まれています。サードパーティ製ツールを使用してファイルを表示することもできます。詳細については、[ファイルの表示]()を参照してください。