---
title: Pega Webhook コネクタ構成ガイド
description: この記事では、Pega API用にカスタムリクエストアクションを送信するための高度なWebhookを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/pega-webhook-connector/
---
## 前提条件

* [Pega Customer Decision Hub](https://docs.pega.com/pega-customer-decision-hub-implementation-guide/87/pega-customer-decision-hub-implementation-guide)の構成
* Tealium EventStream API HubまたはTealium AudienceStream CDP

## 動作原理

PegaのアウトゴーイングWebhookは、PegaのCustomer Decision Hub、Next-Best-Actionsデザイナー、およびCustomer Profileデザイナーとの統合を可能にします。TealiumとPegaを一緒に使用することで、セキュリティ規制を遵守し、リアルタイムデータ収集を活用してより迅速に対応し、Next-Bestエクスペリエンスメッセージで個々の顧客を特定してターゲットにすることができます。Pegaとの統合により、TealiumのデータがPegaを通じてニュースレタープロモーションやプロモーションコードの提供など、カスタム顧客インタラクションをトリガーすることができ、カスタマージャーニーをパーソナライズするのに役立ちます。はじめに、Pegaにファーストパーティのパーソナライズデータを送信するHTTPリクエストを送信してください。

## ベンダー要件

### リクエストURL

PegaのDesigner Studioを使用して、PegaでカスタムリクエストURLを作成できます。リクエストURLは、Pegaの実装とPegaアカウントのサービスパッケージに基づいています。リクエストURLを作成する際には、特定のパスパラメータを含める必要があります。カスタムURLの変数とパスパラメータを指定するために、RESTサービスを構成するには、Pegaのドキュメントにある[Creating a Service REST rule](https://docs.pega.com/data-management-and-integration/87/creating-service-rest-rule)を参照してください。Service RESTルールを作成した後、[configuring the resources and processing details](https://docs.pega.com/data-management-and-integration/87/defining-resource-and-processing-details-service-rest-rule)でRESTルールの構成を完了してください。

PegaのAPI、APIのベストプラクティス、およびREST統合の作成に関する詳細情報については、Pegaのドキュメントにある[Pega APIs and services](https://docs.pega.com/data-management-and-integration/84/pega-apis-and-services)を参照してください。

### メソッドフィールド

サービスRESTルールで使用できるメソッドについての詳細は、Pegaのドキュメントにある[Service REST methods](https://docs.pega.com/data-management-and-integration/87/service-rest-methods)を参照してください。

## Webhook例

リクエスト本体は、カスタマイズ可能な本体テンプレートを持つJSONメッセージです。PegaはネストされたJSONまたはフラットJSONのいずれかを受け入れます。JSONリクエストの構造は、Designer Studioで指定されたPegaの実装とデータポイントに依存します。

Webhookコネクタの構成方法についての詳細は、を参照してください。

この例では、Webhookがユーザーを識別するパラメータを持つ`PageView`リクエストを送信します。

* **メソッド**: `POST`
* **URL**: `https://&lt;host&gt;:&lt;port&gt;/prweb/PRRestService/&lt;servicepackage&gt;/&lt;serviceclass&gt;/&lt;servicemethod&gt;`
* **本体コンテンツタイプ**: `application/json`
* **本体データ**: ``Map `{{data}}` To Body``
* **テンプレート変数:**
  * `Map &#34;PageView&#34; To Intent`
  * `Map customer_id to ID`
  * `Map tealium_firstparty_visitor_id To Cookieidvalue`
  * `Map Last event timestamp To time`

* **テンプレート**:
  * 名前: `data`
  * テンプレート:  
```json
{
  &#34;Cookieidvalue&#34;: &#34;{{Cookieidvalue}}&#34;,
  &#34;ID&#34;: &#34;{{ID}}&#34;,
  &#34;Intent&#34;: &#34;{{Intent}}&#34;,
  &#34;Lastviewedproduct&#34;: &#34;{{time}}&#34;
}
```