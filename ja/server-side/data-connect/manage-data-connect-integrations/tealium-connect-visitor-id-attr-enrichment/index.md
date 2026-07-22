---
title: Tealium Connectの訪問ID属性のエンリッチメント
description: この記事では、AudienceStreamでData Connectを使用するための訪問ID属性をマッピングおよびエンリッチメントする方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/manage-data-connect-integrations/tealium-connect-visitor-id-attr-enrichment/
---
Tealium Connectで訪問ID属性をエンリッチメントするには、以下の手順を完了します：

1. Data Connectで使用するために作成したTealiumイベント仕様で、Tealium Connectデータソースに送信されるイベントを探します。
  1. Workatoレシピの訪問ID属性と一緒に使用するイベント属性の名前をメモします。例えば、`customer_id`。
  1. すでに存在しない場合は、イベント属性名でUniversal Data Objectタイプの文字列イベント属性を作成します。
1. ビルトインのイベント属性`tealium_datasource={{tealium_data_source_key}}`に基づいてTealium Connectデータソースからのイベントを識別するルールを作成します。このルールがまだ存在しない場合は、あなたのデータソースキーは[Tealium Connectデータソース](https://docs.tealium.com/tealium-connect-data-source/)で見つけることができます。
1. **Transform > Visitor / Visit Attributes**に移動します。
1. Tealium Connectデータと一緒に使用したい訪問IDを選択します。訪問IDがまだ存在しない場合は、以下の手順を完了します：
  1. **+ 属性を追加**をクリックします。
  1. 属性スコープで**訪問**を選択し、**続行**をクリックします。
  1. **データタイプを選択**画面で**訪問ID**を選択し、**続行**をクリックします。
  1. 属性画面で訪問ID属性の名前を入力します。
1. 訪問IDを選択し、**エンリッチメントを追加**をクリックします。
1. **訪問IDを構成**のドロップダウンで、上記で選択したイベント属性を選択します。
1. **いつ**の条件では、データソースがTealium Connectデータソースであるときにこのエンリッチメントが発生することを確認します。Tealium Connectデータソースルールを選択します。
1. **完了**をクリックします。


<blockquote>
Tealium Connectからの訪問がAudienceStreamに継続して存在することを確認するために、Data Connectイベントが発生するたびに、同じルールを使用してバッジを割り当てます。そのようなバッジがまだ存在しない場合は。
</blockquote>

