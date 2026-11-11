---
title: Slackコネクタ構成ガイド
description: Slackは、すべてのコミュニケーションを1か所に集約します。この連携を使用すると、任意の会話に自動メッセージを投稿できます。この記事では、Customer Data HubアカウントでSlackコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/slack-connector/
---
### コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|チャンネルメッセージを投稿| ✓| ✓|
|チャンネルに拡張メッセージを投稿| ✓| ✓|

### 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/ja/server-side/connectors/manage/)の記事を参照してください。

コネクタを追加した後に構成する構成はありません。**完了**をクリックして、次の手順に進みます。

### アクション構成 — パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

以下のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

#### アクション — チャンネルメッセージを投稿

##### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アプリからのWebhook URL| アプリによって生成されたWebhook URL。<br>詳細については、[Incoming Webhook入門](https://api.slack.com/messaging/webhooks#getting_started)を参照してください。|
|メッセージ| 上記で指定したWebhook URLに関連付けられているチャンネルに送信するメッセージ。[Slackのメッセージ書式](https://api.slack.com/docs/message-formatting)の詳細を確認してください。|

#### アクション — チャンネルに拡張メッセージを投稿

##### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|アプリからのWebhook URL| アプリによって生成されたWebhook URL。<br>詳細については、[Incoming Webhook入門](https://api.slack.com/messaging/webhooks#getting_started)を参照してください。|
|Blocksテンプレート変数| Blocksのデータ入力としてテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<br>ネストされたテンプレート変数には、ドット表記を使用して名前を付けます（例：`items.name`）。<br>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から構築されます。|
|Blocks| メッセージを拡張するためのBlock Kitビジュアルコンポーネント。<br>送信する**blocks**配列の配列テンプレートを指定します。<br>テンプレート変数を使用できます。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。|
|メッセージ| 上記で指定したWebhook URLに関連付けられているチャンネルに送信するメッセージ。[Slackのメッセージ書式](https://api.slack.com/docs/message-formatting)の詳細を確認してください。|