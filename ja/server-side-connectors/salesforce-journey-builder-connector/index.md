---
title: Salesforce Journey Builder コネクタ構成ガイド
description: この記事では、Customer Data Hub アカウントで Salesforce Journey Builder コネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/salesforce-journey-builder-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ジャーニーを開始するためのイベント送信| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()の記事を読んでください。

コネクタを追加した後、以下の構成を構成します：

* **クライアントID**
  * 必須。
  * アプリのクライアントIDを提供してください。
  * 追加情報については、こちらを参照してください：[OAuthクライアント認証情報の取得](https://developer.salesforce.com/docs/atlas.en-us.mc-getting-started.meta/mc-getting-started/get-api-key.htm)

* **クライアントシークレット**
  * 必須。
  * アプリのクライアントシークレットを提供してください。

* **アカウントID**
  * 必須。
  * 対象ビジネスユニットのアカウント識別子（MID）を提供してください。

* **テナント固有のサブドメイン**
  * 必須。
  * アプリケーションのテナント固有のサブドメインを提供してください。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ジャーニーを開始するためのイベント送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベントエントリ定義|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;イベントエントリ定義を選択するか、手動で入力します。&lt;/li&gt;&lt;li&gt;ドロップダウンリストは新しい順にリストされ、最大2000エントリが表示されます。&lt;/li&gt;&lt;li&gt;詳細については、[Salesforce: POST /interaction/v1/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|コンタクトキー|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;コンタクトキーを提供してください。&lt;/li&gt;&lt;/ul&gt; |
|イベントデータ|  &lt;ul&gt;&lt;li&gt;カスタムイベントで定義されている場合、またはイベントによって指定されている場合は必須。&lt;/li&gt;&lt;li&gt;コンタクトイベント属性に値をマッピングします。&lt;/li&gt;&lt;li&gt;詳細については、[Salesforce: POST /interaction/v1/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html)を参照してください。&lt;/li&gt;&lt;/ul&gt; |

## ベンダー文書

* [Salesforce: OAuthクライアント認証情報の取得](https://developer.salesforce.com/docs/atlas.en-us.mc-getting-started.meta/mc-getting-started/get-api-key.htm)
* [Salesforce: POST /interaction/v1/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html)
* [Salesforce: エントリイベントとデータ定義](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/event-definition-key.html#:~:text=Event%20definitions%20define%20the%20name,the%20journey%20to%20be%20published.)
