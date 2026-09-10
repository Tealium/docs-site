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

このコネクタを構成する前に、Google Display & Video 360アカウントでTealiumをリンクアカウントとして追加してください。

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
| List type | （必須）リストタイプ。このタイプは、このリストで使用されるユーザー識別情報のタイプに影響します：<ul><li>Contact Info - メンバーは顧客情報（メールアドレス、電話番号、または物理的な住所）からマッチされます。</li><li>Mobile Advertising - メンバーはモバイル広告IDからマッチされます。</li></ul> |
| App ID | Mobile Advertisingリストタイプに必要。データが収集されたモバイルアプリケーションを一意に識別する文字列。 |
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

各アクションにはユーザー識別子が必要であり、これらの値は正規化され、SHA-256でハッシュ化する必要があります。マッピングする各ユーザー識別子値は、以下の要件を満たす必要があります：

* 小文字
* テキストの先頭と末尾から空白をトリム
* SHA-256でハッシュ化

既に正規化されハッシュ化された属性をマッピングするか、コネクタに正規化とハッシュ化を許可します。シナリオに適したマッピングを選択してください。

選択する`User List`タイプはユーザー識別子のタイプを決定します。`User List`タイプは以下のいずれかです：

* `CONTACT_INFO`
* `MOBILE_ADVERTISING_ID`

サポートされているユーザー識別子フィールドは以下の通りです：

|ユーザー識別子フィールド| 説明|
|---| ---|
| `CONTACT_INFO` |  <ul><li>ハッシュ化されたメール、ハッシュ化された電話番号、または住所情報を提供します。</li><li>住所情報を提供する場合、すべての4つのフィールドが必要です：国コード、名、姓、郵便番号。住所情報フィールドのいずれかが欠けている場合、コネクタはリクエストから住所オブジェクト全体を削除します。削除後にユーザーデータが残っていない場合、アクションは検証エラーで失敗し、再試行されません。</li><li>**住所情報：国コード** - ISO 3166-1 alpha-2形式のユーザーの住所の2文字国コード。</li><li>**住所情報：名（既にSHA256ハッシュ化済み）** - 空白をトリムし、小文字にしてSHA256でハッシュ化された名を提供します。</li><li>**住所情報：名（SHA256ハッシュを適用）** - プレーンテキストの名を提供します。コネクタはこの値をSHA256ハッシュでハッシュ化します。</li><li>**住所情報：姓（既にSHA256ハッシュ化済み）** - 空白をトリムし、小文字にしてSHA256でハッシュ化された姓を提供します。</li><li>**住所情報：姓（SHA256ハッシュを適用）** - プレーンテキストの姓を提供します。コネクタはこの値をSHA256ハッシュでハッシュ化します。</li><li>**住所情報：郵便番号** - ユーザーの住所の郵便番号。</li><li>**メールアドレス（既にSHA256ハッシュ化済み）** - 空白をトリムし、小文字にしてSHA256でハッシュ化されたメールアドレスを提供します。</li><li>**メールアドレス（SHA256ハッシュを適用）** - プレーンテキストのメールアドレスを提供します。コネクタはこの値をSHA256ハッシュでハッシュ化します。</li><li>**電話番号（既にSHA256ハッシュ化済み）** - 空白をトリムし、SHA256でハッシュ化された電話番号を提供します。</li><li>**電話番号（SHA256ハッシュを適用）** - プレーンテキストの電話番号を提供します。コネクタはこの値をSHA256ハッシュでハッシュ化します。</li></ul> |
|`MOBILE_ADVERTISING_ID`|  <ul><li>**モバイルID**（必須） - モバイルデバイスID（広告ID/IDFA）。</li></ul> |

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

**Add Visitor to Customer Match List**アクションを使用する場合、コネクタはデフォルトで`adUserData`および`adPersonalization`の同意に`GRANTED`の値を送信します。リストに追加されないように非同意の訪問に対するオーディエンスロジックを使用してください。リストから非同意の訪問を削除するには、**Remove from Customer Match List**アクションを使用してください。

### Remove from Customer Match List (Data Manager API)

マッピングオプションについては、[Add to Customer Match List (Data Manager API)](#add-to-customer-match-list-data-manager-api)を参照してください。

### Add to Customer Match List (Deprecated)


<blockquote>
このアクションは非推奨であり、将来のリリースで削除されます。[Add to Customer Match List (Data Manager API)](#add-to-customer-match-list-data-manager-api)に移行してください。
</blockquote>



<blockquote>
TealiumはGoogle DV 360から直接リスト統計を取得するため、このコネクタと[Google DV 360 Customer Match connector insight](https://docs.tealium.com/connector-insights-google-dv360-customer-match/)のマッチ数とコネクタリクエストの総量に差が生じる場合があります。
</blockquote>


#### API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Google Ads API
* APIバージョン：v18
* APIエンドポイント：`https://googleads.googleapis.com/`
* ドキュメント：[Google Ads API](https://developers.google.com/google-ads/api/docs/start)
#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* リクエストの最大数：100,000
* 最古のリクエストからの最大時間：1440分
* リクエストの最大サイズ：50 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| カスタマーマッチリスト | カスタマーマッチリストを選択します。Tealiumコネクタを通じて作成されたリストのみが利用可能です。カスタマーマッチリストを作成するには、[カスタマーマッチリストの作成](#create-customer-match-list)を参照してください。 |

##### 同意

**カスタマーマッチリストへの訪問追加** アクションを使用する際、コネクタはデフォルトで `adUserData` と `adPersonalization` の同意に対して `GRANTED` の値を送信します。同意していない訪問がリストに追加されないようにオーディエンスロジックを使用してください。同意していない訪問をリストから削除するには、**カスタマーマッチリストから削除** アクションを使用してください。

### カスタマーマッチリストからの削除（非推奨）


<blockquote>
このアクションは非推奨であり、将来のリリースで削除されます。[カスタマーマッチリストからの削除（データマネージャAPI）](#remove-from-customer-match-list-data-manager-api)に移行してください。
</blockquote>


#### API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Google Ads API
* APIバージョン：v18
* APIエンドポイント：`https://googleads.googleapis.com/`
* ドキュメント：[Google Ads API](https://developers.google.com/google-ads/api/docs/start)

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* リクエストの最大数：100,000
* 最古のリクエストからの最大時間：1440分
* リクエストの最大サイズ：50 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| カスタマーマッチリスト | カスタマーマッチリストを選択します。Tealiumコネクタを通じて作成されたリストのみが利用可能です。 |