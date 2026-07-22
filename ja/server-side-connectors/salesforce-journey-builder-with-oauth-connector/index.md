---
title: Salesforce Journey BuilderとOAuthコネクタの構成ガイド
description: この記事では、Customer Data HubアカウントでSalesforce Journey Builderコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/salesforce-journey-builder-with-oauth-connector/
---

<blockquote>
このコネクタは、廃止されたSalesforce Journey Builderコネクタを置き換えます。
</blockquote>


## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ジャーニーの開始イベントを送信| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタの概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **クライアントID**
  * 必須。
  * アプリのクライアントIDを提供します。
  * 詳細情報については、[OAuthクライアント資格情報の取得](https://developer.salesforce.com/docs/atlas.en-us.mc-getting-started.meta/mc-getting-started/get-api-key.htm)を参照してください。

* **クライアントシークレット**
  * 必須。
  * アプリのクライアントシークレットを提供します。

* **アカウントID**
  * 必須。
  * ターゲットビジネスユニットのアカウント識別子（MID）を提供します。

* **テナント固有のサブドメイン**
  * 必須。
  * アプリケーションのテナント固有のサブドメインを提供します。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ジャーニーの開始イベントを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|イベントエントリ定義|  <ul><li>必須。</li><li>イベントエントリ定義を選択します。</li><li>参照：[API経由でコンタクトを認証](http://help.marketingcloud.com/en/documentation/journey_builder/entry_sources/entry_events/admit_contacts_via_api/)</li></ul> |
|コンタクトキー|  <ul><li>必須。</li><li>コンタクトキーを提供します。</li></ul> |
|イベントデータ|  <ul><li>カスタムイベントまたはイベントで定義されている場合は必須。</li><li>値をコンタクトイベント属性にマッピングします。</li><li>Salesforceの[イベントの発火](http://help.marketingcloud.com/en/documentation/journey_builder/entry_sources/entry_events/entry_events_and_data_extensions/)ドキュメンテーションを参照してください。</li></ul> |

## ベンダードキュメンテーション

* [OAuthクライアント資格情報の取得](https://developer.salesforce.com/docs/atlas.en-us.mc-getting-started.meta/mc-getting-started/get-api-key.htm)
* [API経由でコンタクトを認証](http://help.marketingcloud.com/en/documentation/journey_builder/entry_sources/entry_events/admit_contacts_via_api/)
* [エントリイベントとデータ定義](http://help.marketingcloud.com/en/documentation/journey_builder/entry_sources/entry_events/entry_events_and_data_extensions/)<br>
