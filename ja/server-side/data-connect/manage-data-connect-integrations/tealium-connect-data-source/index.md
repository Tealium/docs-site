---
title: Tealium Connect データソースの構成
description: この記事では、Tealium Connect データソースの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/manage-data-connect-integrations/tealium-connect-data-source/
---
Tealium Collectにイベントを送信し、Data Connectイベントを識別するためには、各統合に対してTealium Connectデータソースを使用します。各Data Connect統合に専用のデータソースを持つことで、[Live Events]()で関連イベントを簡単に確認できます。また、Tealium EventStreamやAudienceStreamで、Data Connectイベントのみを処理するコネクタを構成することもできます。

Tealiumのデータソースについての詳細は、[About Data Sources]()を参照してください。

各オリジナルデータソースごとに1つのTealium Connectデータソースを構成することを推奨します。例えば、Salesforceデータ用のTealium Connectデータソースと、Snowflakeデータ用の別のデータソースなどです。

Tealium Connectデータソースを追加するには、以下の手順を完了します：

1. **Sources &gt; Data Sources**に移動します。
1. **&#43; Add Data Source**をクリックします。
1. **Select a Platform**画面から**Tealium Connect**を選択します。
1. **Summary**の下の**Name**フィールドに名前を入力し、**Continue**をクリックします。
1. **Choose Event Specifications**ステップで**Continue**をクリックします。
1. イベント仕様を選択し、**Continue**をクリックするか、このステップをスキップするために**Skip**をクリックします。
1. **Get Code**画面では、以下の形式でTealium ConnectエンドポイントURLが表示されます：  
```
https://collect-us-east-1.tealiumiq.com/dataconnect/event/{{account}}/{{profile}}/{{data source key}}
```
このキーは、WorkatoのTealium Eventsアプリを構成するために必要です。Tealium APIドメインは、[Tealium Private Cloud](https://tealium.com/resource/fundamentals/tealium-private-cloud/)を使用するクライアントに対してカスタムされます。
8. オプション。インストール手順をダウンロードするには、**Download as PDF**をクリックします。
9. **Save &amp; Continue**をクリックします。
10. データソースの概要が表示されます。
11. **Close**をクリックします。  
新しいデータソースは**Data Sources**ダッシュボードで確認できます。
12. データソースエンドポイントを有効化するには、プロファイルを**Save/Publish**します。

 Tealium Connectを構成した後でデータソースキーを見つけるには、**Data Sources**ダッシュボードに移動し、使用したいデータソースをクリックし、**Data Source Key**フィールドからキーをコピーします。

