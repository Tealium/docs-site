---
title: データソースに接続する
description: この記事では、アカウントにデータソースを追加し、接続する方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/platform-data-sources/connect-to-data-source/
---
## コードとデータソースキー

データソースのコードをインストールするには、データソースキーとインストールガイドへのリンクが必要です。

データソースキーを取得するには：

1. サイドバーで、**Connect &gt; Data Sources**を選択します。
1. インストールしたいデータソースの名前をクリックして詳細を展開します。
1. 詳細ビューから、**Data Source Key**の値をコピーします。  
      ![](/images/server-side/whiteui-viewdatasource-datasourcekey.png)
1. プラットフォームのインストール手順を使用して、データソースキーの値をコードに貼り付けます。
1. データソースの詳細が展開された状態で、**Get Code**をクリックします。  
      ![](/images/server-side/whiteui-editdatasource-getcode.png)**Get Code**ダイアログが表示されます。このダイアログから、インストール手順が記載されたPDFをダウンロードしたり、基本コードを表示・コピーしたり、イベントトラッキングコードを表示・コピーしたりすることができます。  
      ![](/images/server-side/whiteui-getcode.png)
1. ウィンドウに表示されるコードをコピーします。
1. プラットフォームのインストール手順を使用して、コードをインストールします。
1. **Close**をクリックしてGet Codeダイアログを閉じます。


## Webhooks

Webhookデータソースは、生成された一意のURLで構成されています。データソースキーはWebhook URLに追加されて一意になります。

WebhookデータソースURLの形式は次のとおりです：

```
https://collect.tealiumiq.com/integration/event/ACCOUNT/PROFILE/DATA_SOURCE_KEY
```

## データソースの確認

データソースのコードを保存、公開、インストールした後、Live Eventsを使用して構成を確認します。

データソースを表示し、確認するための手順は次のとおりです：

1. データソースの詳細が展開された状態で、**Live Events**チャートアイコンをクリックして、このデータソースにフィルタリングされたライブイベントを表示します。
1. インストールでテストイベントをトリガーし、Live Eventsフィードで表示されるのを確認します。