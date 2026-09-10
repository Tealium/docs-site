---
title: Brazeコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでBrazeコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/braze-connector/
---
## 同意カテゴリ

* アナリティクス
* モバイル
* パーソナライゼーション

## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIエンドポイント**  
（必須）アカウントがプロビジョニングされているインスタンスのAPIエンドポイントを選択します。  
詳細については、[Braze APIエンドポイント](https://www.braze.com/docs/developer_guide/rest_api/basics/#endpoints)を参照してください。
* **APIキー**  
（必須）`users.track`および`users.delete`の権限が有効になっているAPIキーを提供します。  
詳細については、[Braze App Group REST APIキー](https://www.braze.com/docs/api/basics/?redirected=true#app-group-rest-api-keys)を参照してください。

追加情報については、Brazeドキュメント[Braze Technology Partners: Tealium](https://www.braze.com/docs/partners/data_and_infrastructure_agility/customer_data_platform/tealium/)を参照してください。

## アクション

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。


<blockquote>
**ユーザーを追跡**アクションは、AudienceStreamとEventStreamの両方で同じ機能を含んでいます。ベストプラクティスとして、AudienceStreamアクションのユーザー属性マッピングを構成し、EventStreamアクションのイベントと購入マッピングを構成します。
</blockquote>


| **アクション名**                                   | **AudienceStream** | **EventStream** |
|:--------------------------------------------------|:-------------------|:----------------|
| ユーザーを追跡（バッチ）                                | ✓                  | ✓               |
| ユーザーを追跡（非バッチ）                            | ✓                  | ✓               |
| ユーザーを削除（非バッチ）                            | ✓                  | ✓               |
| ユーザーのサブスクリプショングループステータスを更新（非バッチ） | ✓                  | ✗               |
| 複数のサブスクリプショングループでユーザーのサブスクリプショングループステータスを更新（非バッチ） | ✓ | ✗ |
| キャンペーンメッセージを送信                             | ✓                  | ✓               |
| キャンバスメッセージを送信                               | ✓                  | ✓               |
| トランザクショナルメールを送信                          | ✓                  | ✓               |
| ユーザーを特定                                     | ✓                  | ✓               |

### ユーザーを追跡（バッチ/非バッチ）

できるだけ多くのIDパラメータをマッピングすることをお勧めします。アクションが複数のIDでトリガーされた場合、以下の優先順位に基づいて最初の空白でない値が選択されます：

* 外部ID
* Braze ID
* エイリアス名/エイリアスラベル

詳細については、[Braze API: ユーザー追跡](https://www.braze.com/docs/api/endpoints/user_data/post_user_track/)を参照してください。

#### バッチ対非バッチ  

* **バッチ**: 大規模なユーザープロファイルのバックフィルや同期に使用します。
* **非バッチ**: リアルタイムのユースケースに使用します。


<blockquote>
ピーク時のトラフィック状況では、Brazeは非バッチリクエストをバッチリクエストより優先します。
</blockquote>


#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：75
* 最古のリクエストからの最大時間：60分
* リクエストの最大サイズ：1 MB

#### ユーザーID

| **パラメータ**    | **説明**                                                                       |
|:-----------------|:--------------------------------------------------------------------------------------|
| 外部ID      | ユーザーの外部ID。                                                              |
| Braze ID         | ユーザーのBraze ID。                                                                 |
| ユーザーエイリアス名  | ユーザーのエイリアス名。`Alias Name`と`Alias Label`の両方を構成する必要があります。  |
| ユーザーエイリアスラベル | ユーザーのエイリアスラベル。`Alias Name`と`Alias Label`の両方を構成する必要があります。 |
| 顧客のメールアドレス | 顧客のメールアドレス。 |
| 顧客の電話番号 | 顧客の電話番号。 |

#### ユーザー属性

Brazeのベストプラクティスに従い、変更されたユーザー属性のみを送信し、変更されていない属性の送信を避けることをお勧めします。変更されていない属性の送信を避けるために、訪問と訪問属性のエンリッチメントと、属性が変更されたときに認識するルールを使用します。詳細については、[エンリッチメントルール](https://docs.tealium.com/about-enrichments/)を参照してください。


<blockquote>
空の値は`null`に変換され、Brazeユーザープロファイルから削除されます。
</blockquote>


| **パラメータ** | **説明** |
|:--------------|:----------------|
| 国ホーム                      | ユーザーの国。|
| 現在の位置 - 緯度  | ユーザーの追跡のための現在の緯度。|
| 現在の位置 - 経度 | ユーザーの現在の経度。|
| 最初のセッションの日付        | ユーザーの最初のセッションの日付。|
| 最後のセッションの日付         | ユーザーの最後のセッションの日付。|
| 生年月日                | ユーザーの生年月日。|
| メールアドレス                | ユーザーのメールアドレス。|
| メール購読ステータス    | ユーザーのメール購読ステータス。|
| Facebook                     | `id`（文字列）、`likes`（文字列の配列）、`num_friends`（整数）を含むハッシュ。|
| 名前                   | ユーザーの名前。|
| 性別                       | ユーザーの性別。`M`、`F`、`O`（その他）、`N`（該当なし）、`P`（答えたくない）、またはnil（不明）。|
| 自宅の都市                    | ユーザーの自宅の都市。|
| 画像URL                    | ユーザープロファイルに関連付けられる画像のURL。|
| 言語                     | ISO 639-1形式でのユーザーの言語構成。詳細については、[Braze: 受け入れられる言語コードのリスト](https://www.braze.com/docs/user_guide/data_and_analytics/user_data_collection/language_codes/)を参照してください。|
| 姓                    | ユーザーの姓。|
| スパムとしてマークされたメールの日付      | ユーザーのメールがスパムとしてマークされた日付。ISO 8601形式または`yyyy-MM-dd’T’HH:mm:ss:SSSZ`形式で表示されます。|
| 電話番号                 | ユーザーの電話番号。|
| プッシュ購読ステータス     | `opt_in`（プッシュメッセージを受信するために明示的に登録された）、`unsubscribed`（プッシュメッセージの受信を明示的に拒否した）、または`subscribed`（登録も拒否もしていない）に構成します。|
| プッシュトークンID配列         | プッシュトークン移行に使用するアプリIDの配列。詳細については、[Braze API: APIを介した移行](https://www.braze.com/docs/help/help_articles/push/push_token_migration/#migration-via-api)を参照してください。|
| プッシュトークン配列            | プッシュトークンの配列。|
| プッシュトークンデバイスID配列  | プッシュトークン移行に使用するデバイスIDの配列。詳細については、[Braze API: APIを介した移行](https://www.braze.com/docs/help/help_articles/push/push_token_migration/#migration-via-api)を参照してください。     |
| タイムゾーン                    | [IANAタイムゾーンデータベース](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)からのタイムゾーン名。例：`America/New_York`または`Eastern Time (US & Canada)`。無効なタイムゾーン値は無視されます。 |
| Twitter                      | ID（整数）、スクリーン名（文字列、Xハンドル）、フォロワー数（整数）、フレンド数（整数）、ステータス数（整数）を含むハッシュ。|
| 既存のユーザーのみを更新 (Users) | `true`または`false`に構成します。ユーザー値が存在しない場合は、デフォルトで作成されます。**true**に構成すると、既存のユーザーのみが更新され、新しいユーザーは作成されません。|


#### ユーザー属性の変更

次の操作を使用して数値ユーザー属性を変更します：

* インクリメント（正または負の値を受け入れる）
* デクリメント
* 追加

配列属性を持つ属性は、既存の配列から値を追加または削除することで変更します。

#### イベント

イベント名は **Name** にマッピングする必要があります。

同じ長さの配列属性をマッピングして複数のイベントを送信します。単一値属性を使用することもでき、各イベントに適用されます。

| **パラメータ** | **説明** |
|:--------------|:----------------|
| App ID | 特定のアプリに関連付けられた App Identifier API キーまたは `app_id`。詳細については、[Braze API: App Identifier API キー](https://www.braze.com/docs/api/api_key/#the-app-identifier-api-key)を参照してください。 |
| Name | （必須）イベントの名前。|
| Time | イベントの時間。値がマッピングされない限り、自動的に `now` に構成されます。|
| Update Existing Only (Events) | **true** または **false** に構成します。イベント値が存在しない場合、デフォルトで作成されます。**true** に構成すると、既存のイベントのみが更新され、新しいイベントは作成されません|

#### イベントテンプレート変数

データ入力としてテンプレート変数を提供します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。

ドット表記を使用してネストされたテンプレート変数を名付けます（例：`items.name`）。

ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。

#### イベントテンプレート

Body Dataで参照されるテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。

テンプレートは、サポートされるフィールドに名前で二重中括弧を使用して注入されます。例えば、`{{SomeTemplateName}}`。

#### 購入

購入データをマッピングするには、製品ID、通貨、および価格の値をマッピングする必要があります。同じ長さの配列属性をマッピングして複数のイベントを送信します。単一値属性を使用することもでき、各イベントに適用されます。

次のコードサンプルは、複数の製品に対する単一イベントの受信に関するBrazeのベストプラクティスの例を示しています：

```json
// Tealiumへのイベント：
{
  [...]
  "tealium_event": "purchase",
  "product_name": ["Backpack", "Pencil", "Notebook"],
  "product_quantity": [1, 5, 3],
  "product_category": ["Travel", "Office", "Office"],
  "product_price": [39.95, 1.99, 3.99],
  "order_currency": "USD"
}
```

対応する製品配列属性をBrazeパラメータにマッピングします：

* `product_name` > 製品ID
* `product_quantity` > 数量
* `product_price` > 価格

この例の結果は、次のようにBrazeに送信される購入オブジェクトを表しています：

```json
// Tealium Connectorを通じてBrazeへのペイロード：
{
  "purchases": [
    {
      "external_id" : "user1",
      "app_id" : "11ae5b4b-2445-4440-a04f-bf537764c9ad",
      "product_id" : "Backpack",
      "currency" : "USD",
      "price" : 39.95,
      "time" : "2013-07-16T19:20:30+01:00",
    },
    {
      "external_id" : "user1",
      "app_id" : "11ae5b4b-2445-4440-a04f-bf537764c9ad",
      "product_id" : "Pencil",
      "currency" : "USD",
      "price" : 1.99,
      "time" : "2013-07-16T19:20:30+01:00",
    },
    {
      "external_id" : "user1",
      "app_id" : "11ae5b4b-2445-4440-a04f-bf537764c9ad",
      "product_id" : "Backpack",
      "currency" : "USD",
      "price" : 3.99,
      "time" : "2013-07-16T19:20:30+01:00",
    }
  ]
}
```

| **パラメータ**| **説明**|
|:-------------|:-----------------|
| App ID | イベントアプリケーションID。|
| Product ID | 製品IDの配列。<br> 購入イベントに必要です。|
| Currency | 購入のISO 4217アルファベット通貨コード。<br> 購入イベントに必要です。|
| Price | 製品価格の配列。<br> 購入イベントに必要です。|
| Quantity | 製品数量の配列。|
| Purchase Time | ISO 8601形式の購入時間。明示的にマッピングされない限り、自動的に `now` に構成されます。|
| Update Existing Only (Purchases) | （オプション）値は `true` または `false` です。デフォルトでは、購入値が存在する場合、デフォルトで作成されます。`true` に構成すると、既存の購入のみが更新され、新しい購入は作成されません。 |

#### 購入テンプレート変数

データ入力としてテンプレート変数を提供します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。

ドット表記を使用してネストされたテンプレート変数を名付けます（例：`items.name`）。

ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。

#### 購入テンプレート

ネストされたオブジェクトを送信するためのテンプレートを定義します。

テンプレートが定義されている場合、**Purchases** セクションのマッピングは無視されます。

Body Dataで参照されるテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。

テンプレートは、サポートされるフィールドに名前で二重中括弧を使用して注入されます。例えば、`{{SomeTemplateName}}`。

#### バッチの有効期限

| **パラメータ** | **説明** |
|:--------------|:----------------|
| Batch Time To Live | （オプション）バッチの有効期限（分）。1から60の間の値を入力します。デフォルト値は10分です。短い間隔でデータが早く送信されますが、APIリクエストの頻度が増加する可能性があります。 |

### ユーザー削除（非バッチ）

External ID、Braze ID、User Aliasのいずれか一つが各アクションで必要ですが、できるだけ多くの属性をマッピングすることをお勧めします。IDがマッピングされると、次の優先順位に基づいて最初の空白でない値が選択されます：

* External ID
* Braze ID
* Alias Name
* Alias Label

詳細については、[Braze API: User Delete Endpoint](https://www.braze.com/docs/api/endpoints/user_data/post_user_delete/)を参照してください。

#### パラメータ

| **パラメータ**    | **説明**|
|:-----------------|:---------------|
| External ID      | 削除するユーザーの外部ID。|
| Braze ID         | 削除するユーザーのBraze ID。|
| User Alias Name  | 削除するユーザーのエイリアス名。ユーザーエイリアスを指定する場合、Alias NameとAlias Labelの両方を構成する必要があります。  |
| User Alias Label | 削除するユーザーのエイリアスラベル。ユーザーエイリアスを指定する場合、Alias NameとAlias Labelの両方を構成する必要があります。 |
| Customer Email Address | ユーザーのメールアドレス。 |
| Customer Phone Number | E.164形式のユーザーの電話番号。 |
| Deletion Prioritization | **Customer Email Address** がユーザーを特定するために使用されるパラメータである場合に必要です。削除リクエストの優先順位をリストする配列。許可される値は `most_recently_updated` および `identified`（External IDを持つユーザー）または `unidentified`（External IDを持たないユーザー）です。 |

### ユーザー購読グループステータスの更新（非バッチ）

詳細については、[Braze API: Subscription Groups Endpoints](https://www.braze.com/docs/api/endpoints/subscription_groups/)を参照してください。

#### パラメータ

| **パラメータ**| **説明**|
|:-------------|:---------------|
| Group Type | (必須) 管理する購読グループのタイプ（`SMS` または `EMAIL`）。|
| Update Type | (必須) 構成する購読状態（`SUBSCRIBE` または `UNSUBSCRIBE`）。|
| Subscription Group ID  | (必須) 購読グループのID。|
| External ID | ユーザーまたはユーザーの外部ID。|
| Email | (EMAIL購読グループで使用。)<br> ユーザーのメールアドレス。<br> External IDが `EMAIL` グループに構成されていない場合、メールが必要です。|
| Phone | (SMS購読グループで使用。)<br> E.164形式の電話番号。<br> 例：`+1415555371`<br> External IDが `SMS` グループに構成されていない場合、電話が必要です。 |

### 複数の購読グループにわたるユーザー購読グループステータスの更新（非バッチ）
#### パラメータ

| **パラメータ** | **説明** |
|:--------------|:----------------|
| グループタイプ | (必須) 管理するサブスクリプショングループのタイプ (`SMS`, `EMAIL`, または `SMS` と `EMAIL` の両方)。|
| 更新タイプ | (必須) 構成するサブスクリプションの状態 (`SUBSCRIBE` または `UNSUBSCRIBE`)。  |
| サブスクリプショングループID  | (必須) サブスクリプショングループのID。複数のサブスクリプショングループで同時にユーザーのステータスを更新するために、配列型属性をマッピングします。|
| 外部ID | ユーザーの外部ID。<br> Emailが構成されていない場合、外部IDが必要です。|
| Email | (EMAILサブスクリプショングループで使用)。<br> ユーザーのメールアドレス。<br> `EMAIL` グループで外部IDが構成されていない場合、Emailが必要です。|
| 電話 | (SMSサブスクリプショングループで使用)。<br> E.164形式の電話番号。<br> 例: `+1415555371`<br> `SMS` グループで外部IDが構成されていない場合、電話が必要です。 |

### キャンペーンメッセージの送信

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* リクエストの最大数: 50
* 最古のリクエストからの最大時間: 10分
* リクエストの最大サイズ: 1 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| キャンペーンID | (必須) キャンペーンID。 |
| 送信ID | Brazeによって生成されるか、またはあなたによって作成されるキーで、特定のメッセージ送信の下で追跡されるべき分析のために使用されます。 |
| エイリアス名 | エイリアスの値。 |
| エイリアスラベル | エイリアスのキー。 |
| 外部ユーザーID | 複数のデバイス間で同じユーザープロファイルを識別するために使用される値。 |
| 既存のみに送信 | デフォルト値は `true` です。`false` の場合、属性オブジェクトも含める必要があります。 |
| トリガープロパティ | メッセージテンプレートで参照できるパーソナライゼーションのキー値ペア。<br>ネストされたオブジェクトのテンプレート化に使用します。 |
| 受信者属性 | 受信者の属性を作成または更新します。 |
| テンプレート変数 | <b>テンプレート</b>のためのデータ入力としてテンプレート変数を提供します。<br>詳細と使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<br>ドット表記でネストされたテンプレート変数を名前付けします。例: `items.name`。<br>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。 |
| テンプレート | トリガープロパティで参照されるテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。<br>サポートされるフィールドに名前でテンプレートを挿入します。例: `{{SomeTemplateName}}`。 |

### Canvasメッセージの送信

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* リクエストの最大数: 50
* 最古のリクエストからの最大時間: 10分
* リクエストの最大サイズ: 1 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| Canvasデータ | <b>Canvas ID</b> - Brazeダッシュボード内の特定のCanvasに対してBrazeによって生成されるランダムキー。 |
| エイリアス名 | エイリアスの値。 |
| エイリアスラベル | エイリアスのキー。 |
| 外部ユーザーID | 複数のデバイス間で同じユーザープロファイルを識別するために使用される値。 |
| 既存のみに送信 | デフォルト値は `true` です。`false` の場合、属性オブジェクトも含める必要があります。 |
| トリガープロパティ | メッセージテンプレートで参照できるパーソナライゼーションのキー値ペア。<br>ネストされたオブジェクトのテンプレート化に使用します。 |
| 受信者属性 | 受信者の属性を作成または更新します。 |
| Canvasエントリプロパティ | メッセージテンプレートで参照できるパーソナライゼーションのキー値ペア。<br>ネストされたオブジェクトのテンプレート化に使用します。 |
| テンプレート変数 | <b>テンプレート</b>のためのデータ入力としてテンプレート変数を提供します。<br>詳細と使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<br>ドット表記でネストされたテンプレート変数を名前付けします。例: `items.name`。<br>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。 |
| テンプレート | トリガープロパティで参照されるテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。<br>サポートされるフィールドに名前でテンプレートを挿入します。例: `{{SomeTemplateName}}`。 |

### トランザクショナルメールの送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| キャンペーンID | (必須) キャンペーンID。 |
| 外部送信ID | 特定の送信のための識別子。渡された場合、この識別子は重複キーとしても使用され、Brazeは24時間保存します。 |
| エイリアス名 | エイリアスの値。 |
| エイリアスラベル | エイリアスのキー。 |
| 外部ユーザーID | 複数のデバイス間で同じユーザープロファイルを識別するために使用される値。 |
| トリガープロパティ | メッセージテンプレートで参照できるパーソナライゼーションのキー値ペア。<br>ネストされたオブジェクトのテンプレート化に使用します。 |
| 受信者属性 | 受信者の属性を作成または更新します。 |
| テンプレート変数 | <b>テンプレート</b>のためのデータ入力としてテンプレート変数を提供します。<br>詳細と使用例については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。<br>ドット表記でネストされたテンプレート変数を名前付けします。例: `items.name`。<br>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。 |
| テンプレート | トリガープロパティで参照されるテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。<br>サポートされるフィールドに名前でテンプレートを挿入します。例: `{{SomeTemplateName}}`。 |

### ユーザーの識別

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* リクエストの最大数: 50
* 最古のリクエストからの最大時間: 10分
* リクエストの最大サイズ: 1 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 外部ID | Brazeで外部IDにマッピングする属性を選択します。 |
| エイリアス名 | (必須) エイリアス名。 |
| エイリアスラベル | (必須) エイリアスラベル。 |

## よくある質問

### このコネクタは他のBraze統合とどのように連携しますか？

Track User APIに加えて、Brazeにはユーザー属性のマッピングをサポートする追加のデータ収集方法があります。Tealiumは、次の2つの独立したが類似した統合でWebおよびネイティブモバイルのBraze SDKをサポートしています：

* [Braze Web SDK Tag Setup](https://docs.tealium.com/braze-web-sdk-tag/), [Braze Initial SDK Setup](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/initial_sdk_setup/)
* AndroidおよびiOS/Swift用Tealium Remote Command for Braze ([詳細はこちら](https://docs.tealium.com/platforms/remote-commands/integrations/braze/))

これらの統合は、コネクタのイベントおよび購入アクションで収集されるデータに類似したユーザー行動データをBrazeが収集するために使用される代替方法です。