---
title: Tealium Connect向け訪問ID属性のエンリッチメント
description: この記事では、Data Connectで使用するために、顧客データプラットフォーム（CDP）で訪問ID属性をマッピングおよびエンリッチする方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/manage-data-connect-integrations/tealium-connect-visitor-id-attr-enrichment/
---
Tealium Connectで使用する訪問ID属性をエンリッチするには、次の手順を実行します。

1. Data Connectで使用するために作成したTealiumイベント仕様で、Tealium Connectデータソースに送信されたイベントを探します。
  1. Workatoレシピで訪問ID属性とともに使用するイベント属性の名前（例：`customer_id`）を確認します。
  1. そのイベント属性がまだ存在しない場合は、該当するイベント属性名を使用して、Universal Data Object型の文字列イベント属性を作成します。
1. まだルールが存在しない場合は、組み込みイベント属性`tealium_datasource={{tealium_data_source_key}}`に基づいてTealium Connectデータソースからのイベントを識別するルールを作成します。データソースキーは、[Tealium Connectデータソース](https://docs.tealium.com/tealium-connect-data-source/)で確認できます。
1. **変換（Transform）> 訪問／訪問属性（Visitor/Visit Attributes）**に移動します。
1. Tealium Connectデータで使用する訪問IDを選択します。訪問IDがまだ存在しない場合は、次の手順を実行します。
  1. **+ 属性を追加（+ Add Attribute）**をクリックします。
  1. 属性のスコープとして**訪問（Visitor）**を選択し、**続行（Continue）**をクリックします。
  1. **データ型を選択（Choose a Data Type）**画面で、**訪問ID（Visitor ID）**を選択し、**続行（Continue）**をクリックします。
  1. 属性画面で、訪問ID属性の名前を入力します。
1. 訪問IDを選択し、**エンリッチメントを追加（Add Enrichment）**をクリックします。
1. **訪問IDの構成先（Set Visitor ID to）**ドロップダウンで、前の手順で選択したイベント属性を選択します。
1. **条件（When）**では、Tealium Connectデータソースのルールを選択し、データソースがTealium Connectデータソースの場合にこのエンリッチメントが実行されるようにします。
1. **完了（Finish）**をクリックします。


<blockquote>
Tealium Connectからの訪問が顧客データプラットフォーム（CDP）に保持されるようにするには、そのようなバッジがまだ存在しない場合、同じルールを使用してData Connectイベントが発生するたびにバッジを割り当てます。
</blockquote>
