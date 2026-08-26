---
title: Salesforce Journey Builder コネクタ構成ガイド
description: Salesforce Marketing Cloud アカウントに接続し、イベントデータを送信して顧客ジャーニーをトリガーまたはバッチトリガーします。
url: https://docs.tealium.com/ja/server-side-connectors/salesforce-journey-builder-connector/
---
## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタの追加方法についての一般的な説明については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **クライアントID**
  * （必須）アプリのクライアントIDを提供してください。
  * 詳細については、[Salesforce: OAuthクライアント認証情報の取得](https://developer.salesforce.com/docs/atlas.en-us.mc-getting-started.meta/mc-getting-started/get-api-key.htm)を参照してください。

* **クライアントシークレット**
  * （必須）アプリのクライアントシークレットを提供してください。

* **アカウントID**
  * （必須）対象ビジネスユニットのアカウント識別子（MID）を提供してください。

* **テナント固有のサブドメイン**
  * （必須）アプリケーションのテナント固有のサブドメインを提供してください。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| ジャーニーを開始するためのイベント送信 | ✓ | ✗ |
| ジャーニーを開始するためのイベント送信（バッチ処理） | ✓ | ✗ |

### ジャーニーを開始するためのイベント送信

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| イベントエントリ定義 | （必須）イベントエントリ定義を選択するか、手動で入力してください。ドロップダウンリストは最新のエントリから表示され、最大2000エントリを表示します。詳細については、[Salesforce: POST /interaction/v1/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html)を参照してください。 |
| コンタクトキー | （必須）コンタクトキーを提供してください。 |
| イベントデータ | カスタムイベントで定義されている場合、またはイベントによって指定されている場合は必須です。値をコンタクトイベント属性にマッピングしてください。詳細については、[Salesforce: POST /interaction/v1/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html)を参照してください。 |

### ジャーニーを開始するためのイベント送信（バッチ処理）

このアクションは、非同期的にバッチのサブスクライバーをジャーニーに入力します。バルクインポートや高頻度のイベントデータにこのアクションを使用してください。

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。並列処理により、イベントがベンダーに順不同で到達する可能性があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチ処理アクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：100
* 最古のリクエストからの最大時間：5分
* リクエストの最大サイズ：10 MB

このアクションのパラメータは[ジャーニーを開始するためのイベント送信](#send-event-to-initiate-journey)と同一です。

## ベンダー文書

* [Salesforce: OAuthクライアント認証情報の取得](https://developer.salesforce.com/docs/atlas.en-us.mc-getting-started.meta/mc-getting-started/get-api-key.htm)
* [Salesforce: POST /interaction/v1/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html)
* [Salesforce: エントリイベントとデータ定義](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/event-definition-key.html#:~:text=Event%20definitions%20define%20the%20name,the%20journey%20to%20be%20published.)
* [Salesforce: POST /interaction/v1/async/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/enterContactsIntoJourneyInBatches.html)