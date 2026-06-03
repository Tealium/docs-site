---
title: Google AdWords Customer Match コネクタ構成ガイド
description: この記事では、Google AdWords Customer Match（顧客提供の資格情報とTealium提供の資格情報）コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-adwords-customer-match-connector/
---このコネクタは現在非推奨となり、タグマーケットプレイスでは利用できなくなりました。&lt;br&gt;
**基盤となるGoogle AdWords APIは2022年4月27日に廃止予定です。** **[Google Ads Developer Blog](https://ads-developers.googleblog.com/2021/04/upgrade-to-google-ads-api-from-adwords.html)**から詳細を学びましょう。&lt;br&gt;
既存のGoogle AdWordsコネクタを更新版の[Google Ads Customer Matchコネクタ](/ja/server-side-connectors/google-ads-customer-match-connector/)に置き換える必要があります。

----

## 要件

Google AdWords Customer Matchコネクタには2種類あります。コネクタを追加する際に適切なものを選択してください。

* **Google Adwords Customer Match (顧客提供の資格情報)**
  * [Google](https://developers.google.com/google-ads/api/docs/first-call/dev-token)の承認が必要です。

* **Google Adwords Customer Match (Tealium提供の資格情報)**
  * Tealiumは、申請プロセスを経ることなくボリュームを処理するために事前に承認されています。

## コネクタのアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|リマーケティングリストにユーザーを追加| ✓| ✓|
|リマーケティングリストからユーザーを削除| ✓| ✓|

## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Google Audience Partner API DmpUserListService
* APIバージョン：v201809
* APIエンドポイント：`&lt;https://ddp.googleapis.com/&gt;`
* ドキュメンテーション：[AdWords API](https://developers.google.com/google-ads/api/docs/first-call/dev-token)

## バッチ制限

このコネクタは、ベンダーへの大量のデータ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション]()を参照してください。リクエストは、以下のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

* リクエストの最大数：100000
* 最古のリクエストからの最大時間：60分
* リクエストの最大サイズ：100 MB


## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタの概要](/ja/server-side/connectors/manage/)記事を参照してください。

このコネクタを追加すると、ベンダーのデータプラットフォームポリシーを受け入れるように求められます。

コネクタを追加した後、以下の構成を構成します：

* **AdWords Customer ID**
  * 必須
  * 管理するAdwordsアカウントのCustomer IDを提供します。

* **Developer Token**
  * 必須
  * Googleが承認したAPI開発者トークンを提供します。これは、本番ボリュームのAPIリクエストを行うためのものです。
  * 開発者トークンの取得と承認は、自分で所有し管理する必要がある複数のステップのプロセスです。
  * 開始するには、[ここ](https://developers.google.com/adwords/api/docs/guides/signup)をクリックします。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタのアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - リマーケティングリストにユーザーを追加

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リマーケティングリスト|  &lt;ul&gt;&lt;li&gt;ユーザーを追加するリマーケティングユーザーリストを選択します。&lt;/li&gt;&lt;li&gt;詳細については、[リマーケティングとオーディエンスターゲティング](https://developers.google.com/adwords/api/docs/guides/remarketing)を参照してください。&lt;/li&gt;&lt;li&gt;利用可能なオプションは、ファーストパーティCRMデータタイプのユーザーリストのみを含みます。&lt;/li&gt;&lt;/ul&gt; |
|ユーザー識別子|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;適用可能なユーザー識別子をマップします。&lt;/li&gt;&lt;li&gt;詳細については、[リマーケティングとオーディエンスターゲティング](https://developers.google.com/adwords/api/docs/guides/remarketing)を参照してください。&lt;/li&gt;&lt;li&gt;必須フィールドは選択したリストタイプによります。以下の通りです：  &lt;ul&gt;&lt;li&gt;**連絡先情報** (`CONTACT_INFO`) &lt;ul&gt;&lt;li&gt;最小必須：メール、電話番号、またはすべての住所情報。&lt;/li&gt;&lt;li&gt;メール、電話番号、名前と姓は空白を削除し、小文字にし、SHA-256でエンコードする必要があります。&lt;/li&gt;&lt;li&gt;マップされた値がプレーンテキストの場合は、オプションセクションで**連絡先情報ハッシュ**チェックボックスをチェックします。&lt;/li&gt;&lt;li&gt;国コードは2文字のISO 3166 Alpha-2形式に従う必要があります。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;**CRM** (`CRM_ID`) &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;ユーザーID&lt;/li&gt;&lt;li&gt;広告主が生成し、ホワイトリストに登録されたクライアントのみがアクセス可能。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;**モバイル広告** (`MOBILE_ADVERTISING_ID`) &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;モバイルID&lt;/li&gt;&lt;li&gt;モバイルデバイスID（広告ID/IDFA）。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|連絡先情報ハッシュ|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;マップされた連絡先情報がプレーンテキストである場合はチェックします。&lt;/li&gt;&lt;li&gt;値は自動的にSHA-256でハッシュ化されます。&lt;/li&gt;&lt;/ul&gt; |

### アクション - リマーケティングリストからユーザーを削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リマーケティングリスト|  &lt;ul&gt;&lt;li&gt;ユーザーを削除するリマーケティングユーザーリストを選択します。&lt;/li&gt;&lt;li&gt;詳細については、[リマーケティングとオーディエンスターゲティング](https://developers.google.com/adwords/api/docs/guides/remarketing)を参照してください。&lt;/li&gt;&lt;li&gt;利用可能なオプションは、ファーストパーティCRMデータタイプのユーザーリストのみを含みます。&lt;/li&gt;&lt;/ul&gt; |
|ユーザー識別子|  &lt;ul&gt;&lt;li&gt;必須。&lt;/li&gt;&lt;li&gt;適用可能なユーザー識別子をマップします。&lt;/li&gt;&lt;li&gt;詳細については、[リマーケティングとオーディエンスターゲティング](https://developers.google.com/adwords/api/docs/guides/remarketing)を参照してください。&lt;/li&gt;&lt;li&gt;必須フィールドは選択したリストタイプによります。以下の通りです：  &lt;ul&gt;&lt;li&gt;**連絡先情報** (`CONTACT_INFO`)  &lt;ul&gt;&lt;li&gt;最小必須：メール、電話番号、またはすべての住所情報。&lt;/li&gt;&lt;li&gt;メール、電話番号、名前と姓は空白を削除し、小文字にし、SHA-256でエンコードする必要があります。&lt;/li&gt;&lt;li&gt;マップされた値がプレーンテキストの場合は、オプションセクションで**連絡先情報ハッシュ**チェックボックスをチェックします。&lt;/li&gt;&lt;li&gt;国コードは2文字のISO 3166 Alpha-2形式に従う必要があります。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;**CRM** (`CRM_ID`)  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;ユーザーID&lt;/li&gt;&lt;li&gt;広告主が生成し、ホワイトリストに登録されたクライアントのみがアクセス可能。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;**モバイル広告** (`MOBILE_ADVERTISING_ID`)  &lt;ul&gt;&lt;li&gt;必須&lt;/li&gt;&lt;li&gt;モバイルID&lt;/li&gt;&lt;li&gt;モバイルデバイスID（広告ID/IDFA）。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|連絡先情報ハッシュ|  &lt;ul&gt;&lt;li&gt;オプション&lt;/li&gt;&lt;li&gt;マップされた連絡先情報がプレーンテキストである場合はチェックします。&lt;/li&gt;&lt;li&gt;値は自動的にSHA-256でハッシュ化されます。&lt;/li&gt;&lt;/ul&gt; |
