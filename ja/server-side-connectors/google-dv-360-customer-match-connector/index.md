---
title: Google Display & Video 360 カスタマーマッチコネクタ構成ガイド
description: この記事では、Google Display & Video 360 カスタマーマッチコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-dv-360-customer-match-connector/
---
## API 情報

このコネクタは以下のベンダーAPIを使用します：

* API 名: Google Audience Partner API
* API バージョン: v2
* API エンドポイント: `https://audiencepartner.googleapis.com/v2`
* ドキュメント: [Google Audience Partner API: Customer Match audience](https://support.google.com/displayvideo/answer/9539301?hl=ja)

## 要件

このコネクタを構成する前に、Google Display & Video 360 アカウントにTealiumをリンクされたアカウントとして追加してください。

詳細については、[Google Display & Video 360: Sharing audience lists from external data management platforms or customer match uploader partners](https://support.google.com/displayvideo/answer/9649053?hl=ja)を参照してください。

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[About Connectors](https://docs.tealium.com/manage-connectors/)を参照してください。


<blockquote>
このコネクタを追加すると、ベンダーのデータプラットフォームポリシーを受け入れるように求められます。
</blockquote>


コネクタを追加した後、以下の構成を構成します：

* **Customer ID**: (必須) TealiumにリンクされたあなたのGoogle DV360パートナーID。Google DV360ダッシュボードからパートナーIDを見つけるには、**Partner Settings > Basic Details**に進んでください。
* **Target Product**: (必須) リンクされたアカウントのターゲット製品。

コネクタの構成が完了したら、**Done**をクリックします。

### カスタマーマッチリストの作成

カスタマーマッチリストを作成するには、**Create Customer Match List**をクリックし、以下の情報を入力します：

| **パラメータ** | **説明** |
| --- | --- |
| List Name | (必須) カスタマーマッチリスト名。 |
| List Type | (必須) リストタイプ。このリストで使用されるユーザー識別情報のタイプに影響します：<ul><li>Contact Info - メンバーは顧客情報（メールアドレス、電話番号、または物理的住所）からマッチされます。</li><li>Mobile Advertising - メンバーはモバイル広告IDからマッチされます。</li></ul> |
| App ID | Mobile Advertisingリストタイプに必要です。データが収集されたモバイルアプリケーションを一意に識別する文字列。 |
| List Membership Lifespan | (オプション) ユーザーがリストに最後に追加されてからリストに残る日数。数値は `0` から `540` の間でなければなりません。デフォルトの寿命は540日です。 |
| List Description | (オプション) リストの説明。 |

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add to Customer Match List (multiple identifiers) | ✓ | ✓ |
| Remove from Customer Match List (multiple identifiers) | ✓ | ✓ |
| Add to Customer Match List (Deprecated) | ✓ | ✓ |
| Remove from Customer Match List (Deprecated) | ✓ | ✓ |

### ユーザー識別子

各アクションにはユーザー識別子が必要であり、これらの値は正規化され、SHA-256でハッシュ化される必要があります。マッピングされる各ユーザー識別子値は、以下の要件を満たす必要があります：

* 小文字
* テキストの先頭と末尾から空白をトリム
* SHA-256でハッシュ化

既に正規化されハッシュ化された属性をマッピングするか、コネクタに正規化とハッシュ化をさせます。シナリオに適したマッピングを選択してください。

選択する `User List` タイプはユーザー識別子のタイプを決定します。`User List` タイプは以下のいずれかになります：

* `CONTACT_INFO`
* `MOBILE_ADVERTISING_ID`

以下のユーザー識別子フィールドがサポートされています：

|ユーザー識別子フィールド| 説明|
|---| ---|
| `CONTACT_INFO` |  <ul><li>ハッシュ化されたメール、ハッシュ化された電話番号、または住所情報を提供します。</li><li>**住所情報: 国コード** - ISO 3166-1 alpha-2形式のユーザーの住所の2文字国コード。</li><li>**住所情報: 名（既にSHA256ハッシュ化済み）** - 空白をトリムし、小文字にしてSHA256でハッシュ化された名を提供します。</li><li>**住所情報: 名（SHA256ハッシュを適用）** - プレーンテキストの名を提供します。コネクタはこの値をSHA256ハッシュでハッシュ化します。</li><li>**住所情報: 姓（既にSHA256ハッシュ化済み）** - 空白をトリムし、小文字にしてSHA256でハッシュ化された姓を提供します。</li><li>**住所情報: 姓（SHA256ハッシュを適用）** - プレーンテキストの姓を提供します。コネクタはこの値をSHA256ハッシュでハッシュ化します。</li><li>**住所情報: 郵便番号** - ユーザーの住所の郵便番号。</li><li>**メールアドレス（既にSHA256ハッシュ化済み）** - 空白をトリムし、小文字にしてSHA256でハッシュ化されたメールアドレスを提供します。</li><li>**メールアドレス（SHA256ハッシュを適用）** - プレーンテキストのメールアドレスを提供します。コネクタはこの値をSHA256ハッシュでハッシュ化します。</li><li>**電話番号（既にSHA256ハッシュ化済み）** - 空白をトリムし、SHA256でハッシュ化された電話番号を提供します。</li><li>**電話番号（SHA256ハッシュを適用）** - プレーンテキストの電話番号を提供します。コネクタはこの値をSHA256ハッシュでハッシュ化します。</li></ul> |
|`MOBILE_ADVERTISING_ID`|  <ul><li>**モバイルID** (必須) - モバイルデバイスID（広告ID/IDFA）。</li></ul> |

### カスタマーマッチリストに追加 (複数識別子)

#### API 情報

このコネクタは以下のベンダーAPIを使用します：

* API 名: Google Data Manager API
* API バージョン: v1
* API エンドポイント: `https://datamanager.googleapis.com`
* ドキュメント: [Google Data Manager API](https://developers.google.com/data-manager/api/reference/rest)

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[Batched Actions](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数: 66,000
* 最古のリクエストからの最大時間: 1440分
* リクエストの最大サイズ: 50 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| Customer Match List | カスタマーマッチリストを選択します。Tealiumコネクタを通じて作成されたリストのみが利用可能です。カスタマーマッチリストを作成するには、[Create customer match list](#create-customer-match-list)を参照してください。 |
| User Identifier | マッチするユーザー識別子。サポートされているフィールドについては、[User Identifiers](#user-identifiers)を参照してください。 |

##### 同意

**Add Visitor to Customer Match List** アクションを使用する際、コネクタはデフォルトで `adUserData` および `adPersonalization` の同意に `GRANTED` の値を送信します。リストに追加されない非同意訪問のためにオーディエンスロジックを使用してください。非同意訪問をリストから削除するには、**Remove from Customer Match List** アクションを使用してください。

### カスタマーマッチリストから削除 (複数識別子)

マッピングオプションについては、[Add to Customer Match List (multiple identifiers)](#add-to-customer-match-list-multiple-identifiers)を参照してください。

### カスタマーマッチリストに追加 (非推奨)


<blockquote>
TealiumはGoogle DV 360から直接リスト統計を取得し、このコネクタと[Google DV 360 Customer Match connector insight](https://docs.tealium.com/connector-insights-google-dv360-customer-match/)のコネクタリクエストの総量との間に差異が生じることがあります。
</blockquote>


#### API 情報

このコネクタは以下のベンダーAPIを使用します：

* API 名: Google Ads API
* API バージョン: v18
* API エンドポイント: `https://googleads.googleapis.com/`
* ドキュメント: [Google Ads API](https://developers.google.com/google-ads/api/docs/start)

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[Batched Actions](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値が達成されるか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数: 100,000
* 最古のリクエストからの最大時間: 1440分
* リクエストの最大サイズ: 50 MB
#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| カスタマーマッチリスト | カスタマーマッチリストを選択します。Tealiumコネクタを通じて作成されたリストのみが利用可能です。カスタマーマッチリストを作成するには、[カスタマーマッチリストの作成](#create-customer-match-list)を参照してください。 |

##### 同意

**Add Visitor to Customer Match List** アクションを使用する際、コネクタはデフォルトで `adUserData` と `adPersonalization` の同意に対して `GRANTED` の値を送信します。同意していない訪問がリストに追加されないようにオーディエンスロジックを使用してください。同意していない訪問をリストから削除するには、**Remove from Customer Match List** アクションを使用します。

### カスタマーマッチリストから削除（非推奨）

#### API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Google Ads API
* APIバージョン：v18
* APIエンドポイント：`https://googleads.googleapis.com/`
* ドキュメント：[Google Ads API](https://developers.google.com/google-ads/api/docs/start)

#### バッチ制限

このアクションはバッチリクエストを使用して、ベンダーへの大量データ転送をサポートします。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：100,000
* 最古のリクエストからの最大時間：1440分
* リクエストの最大サイズ：50 MB

#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| カスタマーマッチリスト | カスタマーマッチリストを選択します。Tealiumコネクタを通じて作成されたリストのみが利用可能です。 |