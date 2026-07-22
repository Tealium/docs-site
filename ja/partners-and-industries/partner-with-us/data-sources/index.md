---
title: データソース
description: 受信データ統合を使用して、アプリケーションからTealiumにデータを送信する方法を学びます。
url: https://docs.tealium.com/ja/partners-and-industries/partner-with-us/data-sources/
---

データソースはデータをTealiumに送信します。データソースはウェブサイト、CRMシステム、モバイルSDK、サーバーサイドアプリケーション、あるいはウェブフックであることができます。可能なデータソースの数は無限ですが、Tealiumにデータを送信する主な方法は2つあります：ウェブベースとAPIベースです。プラットフォームに合った方法を選び、Tealiumにデータを送信する方法を決定します。

## ウェブ

ウェブベースの統合は、Tealium Universal Tag (utag.js)とUniversal Data Object (utag_data)を使用して、Tealium Collectタグ（データをTealium Customer Data Hubに送信するJavaScriptタグ）をロードします。最も一般的なウェブベースの統合はCMSプラグインです。Tealiumプラグインは、CMSのページに必要なJavaScriptタグとデータレイヤーオブジェクトを追加します。

成功したCMS統合は、Universal Tagをロードし、ページ名、サイト言語、ユーザーログインステータスなどの組み込みシステムデータでデータレイヤーを動的に充実させます。電子商取引プラットフォームは、システム内の関連ページに商品と注文の変数を充実させます。

ウェブ統合の例には以下のようなものがあります：

* JavaScript（ウェブ）
* Angular
* Magento
* Shopify
* SiteCore

詳細を学ぶ

* [データレイヤーへの導入](https://docs.tealium.com/an-introduction-to-the-data-layer/)
* [JavaScriptのインストール](https://docs.tealium.com/ja/platforms/javascript/install/)

## API

APIベースの統合は、Tealium Collect HTTPエンドポイントまたはカスタムエンドポイントを使用して、データをTealium Customer Data Hubに送信します。このアプローチは、システムがトリガーされたコールバックやウェブフックをサポートしている場合に便利です。API統合の最も一般的なプラットフォームはCRMとメールマーケティングプラットフォームです。

以下に、利用可能なAPIデータソース統合をリストします：

- [Affirm](https://docs.tealium.com/affirm-incoming-webhook-setup-guide/)
- [Airship](https://docs.tealium.com/airship-incoming-webhook-setup-guide/)
- [Braze Currents](https://docs.tealium.com/braze-currents-data-source-setup-guide/)
- [Hubspot](https://docs.tealium.com/hubspot-workflow-incoming-webhook-setup-guide/)
- [Intercom](https://docs.tealium.com/intercom-incoming-webhook-setup-guide/)
- [Iterable](https://docs.tealium.com/iterable-incoming-webhook-setup-guide/)
- [Mailchimp](https://docs.tealium.com/mailchimp-incoming-webhook-setup-guide/) ([例を見る](#example-mailchimp))
- Salesforce
- [SendGrid](https://docs.tealium.com/sendgrid-incoming-webhook-setup-guide/)
- Zapier

詳細を学ぶ

* [Tealium HTTP API](https://docs.tealium.com/ja/platforms/http-api/)


## 利点

データソース統合の利点には以下のようなものがあります：

- Tealiumユーザーは、さまざまなシステムからのデータを簡単にオンボードし、統合してパーソナライズされた顧客体験を作り出すことができます。
- Tealiumユーザーは、すべての受信データの起源を特定し、データサプライチェーンの理解を深めることができます。
- 受信データの品質が高まります。


<blockquote>
Tealiumは、いくつかのクラウド保存プロバイダからCSVファイルを処理する[file import data source](https://docs.tealium.com/about-file-import/)を提供しています。ただし、現在、パートナー向けの統合方法としてファイルインポートは提供されていません。
</blockquote>



## 例：Mailchimp

Mailchimpは、すべてが一つになったマーケティングプラットフォームで、購読、プロフィール更新、メール変更、キャンペーンステータスなどの一般的なメールアクションのウェブフックを提供しています。例えば、MailChimpが購読アクションを受け取ると、そのイベントに関連するデータを含むウェブフックをトリガーすることができます。この場合、`subscribe`イベントタイプには以下のフィールドがあります（括弧はネストしたJSONを示します）：

```
{
  "type": "subscribe",
  "fired_at": "2009-03-26 21:35:57",
  "data[id]": "8a25ff1d98",
  "data[list_id]": "a6b5da1054",
  "data[email]": "api@mailchimp.com",
  "data[email_type]": "html",
  "data[merges][EMAIL]": "api@mailchimp.com",
  "data[merges][FNAME]": "Mailchimp",
  "data[merges][LNAME]": "API",
  "data[merges][INTERESTS]": "Group1,Group2",
  "data[ip_opt]": "10.20.10.30",
  "data[ip_signup]": "10.20.10.30"
}
```

Tealiumの公式データソース統合とMailchimpとの統合は、一般的なHTTP APIを使用することから得られる以下の追加の利点を提供します：

* **専用エンドポイント**  
Tealiumはこのデータソースのためにカスタマイズされたエンドポイントを発行します。例：`https://collect.tealiumiq.com/integration/event/my_account/main/abc123`。
* **変数の転置**  
TealiumはJSONボディをフラット化し、すべてのフィールド名に`mailchimp_`を前置して、すべてのMailChimpデータに独自の名前空間を与えます。例えば、`"data[merges][EMAIL]"`は`mailchimp_data_merges_email`になります。

これらの利点は、すべての下流のデータエンリッチメントとアクションに対して改善されたデータ品質とガバナンスを提供します。MailChimpデータソースを他のデータソースと活性化と組み合わせることで、Tealiumユーザーはより正確で最新の顧客ビューを維持することができます。

詳細を学ぶ：[MailChimp Incoming Webhook Setup Guide](https://docs.tealium.com/mailchimp-incoming-webhook-setup-guide/)

## パートナーになる

[お問い合わせ](https://tealium.com/tealium-partner-network/)して、あなたの技術を統合してください。