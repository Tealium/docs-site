---
title: Salesforce Journey Builder コネクタ構成ガイド
description: Salesforce Marketing Cloud アカウントを接続し、イベントデータを送信してカスタマージャーニーをトリガーまたは一括トリガーします。
url: https://docs.tealium.com/ja/server-side-connectors/salesforce-journey-builder-connector/
---
## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を行います。

* **クライアント ID**
  * （必須）アプリのクライアント ID を指定します。
  * 詳細については、[Salesforce：OAuth クライアント認証情報の取得](https://developer.salesforce.com/docs/atlas.en-us.mc-getting-started.meta/mc-getting-started/get-api-key.htm)を参照してください。

* **クライアントシークレット**
  * （必須）アプリのクライアントシークレットを指定します。

* **アカウント ID**
  * （必須）対象ビジネスユニットのアカウント識別子（MID）を指定します。

* **テナント固有のサブドメイン**
  * （必須）アプリケーションのテナント固有のサブドメインを指定します。

コネクタを構成した後、**完了**をクリックします。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| ジャーニーを開始するイベントを送信 | ✓ | ✗ |
| ジャーニーを開始するイベントを送信（バッチ） | ✓ | ✗ |

### ジャーニーを開始するイベントを送信

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| イベントエントリ定義 | （必須）イベントエントリ定義を選択するか、手動で入力します。ドロップダウンリストには新しいものから古いものの順にエントリが表示され、最大 2,000 件まで表示されます。詳細については、[Salesforce：POST /interaction/v1/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html)を参照してください。 |
| コンタクトキー | （必須）コンタクトキーを指定します。 |
| イベントデータ | カスタムイベントで定義されている場合、またはイベントによって指定されている場合は必須です。値をコンタクトイベント属性にマッピングします。詳細については、[Salesforce：POST /interaction/v1/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html)を参照してください。 |

### ジャーニーを開始するイベントを送信（バッチ）

このアクションは、購読者のバッチを非同期でジャーニーに追加します。一括インポートや高頻度のイベントデータには、このアクションを使用します。

#### バッチ制限

このアクションでは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。並列処理により、イベントが順不同でベンダーに到達する場合があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。以下のいずれかのしきい値に達するか、プロファイルが公開されるまで、リクエストはキューに保持されます。

* リクエストの最大数：100
* 最も古いリクエストからの最大経過時間：5 分
* リクエストの最大サイズ：10 MB

このアクションのパラメータは、[ジャーニーを開始するイベントを送信](#send-event-to-initiate-journey)と同じです。

## ベンダーのドキュメント

* [Salesforce：OAuth クライアント認証情報の取得](https://developer.salesforce.com/docs/atlas.en-us.mc-getting-started.meta/mc-getting-started/get-api-key.htm)
* [Salesforce：POST /interaction/v1/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html)
* [Salesforce：エントリイベントとデータ定義](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/event-definition-key.html#:~:text=Event%20definitions%20define%20the%20name,the%20journey%20to%20be%20published.)
* [Salesforce：POST /interaction/v1/async/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/enterContactsIntoJourneyInBatches.html)