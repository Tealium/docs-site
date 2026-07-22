---
title: Google AdWords Customer Match コネクタ構成ガイド
description: この記事では、Google AdWords Customer Match（顧客提供の資格情報とTealium提供の資格情報）コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-adwords-customer-match-connector/
---
<blockquote>
このコネクタは現在非推奨となり、タグマーケットプレイスでは利用できなくなりました。<br>
**基盤となるGoogle AdWords APIは2022年4月27日に廃止予定です。** **[Google Ads Developer Blog](https://ads-developers.googleblog.com/2021/04/upgrade-to-google-ads-api-from-adwords.html)**から詳細を学びましょう。<br>
既存のGoogle AdWordsコネクタを更新版の[Google Ads Customer Matchコネクタ](https://docs.tealium.com/ja/server-side-connectors/google-ads-customer-match-connector/)に置き換える必要があります。
</blockquote>


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
* APIエンドポイント：`<https://ddp.googleapis.com/>`
* ドキュメンテーション：[AdWords API](https://developers.google.com/google-ads/api/docs/first-call/dev-token)

## バッチ制限

このコネクタは、ベンダーへの大量のデータ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、以下のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

* リクエストの最大数：100000
* 最古のリクエストからの最大時間：60分
* リクエストの最大サイズ：100 MB


## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタの概要](https://docs.tealium.com/ja/server-side/connectors/manage/)記事を参照してください。


<blockquote>
このコネクタを追加すると、ベンダーのデータプラットフォームポリシーを受け入れるように求められます。
</blockquote>


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
|リマーケティングリスト|  <ul><li>ユーザーを追加するリマーケティングユーザーリストを選択します。</li><li>詳細については、[リマーケティングとオーディエンスターゲティング](https://developers.google.com/adwords/api/docs/guides/remarketing)を参照してください。</li><li>利用可能なオプションは、ファーストパーティCRMデータタイプのユーザーリストのみを含みます。</li></ul> |
|ユーザー識別子|  <ul><li>必須。</li><li>適用可能なユーザー識別子をマップします。</li><li>詳細については、[リマーケティングとオーディエンスターゲティング](https://developers.google.com/adwords/api/docs/guides/remarketing)を参照してください。</li><li>必須フィールドは選択したリストタイプによります。以下の通りです：  <ul><li>**連絡先情報** (`CONTACT_INFO`) <ul><li>最小必須：メール、電話番号、またはすべての住所情報。</li><li>メール、電話番号、名前と姓は空白を削除し、小文字にし、SHA-256でエンコードする必要があります。</li><li>マップされた値がプレーンテキストの場合は、オプションセクションで**連絡先情報ハッシュ**チェックボックスをチェックします。</li><li>国コードは2文字のISO 3166 Alpha-2形式に従う必要があります。</li></ul> </li><li>**CRM** (`CRM_ID`) <ul><li>必須</li><li>ユーザーID</li><li>広告主が生成し、ホワイトリストに登録されたクライアントのみがアクセス可能。</li></ul> </li><li>**モバイル広告** (`MOBILE_ADVERTISING_ID`) <ul><li>必須</li><li>モバイルID</li><li>モバイルデバイスID（広告ID/IDFA）。</li></ul> </li></ul> </li></ul> |
|連絡先情報ハッシュ|  <ul><li>オプション</li><li>マップされた連絡先情報がプレーンテキストである場合はチェックします。</li><li>値は自動的にSHA-256でハッシュ化されます。</li></ul> |

### アクション - リマーケティングリストからユーザーを削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|リマーケティングリスト|  <ul><li>ユーザーを削除するリマーケティングユーザーリストを選択します。</li><li>詳細については、[リマーケティングとオーディエンスターゲティング](https://developers.google.com/adwords/api/docs/guides/remarketing)を参照してください。</li><li>利用可能なオプションは、ファーストパーティCRMデータタイプのユーザーリストのみを含みます。</li></ul> |
|ユーザー識別子|  <ul><li>必須。</li><li>適用可能なユーザー識別子をマップします。</li><li>詳細については、[リマーケティングとオーディエンスターゲティング](https://developers.google.com/adwords/api/docs/guides/remarketing)を参照してください。</li><li>必須フィールドは選択したリストタイプによります。以下の通りです：  <ul><li>**連絡先情報** (`CONTACT_INFO`)  <ul><li>最小必須：メール、電話番号、またはすべての住所情報。</li><li>メール、電話番号、名前と姓は空白を削除し、小文字にし、SHA-256でエンコードする必要があります。</li><li>マップされた値がプレーンテキストの場合は、オプションセクションで**連絡先情報ハッシュ**チェックボックスをチェックします。</li><li>国コードは2文字のISO 3166 Alpha-2形式に従う必要があります。</li></ul> </li><li>**CRM** (`CRM_ID`)  <ul><li>必須</li><li>ユーザーID</li><li>広告主が生成し、ホワイトリストに登録されたクライアントのみがアクセス可能。</li></ul> </li><li>**モバイル広告** (`MOBILE_ADVERTISING_ID`)  <ul><li>必須</li><li>モバイルID</li><li>モバイルデバイスID（広告ID/IDFA）。</li></ul> </li></ul> </li></ul> |
|連絡先情報ハッシュ|  <ul><li>オプション</li><li>マップされた連絡先情報がプレーンテキストである場合はチェックします。</li><li>値は自動的にSHA-256でハッシュ化されます。</li></ul> |
