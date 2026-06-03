---
title: Salesforce Journey Builder コネクタ構成ガイド（廃止）
description: Salesforce Marketing Cloud Journey Builderは、顧客を1対1の旅に導き、適切なデジタルマーケティングソリューションを適切なチャネルで提供することができます。この記事では、Customer Data Hubプロファイルでコネクタを構成するプロセスを説明します。
url: https://docs.tealium.com/ja/server-side-connectors/salesforce-journey-builder-connector-deprecated/
---
このコネクタは、コネクタマーケットプレイスで利用できなくなりました。OAuth 2.0サポートを含むこのコネクタの最新バージョンについては、[Salesforce Journey Builder with OAuth Connector Setup Guide]()を参照してください。

## 必要条件

* Salesforce Marketing Cloudアプリクライアントの資格情報
* Salesforce Marketing Cloudアカウント
* Journey
* イベントエントリー定義

## サポートされているアクション

|**アクション名**| **オーディエンスにトリガー**| **ストリームにトリガー**|
|---| ---| ---|
|Journeyを開始するためのイベント送信| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいSalesforce Marketing Cloudコネクタを追加します。コネクタの追加方法については、[Connector Overview]()の記事を参照してください。

ベンダーを構成するには、次の手順に従います：

* **Configure**タブで、コネクタインスタンスにタイトルを提供します。

* Marketing CloudアプリのクライアントIDとクライアントシークレットを提供します。

* 提供された資格情報でAPI接続を確認するために**Test Connection**をクリックします。

詳細については、[Get App Client Credentials](https://developer.salesforce.com/docs/atlas.en-us.mc-getting-started.meta/mc-getting-started/get-api-key.htm)を参照してください。

## アクション構成 - パラメータとオプション

**Next**をクリックするか、**Actions**タブに移動します。ここでアクションのトリガーを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - Journeyを開始するためのイベント送信

#### パラメータ

1. **Event Entry Definition**（必須）：このリストから、journeyを開始するためのイベントデータ形式を指定するイベントエントリー定義を選択します。
1. **Contact Key**（必須）：連絡先イベントデータを一意に識別するための属性をマッピングします。
1. **Event Data**（必須）：属性を連絡先イベント属性にマッピングします。属性名は、選択したイベント定義のデータ拡張属性と一致する必要があります（参照：[Entry Events and Data Definitions](http://help.marketingcloud.com/en/documentation/journey_builder/entry_sources/entry_events/entry_events_and_data_extensions/)）。
1. **Disable Auto Create Contact**：デフォルトでは、新しい連絡先キーでイベントデータを送信すると新しい連絡先が作成されます。新しい連絡先は、journeyに注入するために利用可能になります。このオプションをチェックすると、連絡先の自動作成が無効になります。

詳細については、[Admit Contacts via API](http://help.marketingcloud.com/en/documentation/journey_builder/entry_sources/entry_events/admit_contacts_via_api/)を参照してください。

## ベンダー文書

* [Get App Client Credentials](https://developer.salesforce.com/docs/atlas.en-us.mc-getting-started.meta/mc-getting-started/get-api-key.htm)
* [Admit Contacts via API](http://help.marketingcloud.com/en/documentation/journey_builder/entry_sources/entry_events/admit_contacts_via_api/)
* [Entry Events and Data Definitions](http://help.marketingcloud.com/en/documentation/journey_builder/entry_sources/entry_events/entry_events_and_data_extensions/)
