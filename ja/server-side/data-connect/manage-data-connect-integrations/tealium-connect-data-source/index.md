---
title: Tealium Connectデータソースの構成
description: この記事では、Tealium Connectデータソースを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/manage-data-connect-integrations/tealium-connect-data-source/
---
Tealium Collectにイベントを送信し、Data Connectイベントを識別するには、統合ごとにTealium Connectデータソースを使用します。Data Connect統合ごとに専用のデータソースを用意すると、関連するイベントを[ライブイベント](https://docs.tealium.com/about-live-events/)で簡単に確認できます。また、Data Connectイベントのみを処理するコネクタを、Event StreamingまたはCustomer Data Platform（CDP）で構成することもできます。

Tealiumのデータソースの詳細については、[データソースについて](https://docs.tealium.com/about-data-sources/)を参照してください。


<blockquote>
送信元データソースごとに1つのTealium Connectデータソースを構成することをお勧めします。たとえば、Salesforceデータ用のTealium Connectデータソースと、Snowflakeデータ用の別のデータソースを構成します。
</blockquote>


Tealium Connectデータソースを追加するには、次の手順を実行します。

1. **Connect > データソース**に移動します。
1. **+ データソースを追加**をクリックします。
1. **プラットフォームを選択**画面で、**Tealium Connect**を選択します。
1. **概要**の下にある**名前**フィールドに名前を入力し、**続行**をクリックします。
1. **イベント仕様を選択**ステップで、**続行**をクリックします。
1. イベント仕様を選択して**続行**をクリックするか、**スキップ**をクリックしてこのステップを省略します。
1. **コードを取得**画面に、Tealium ConnectのエンドポイントURLが次の形式で表示されます。  
```
https://collect-us-east-1.tealiumiq.com/dataconnect/event/{{account}}/{{profile}}/{{data source key}}
```
WorkatoでTealium Eventsアプリを構成するには、このキーが必要です。
<blockquote>
[Tealium Private Cloud](https://tealium.com/resource/fundamentals/tealium-private-cloud/)を使用するクライアントの場合、Tealium APIドメインはカスタムドメインになります。
</blockquote>

8. （任意）インストール手順をダウンロードするには、**PDFとしてダウンロード**をクリックします。
9. **保存して続行**をクリックします。
10. データソースの概要が表示されます。
11. **閉じる**をクリックします。  
新しいデータソースが**データソース**ダッシュボードに表示されます。
12. データソースのエンドポイントを有効化するには、プロファイルを**保存／パブリッシュ**します。


<blockquote>
Tealium Connectの構成後にデータソースキーを確認するには、**データソース**ダッシュボードに移動し、使用するデータソースをクリックして、**データソースキー**フィールドからキーをコピーします。
</blockquote>
