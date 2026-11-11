---
title: Pega Webhookコネクタ構成ガイド
description: この記事では、テンプレート変数を使用してPega APIにカスタムリクエストアクションを送信する、高度なWebhookの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/pega-webhook-connector/
---
## 前提条件

* [Pega Customer Decision Hub](https://docs.pega.com/pega-customer-decision-hub-implementation-guide/87/pega-customer-decision-hub-implementation-guide)を構成する
* Event Streaming API HubまたはCustomer Data Platform（CDP）

## 仕組み

Pegaの送信Webhookを使用すると、PegaのCustomer Decision Hub、Next-Best-Actionsデザイナー、およびCustomer Profileデザイナーと連携できます。TealiumとPegaを併用することで、セキュリティ規制への準拠、リアルタイムデータ収集を活用した迅速な対応、Next-Best-Experienceメッセージによる個々の顧客の識別とターゲティングが可能になります。Pegaと連携すると、Tealiumのデータをトリガーとして、ニュースレターによるプロモーションやPegaを通じたプロモーションコードの提供など、カスタムの顧客インタラクションを実行でき、カスタマージャーニーのパーソナライズに役立ちます。開始するには、HTTPリクエストを送信して、パーソナライズされたファーストパーティデータをPegaに送信します。

## ベンダー要件

### リクエストURL

PegaのDesigner Studioを使用して、カスタムリクエストURLを作成できます。リクエストURLは、使用しているPegaの実装とPegaアカウント内のサービスパッケージに基づきます。リクエストURLを作成する際は、特定のパスパラメータを含める必要があります。カスタムURLの変数とパスパラメータの指定を含むRESTサービスの構成方法については、Pegaドキュメントの[Service RESTルールの作成](https://docs.pega.com/data-management-and-integration/87/creating-service-rest-rule)を参照してください。Service RESTルールを作成したら、そのルールの[リソースと処理の詳細を構成](https://docs.pega.com/data-management-and-integration/87/defining-resource-and-processing-details-service-rest-rule)して、RESTルールの構成を完了します。


<blockquote>
PegaのすべてのAPI、APIのベストプラクティス、およびREST連携の作成方法について詳しくは、Pegaドキュメントの[PegaのAPIとサービス](https://docs.pega.com/data-management-and-integration/84/pega-apis-and-services)を参照してください。
</blockquote>


### メソッドフィールド

Service RESTルールで使用できるメソッドについて詳しくは、Pegaドキュメントの[Service RESTのメソッド](https://docs.pega.com/data-management-and-integration/87/service-rest-methods)を参照してください。

## Webhookの例

リクエストボディは、カスタマイズ可能なボディテンプレートを持つJSONメッセージです。Pegaは、ネストされたJSONとフラットなJSONのいずれも受け付けます。JSONリクエストの構造は、Pegaの実装とDesigner Studioで指定したデータポイントによって異なります。

Webhookコネクタの構成について詳しくは、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。

この例では、Webhookはユーザーを識別するためのパラメータを含む`PageView`リクエストを送信します。

* **メソッド**: `POST`
* **URL**: `https://<host>:<port>/prweb/PRRestService/<servicepackage>/<serviceclass>/<servicemethod>`
* **ボディのコンテンツタイプ**: `application/json`
* **ボディデータ**: ``Map `{{data}}` To Body``
* **テンプレート変数:**
  * `Map "PageView" To Intent`
  * `Map customer_id to ID`
  * `Map tealium_firstparty_visitor_id To Cookieidvalue`
  * `Map Last event timestamp To time`

* **テンプレート**:
  * 名前: `data`
  * テンプレート:  
```json
{
  "Cookieidvalue": "{{Cookieidvalue}}",
  "ID": "{{ID}}",
  "Intent": "{{Intent}}",
  "Lastviewedproduct": "{{time}}"
}
```