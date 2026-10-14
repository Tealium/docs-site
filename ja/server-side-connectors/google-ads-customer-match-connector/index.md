---
title: Google Ads カスタマーマッチ（Tealium提供の資格情報）コネクタ構成ガイド
description: この記事では、Tealiumが提供する資格情報を使用するGoogle Adsカスタマーマッチコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-ads-customer-match-connector/
---
## Google Data Manager API アクションへの移行

以下のアクションは古いGoogle Ads APIを使用しています：

* リマーケティングリストへのユーザー追加
* リマーケティングリストからのユーザー削除

以下の置き換えアクションを使用してください。これらはGoogle Data Manager APIに基づいています：

* リストへのユーザー追加（Data Manager API）
* リストからのユーザー削除（Data Manager API）

詳細については、[Google Data Manager API移行ガイド](https://docs.tealium.com/google-data-manager-api-migration-guide/)を参照してください。

## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタの追加方法については、[コネクタについて](https://docs.tealium.com/about-connectors/)の記事を参照してください。


<blockquote>
このコネクタを追加する際には、ベンダーのデータプラットフォームポリシーを受け入れるよう求められます。
</blockquote>


コネクタを追加した後、以下の構成を構成します：

* **Customer ID**：（必須）管理する広告アカウントの顧客IDを提供してください。
* **Manager Customer ID**：（オプション）クライアントの顧客にアクセスする場合、Manager Customer IDを構成し、広告アカウントへの完全なアクセス権を持っている必要があります。

### ユーザーリストの作成

ユーザーリストを作成するには、**Create User List**をクリックし、以下の情報を入力します：

| **パラメータ** | **説明** |
| --- | --- |
| リスト名 | （必須）ユーザーリストの名前。 |
| リストタイプ | （必須）リストのタイプ。これは、このリストで使用されるユーザー識別情報のタイプに影響します：<ul><li>`CONTACT_INFO`：顧客情報（メールアドレス、電話番号、物理的住所など）からユーザーを照合します。</li><li>`CRM_ID`：広告主が生成し割り当てたユーザーIDからユーザーを照合します。</li><li>`MOBILE_ADVERTISING_ID`：モバイルデバイスID（広告ID/IDFA）からユーザーを照合します。</li></ul> |
| アプリID | モバイル広告リストタイプに必要です。データがGoogle Ads APIに送信されるモバイルアプリケーションを一意に識別する文字列。 |
| リストメンバーシップの寿命 | （オプション）ユーザーがリストに最後に追加されてからリストに残る日数。数値は`0`から`540`の間でなければなりません。デフォルトの寿命は540日です。 |
| リストの説明 | （オプション）リストの説明。 |

## Google AdsとTealiumのリンク

Google Data Manager APIアクションは、Google AdsとTealium間の製品リンクを必要とします。リンクはTealiumまたはGoogle Adsのいずれかで作成できます。どちらのオプションも新しいData Manager APIアクションと、レガシーGoogle Ads APIアクションから移行されたアクションをサポートします。

### オプション1：Tealiumで製品リンクを作成する

このオプションを使用して、コネクタ構成からリンキングプロセスを完了します。

1. TealiumでGoogle Adsカスタマーマッチコネクタを開きます。
1. 新しいコネクタの場合はGoogleで認証します。既存のコネクタの場合は、Google Data Manager APIスコープを含む資格情報で再認証します。
1. コネクタ構成で**Link Customer ID to Tealium**セクションを見つけます。
1. Customer Matchユーザーリストを所有するGoogle Adsの顧客IDを入力します。
1. **Create Product Link**をクリックし、確認メッセージを待ちます。
1. Data Manager APIアクションを構成または移行し、適切なユーザーリストを選択し、リストキータイプに一致する識別子をマッピングします。

アクションが**Customer ID Override**を使用する場合、アクションによって使用されるユーザーリストを所有する各顧客アカウントに対して製品リンクを作成します。

### オプション2：Google Adsで製品リンクを作成する

このオプションを使用して、TealiumでGoogle OAuthフローを使用せずにGoogle Adsで製品リンクを作成します。

1. Google Adsにサインインします。
1. **ツール > データマネージャ**に移動します。
1. **+ Connect product**をクリックします。
1. 利用可能な製品からTealiumを選択します。
1. 必要に応じて、使用ケースとして**Audiences**を選択します。
1. 顧客データポリシーを確認し、受け入れた後、リンクを完了します。
1. Tealiumで、リンクされたGoogle Adsの顧客アカウントと適切なユーザーリストを使用してData Manager APIアクションを構成または移行します。

リンク後も、アクションに必要な顧客IDとユーザーリストの構成を提供してコネクタアクションを構成する必要があります。

### マネージャーアカウントのリンク

Google Adsのマネージャーアカウントの代わりに、各顧客アカウントを個別にリンクすることなく、マネージャーアカウントの製品リンクを作成することができます。マネージャーアカウントのリンクは、そのマネージャーアカウントとその下のクライアントアカウントに使用できます。

アクションを構成する際には、オーディエンス更新を受け取る特定のGoogle Adsアカウントの顧客IDを使用します。マネージャーアカウントのリンクは、リンクされたマネージャーアカウントの階層外のアカウント（親マネージャーアカウントやリンクされていない子アカウントなど）には拡張されません。

ターゲットのGoogle Adsアカウントは必要な権限を持っている必要があり、ターゲットのユーザーリストはアクションに使用される顧客アカウントに属している必要があります。

## アクション

| アクション名 | AudienceStream | EventStream |
| ------------| :------------: | :---------: |
| リストへのユーザー追加（Data Manager API） | ✓ | ✓ |
| リストからのユーザー削除（Data Manager API） | ✓ | ✓ |
| リマーケティングリストへのユーザー追加（非推奨）| ✓ | ✓ |
| リマーケティングリストからのユーザー削除（非推奨）| ✓ | ✓ |
### ユーザー識別子

各アクションにはユーザー識別子が必要です。ベンダーはこれらの値が正規化され、SHA-256を使用してハッシュ化されることを要求しています。各マップされたユーザー識別子値は、以下の要件を満たすことが期待されています：

* 小文字
* テキストの先頭と末尾からの空白のトリム
* SHA-256でハッシュ化

すでに正規化されハッシュ化された属性をマッピングすることも、コネクタに正規化とハッシュ化を任せることもできます。シナリオに適したマッピングを選択してください。

必要なユーザー識別子は、選択されたユーザーリストのタイプに基づいています。ユーザーリストのタイプは以下のいずれかになります：

* Google Ads API:
  * `CONTACT_INFO`
  * `CRM_ID`
  * `MOBILE_ADVERTISING_ID`
* Google Data Manager API:
  * `CONTACT_ID`
  * `MOBILE_ID`
  * `USER_ID`

以下のユーザー識別子フィールドがサポートされています：

| ユーザー識別子フィールド | 説明 |
|---| ---|
| `CONTACT_INFO` (Google Ads API)|  ハッシュ化されたメール、ハッシュ化された電話番号、または住所情報を提供します。このユーザーデータタイプには、以下にリストされているすべての住所情報フィールドが必要です。<ul><li>**住所情報: 国コード**: ユーザーの住所の2文字の国コード、ISO 3166-1 alpha-2形式。</li><li>**住所情報: 名 (既にSHA256ハッシュ化)**: 空白トリムされ、小文字化され、SHA256ハッシュ化された名を提供します。</li><li>**住所情報: 名 (SHA256ハッシュを適用)**: プレーンテキストの名を提供し、コネクタがこの値をSHA256ハッシュでハッシュ化します。</li><li>**住所情報: 姓 (既にSHA256ハッシュ化)**: 空白トリムされ、小文字化され、SHA256ハッシュ化された姓を提供します。</li><li>**住所情報: 姓 (SHA256ハッシュを適用)**: プレーンテキストの姓を提供し、コネクタがこの値をSHA256ハッシュでハッシュ化します。</li><li>**住所情報: 郵便番号**: ユーザーの住所の郵便番号を提供します。</li><li>**メールアドレス (既にSHA256ハッシュ化)**: 空白トリムされ、小文字化され、SHA256ハッシュ化されたメールアドレスまたはメールアドレスの配列を提供します。</li><li>**メールアドレス (SHA256ハッシュを適用)**: プレーンテキストのメールアドレスまたはメールアドレスの配列を提供し、コネクタがこれらの値をSHA256ハッシュでハッシュ化します。</li><li>**電話番号 (既にSHA256ハッシュ化)**: 空白トリムされ、SHA256ハッシュ化された電話番号または電話番号の配列を提供します。</li><li>**電話番号 (SHA256ハッシュを適用)**: プレーンテキストの電話番号または電話番号の配列を提供し、コネクタが値をSHA256ハッシュでハッシュ化します。</li></ul> |
|`CRM_ID` (Google Ads API)|  <ul><li>**ユーザーID**: (必須) 顧客マッチアップロード用に広告主が割り当てたユーザーID。</li></ul> |
|`MOBILE_ADVERTISING_ID` (Google Ads API)|  <ul><li>**モバイルID**: (必須) モバイルデバイスID (広告ID/IDFA)。</li></ul> |
| `CONTACT_ID` (Data Manager API) | **連絡先情報**: メールアドレス、電話番号、および住所。事前にハッシュ化されたメールおよび電話の値は、64の16進数文字を含む有効なSHA-256 16進数文字列である必要があります。コネクタは無効な値を削除してからリクエストを送信します。住所情報には、国コード、名、姓、郵便番号の4つのフィールドが必要です。いずれかの住所フィールドが欠けている場合、コネクタは住所オブジェクト全体を削除します。有効なユーザー識別子が検証後に残っていない場合、アクションは検証エラーで失敗し、再試行されません。 |
|`MOBILE_ID` (Data Manager API)|  **モバイルID**: モバイルデバイスID。 |
|`USER_ID` (Data Manager API)|  **ユーザーID**: 第一者識別子。 |

### リストへのユーザー追加 (Data Manager API)

#### API情報

このコネクタは以下のベンダーAPIを使用します：

* API名: Google Data Manager API
* APIバージョン: v1
* APIエンドポイント: `https://datamanager.googleapis.com`
* ドキュメント: [Google Data Manager API](https://developers.google.com/data-manager/api/reference/rest)

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。イベントの順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストはキューに入れられます：

* 最大リクエスト数: 10,000
* 最古のリクエストからの最大時間: 60分
* リクエストの最大サイズ: 40 MB

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| ユーザーリスト | Data Manager APIからユーザーリストを選択します。詳細については、[Data Manager API: Customer match overview](https://developers.google.com/data-manager/api/devguides/audiences/google-ads/customer-match)を参照してください。 |

#### ユーザー識別子

| パラメータ | 説明 |
| --- | --- |
| Customer ID Override | (オプション) コネクタ構成のCustomer IDを上書きするCustomer IDを提供します。このオプションを使用する場合、User List ID Overrideも使用する必要があります。 |
| User List ID Override | (オプション) 必要セクションのユーザーリストを上書きするUser List IDを提供します。このフィールドを使用すると、イベント属性を使用してUser List IDを入力できます。このフィールドは、Customer ID Overrideを使用する場合に必要です。値はリストIDでなければなりません。例：`9310271231`。 |

#### IPデータ

| パラメータ | 説明 |
| --- | --- |
| IPアドレス | 顧客とのやり取り中にキャプチャされたIPアドレス。 |
| Observe Start Time | セッション中のIPアドレスからの最初のインタラクションの時間。 |
| Observe End Time | セッション中のIPアドレスからの最後のインタラクションの時間。 |

### リストからユーザーを削除 (Data Manager API)

マッピングオプションについては、[リストへのユーザー追加 (Data Manager API)](#add-user-to-list-data-manager-api)を参照してください。

### リマーケティングリストへのユーザー追加 (非推奨)


<blockquote>
このアクションは非推奨であり、将来のリリースで削除されます。[リストへのユーザー追加 (Data Manager API)](#add-user-to-list-data-manager-api)に移行して、コネクタを再認証し、[Google AdsとTealiumをリンクする](#link-google-ads-to-tealium)ための手順を実行してください。
</blockquote>


#### バッチ制限

このコネクタアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用することができます。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかの閾値に達するか、プロファイルが公開されるまでリクエストはキューに入れられます：

* 最大リクエスト数: 33,000
* 最古のリクエストからの最大時間: 60分
* リクエストの最大サイズ: 40 MB

#### API情報

このコネクタは以下のベンダーAPIを使用します：

* API名: Google Ads API
* APIバージョン: v24
* APIエンドポイント: `https://googleads.googleapis.com/`
* ドキュメント: [Google Ads API](https://developers.google.com/google-ads/api/docs/start)

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| リマーケティングリスト | リマーケティングユーザーリストを選択します。詳細については、[Google Ads: Remarketing and Audience Targeting](https://developers.google.com/google-ads/api/docs/remarketing/overview)を参照してください。利用可能なオプションには、第一者CRMデータタイプのユーザーリストのみが含まれます。ユーザーリストを作成するには、[Create user list](#create-user-list)を参照してください。|
| Customer ID Override | (オプション) コネクタ構成のCustomer IDを上書きするCustomer IDを提供します。このオプションを使用する場合、**User List ID Override**も入力する必要があります。 |
| Manager Customer ID Override | (オプション) **Customer ID Override**を使用してクライアントの顧客にアクセスする場合、Manager Customer IDを提供します。 |
| User List ID Override | (オプション) ユーザーリストを上書きするためのユーザーリストリソース名（リストIDとタイプ）を提供します。このフィールドを使用すると、EventStream変数を使用してユーザーリストIDを入力できます。このフィールドは、**Customer ID Override**を使用する場合に必要です。値は次の形式でなければなりません：`ID:TYPE`、例えば `123456:CONTACT_INFO`。 |

#### 同意

**リマーケティングリストへのユーザー追加**アクションを使用する場合、コネクタは`adUserData`および`adPersonalization`パラメータに対して`GRANTED`の値を送信します。リストに追加されないようにするために、訪問のプロファイル同意状態をチェックするルールを持つオーディエンスを作成します。その後、**リマーケティングリストから削除**アクションを使用して、同意を与えていない訪問をリストから削除します。
### リマーケティングリストからユーザーを削除する（非推奨）


<blockquote>
このアクションは非推奨であり、将来のリリースで削除される予定です。[リストからユーザーを削除する（データマネージャーAPI）](#remove-user-from-list-data-manager-api)に移行してください。置き換えアクションを使用するには、コネクタを再認証し、[Google AdsをTealiumにリンクする](#link-google-ads-to-tealium)必要があります。
</blockquote>


マッピングオプションについては、[リマーケティングリストにユーザーを追加する](#add-user-to-remarketing-list-deprecated)を参照してください。