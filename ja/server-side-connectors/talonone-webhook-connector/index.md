---
title: Talon.One Webhookコネクタ構成ガイド
description: この記事では、Talon.One APIのテンプレート変数を使用してカスタムリクエストアクションを送信するためのWebhookを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/talonone-webhook-connector/
---
## 概要

Talon.Oneは、訪問とセッションデータを中心に構築したターゲット指向のカスタマイズされたマーケティングプロモーションを作成できる強力なプロモーションエンジンです。割引、クーポンコード、紹介、ロイヤルティ、商品バンドルを一つの包括的なプラットフォームで作成、管理、追跡します。

Talon.Oneの統合により、TealiumからTalon.Oneへリアルタイムで訪問データ（標準化、統一、豊富）をストリームし、マーケティングキャンペーンでパーソナライズされたプロモーションを作成することができます。

## 前提条件

* Talon.Oneプロモーションプラットフォームの構成
* Tealium EventStream API HubまたはTealium AudienceStream CDPの構成

## 仕組み

Tealium for Talon.OneのアウトゴーイングWebhookは、Talon.Oneの強力なプロモーションエンジンとの統合を可能にします。Tealiumの堅牢なリアルタイムデータ収集を使用して、Talon.Oneにより関連性の高いパーソナライズされたデータを送信し、個々の顧客を特定し、高度に関連性のあるキャンペーンでターゲットにすることができます。

開始するには、以下の手順を実行します：

1. Talon.Oneを構成します。
1. Tealiumで、データをTalon.Oneに送信するためのWebhookを構成します。

これで、HTTPリクエストを送信して、第一者のパーソナライズされたデータ（Tealium EventStream API Hubからのイベントデータ）またはユーザーデータ（Tealium AudienceStream CDPから）をTalon.Oneに送信することができます。Talon.Oneは、基本認証を使用するWebhook構成をサポートしています。詳細については、[Webhookコネクタ構成ガイド](https://docs.tealium.com/webhook-connectors/)を参照してください。

## Talon.Oneの構成

1. キャンペーンマネージャーでTalon.Oneアプリケーションを開き、**構成 &gt; 開発者構成**をクリックします。
1. **APIキーを作成**をクリックします。  
詳細については、Talon.Oneのドキュメンテーションの[APIキーの管理](https://hubs.li/Q01lKrrX0)を参照してください。
1. **このAPIキーを第三者サービスと使用しますか？**で、**はい**を選択します。
1. ドロップダウンから**Customer Data Platform**を選択します。
1. 有効期限を入力し、**APIキーを作成**をクリックします。
1. APIキーをコピーします。これはTealiumでWebhookを構成するために使用されます。

この統合の構成についての詳細は、[Talon.Oneのドキュメンテーション](https://docs.talon.one/docs/product/applications/managing-api-keys/)を参照してください。

## Talon.OneのアウトゴーイングWebhookの構成

Webhookには以下のデータマッピングが必要です：

* **Method**を`POST`に構成します。
* **URL**を`https://integration.talon.one/cdp/audiences`に構成します。

例：

![](https://docs.tealium.com/images/server-side-connectors/httprequestrequiredps.png)

Talon.Oneにデータを送信するためには、以下の構成も必要です：

* `Body Data`
* `Body Content Type`
* Talon.Oneに送信したい変数

## Webhook構成の例

この例では、リクエストボディはカスタマイズ可能なボディテンプレートを持つJSONメッセージです。Webhookコネクタの構成についての詳細は、[Webhookテンプレート変数ガイド](https://docs.tealium.com/connector-template-variables/)を参照してください。

この例のWebhookは、ユーザーを特定するパラメータを持つ`PageView`リクエストを送信します：

* **Method**: `POST`
* **URL**: `Https://integration.talon.one/cdp/audiences`
* **Body Content Type**: `application/json`
* **Body Data**: `Map {{data}} To Body`
* **Template Variables**:
  * "PageView"を`Intent`にマップします
  * `customer_id`を`ID`にマップします
  * `tealium_firstparty_visitor_id`を`Cookieidvalue`にマップします
  * `Last event timestamp`を`time`にマップします

* **Templates**:
  * **Name**: `data`
