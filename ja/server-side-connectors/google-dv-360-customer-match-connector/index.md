---
title: Google Display & Video 360 カスタマーマッチコネクタ構成ガイド
description: この記事では、Google Display & Video 360 カスタマーマッチコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-dv-360-customer-match-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Google Audience Partner API
* APIバージョン：v2
* APIエンドポイント：`https://audiencepartner.googleapis.com/v2`
* ドキュメント：[Google Audience Partner API: Customer Match audience](https://support.google.com/displayvideo/answer/9539301?hl=ja)

## 要件

このコネクタを構成する前に、Google Display & Video 360アカウントにTealiumをリンクされたアカウントとして追加してください。

詳細については、[Google Display & Video 360: Sharing audience lists from external data management platforms or customer match uploader partners](https://support.google.com/displayvideo/answer/9649053?hl=ja)を参照してください。

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[About Connectors](https://docs.tealium.com/manage-connectors/)を参照してください。


<blockquote>
このコネクタを追加する際には、ベンダーのデータプラットフォームポリシーを受け入れるよう求められます。
</blockquote>


コネクタを追加した後、以下の構成を構成します：

* **Customer ID**：（必須）TealiumにリンクされたあなたのGoogle DV360パートナーID。パートナーIDを見つけるには、Google DV360ダッシュボードの**Partner Settings > Basic Details**にアクセスしてください。
* **Target Product**：（必須）リンクされたアカウントの対象製品。

コネクタの構成が完了したら、**Done**をクリックします。

### カスタマーマッチリストの作成

カスタマーマッチリストを作成するには、**Create Customer Match List**をクリックし、以下の情報を入力します：

| **パラメータ** | **説明** |
| --- | --- |
| List Name | （必須）カスタマーマッチリスト名。 |
| List type | （必須）リストのタイプ。このタイプは、このリストで使用されるユーザー識別情報のタイプに影響します：<ul><li>Contact Info - メンバーは、メールアドレス、電話番号、または物理的住所などの顧客情報からマッチされます。</li><li>Mobile Advertising - メンバーはモバイル広告IDからマッチされます。</li></ul> |
| App ID | Mobile Advertisingリストタイプに必要です。データが収集されたモバイルアプリケーションを一意に識別する文字列。 |
| List Membership Lifespan | （オプション）ユーザーがリストに追加されてからリストに残る日数。数値は`0`から`540`の間でなければなりません。デフォルトの寿命は540日です。 |
| List Description | （オプション）リストの説明。 |

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add to Customer Match List (Data Manager API) | ✓ | ✓ |
| Remove from Customer Match List (Data Manager API) | ✓ | ✓ |
| Add to Customer Match List (Deprecated) | ✓ | ✓ |
| Remove from Customer Match List (Deprecated) | ✓ | ✓ |

### ユーザー識別子

各アクションにはユーザー識別子が必要であり、これらの値は正規化され、SHA-256でハッシュ化される必要があります。マッピングされる各ユーザー識別子値は、以下の要件を満たす必要があります：

* 小文字
* テキストの先頭と末尾から空白をトリム
* SHA-256でハッシュ化

既に正規化されハッシュ化された属性をマッピングするか、コネクタに正規化とハッシュ化をさせます。シナリオに適したマッピングを選択してください。

選択する`User List`タイプによって、ユーザー識別子のタイプが決まります。`User List`タイプは以下のいずれかです：

* `CONTACT_INFO`
* `MOBILE_ADVERTISING_ID`

サポートされているユーザー識別子フィールドは以下の通りです：

|ユーザー識別子フィールド| 説明|
|---| ---|
| `CONTACT_INFO` | <ul><li>ハッシュ化されたメールアドレス、ハッシュ化された電話番号、または住所情報を提供します。</li><li>住所情報を提供する場合、すべての4つのフィールドが必要です：国コード、名、姓、郵便番号。**Address Info**フィールドのいずれかが欠けている場合、コネクタはリクエストから住所オブジェクト全体を削除します。削除後にユーザーデータが残っていない場合、アクションは検証エラーで失敗し、再試行されません。</li><li>**Address Info: Country Code**: ISO 3166-1 alpha-2形式のユーザーの住所の2文字国コードを提供します。</li><li>**Address Info: First Name (already SHA256 hashed)**: 先頭と末尾の空白を削除し、小文字に変換し、SHA-256でハッシュ化された名を提供します。</li><li>**Address Info: First Name (apply SHA256 hash)**: 名をプレーンテキストで提供します。コネクタが値をSHA-256でハッシュ化します。</li><li>**Address Info: Last Name (already SHA256 hashed)**: 先頭と末尾の空白を削除し、小文字に変換し、SHA-256でハッシュ化された姓を提供します。</li><li>**Address Info: Last Name (apply SHA256 hash)**: 姓をプレーンテキストで提供します。コネクタが値をSHA-256でハッシュ化します。</li><li>**Address Info: Postal Code**: ユーザーの住所の郵便番号を提供します。</li><li>**Email Address (already SHA256 hashed)**: 先頭と末尾の空白を削除し、小文字に変換し、SHA-256でハッシュ化されたメールアドレスを提供します。値は64文字の16進数文字を含む有効なSHA-256ヘックス文字列でなければなりません。無効な値はリクエストが送信される前に削除されます。</li><li>**Email Address (apply SHA256 hash)**: メールアドレスをプレーンテキストで提供します。コネクタが値をSHA-256でハッシュ化します。</li><li>**Phone Number (already SHA256 hashed)**: 先頭と末尾の空白を削除し、SHA-256でハッシュ化された電話番号を提供します。値は64文字の16進数文字を含む有効なSHA-256ヘックス文字列でなければなりません。無効な値はリクエストが送信される前に削除されます。有効なユーザー識別子が残っていない場合、アクションは検証エラーで失敗し、再試行されません。</li><li>**Phone Number (apply SHA256 hash)**: 電話番号をプレーンテキストで提供します。コネクタが値をSHA-256でハッシュ化します。</li></ul> |

### Add to Customer Match List (Data Manager API)

#### API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Google Data Manager API
* APIバージョン：v1
* APIエンドポイント：`https://datamanager.googleapis.com`
* ドキュメント：[Google Data Manager API](https://developers.google.com/data-manager/api/reference/rest)

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[Batched Actions](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値が満たされるか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：66,000
* 最古のリクエストからの最大時間：1440分
* リクエストの最大サイズ：50 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| Customer Match List | カスタマーマッチリストを選択します。Tealiumコネクタを通じて作成されたリストのみが利用可能です。カスタマーマッチリストを作成するには、[Create customer match list](#create-customer-match-list)を参照してください。 |
| User Identifier | マッチするユーザー識別子。サポートされているフィールドについては、[User Identifiers](#user-identifiers)を参照してください。 |

##### 同意

**Add Visitor to Customer Match List**アクションを使用する場合、コネクタはデフォルトで`adUserData`および`adPersonalization`の同意に対して`GRANTED`の値を送信します。リストに追加される非同意訪問を防ぐためにオーディエンスロジックを使用してください。**Remove from Customer Match List**アクションを使用して、リストから非同意訪問を削除します。

### Remove from Customer Match List (Data Manager API)

マッピングオプションについては、[Add to Customer Match List (Data Manager API)](#add-to-customer-match-list-data-manager-api)を参照してください。
### 顧客マッチリストへの追加（非推奨）


<blockquote>
このアクションは非推奨であり、将来のリリースで削除される予定です。[顧客マッチリストへの追加（データマネージャーAPI）](#add-to-customer-match-list-data-manager-api)に移行してください。
</blockquote>



<blockquote>
TealiumはGoogle DV 360から直接リスト統計を取得するため、このコネクタと[Google DV 360 顧客マッチコネクタの洞察](https://docs.tealium.com/connector-insights-google-dv360-customer-match/)でのマッチ数とコネクタリクエストの総量に差異が生じる場合があります。
</blockquote>


#### API情報

このコネクタは以下のベンダーAPIを使用しています：

* API名：Google Ads API
* APIバージョン：v18
* APIエンドポイント：`https://googleads.googleapis.com/`
* ドキュメント：[Google Ads API](https://developers.google.com/google-ads/api/docs/start)

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。以下のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストはキューに入れられます：

* 最大リクエスト数：100,000
* 最古のリクエストからの最大時間：1440分
* リクエストの最大サイズ：50 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 顧客マッチリスト | 顧客マッチリストを選択します。Tealiumコネクタを通じて作成されたリストのみが利用可能です。顧客マッチリストを作成するには、[顧客マッチリストの作成](#create-customer-match-list)を参照してください。 |

##### 同意

**顧客マッチリストへの訪問追加** アクションを使用する際、コネクタはデフォルトで `adUserData` および `adPersonalization` の同意に `GRANTED` の値を送信します。同意していない訪問がリストに追加されないようにオーディエンスロジックを使用してください。同意していない訪問をリストから削除するには、**顧客マッチリストからの削除** アクションを使用してください。

### 顧客マッチリストからの削除（非推奨）


<blockquote>
このアクションは非推奨であり、将来のリリースで削除される予定です。[顧客マッチリストからの削除（データマネージャーAPI）](#remove-from-customer-match-list-data-manager-api)に移行してください。
</blockquote>


#### API情報

このコネクタは以下のベンダーAPIを使用しています：

* API名：Google Ads API
* APIバージョン：v18
* APIエンドポイント：`https://googleads.googleapis.com/`
* ドキュメント：[Google Ads API](https://developers.google.com/google-ads/api/docs/start)

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。以下のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストはキューに入れられます：

* 最大リクエスト数：100,000
* 最古のリクエストからの最大時間：1440分
* リクエストの最大サイズ：50 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 顧客マッチリスト | 顧客マッチリストを選択します。Tealiumコネクタを通じて作成されたリストのみが利用可能です。 |