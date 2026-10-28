---
title: Zeta Global Eventsコネクタ構成ガイド
description: Tealium EventStreamからZetaのTrack Event REST APIに行動イベントを送信するためのZeta Global Eventsコネクタを構成します。
url: https://docs.tealium.com/ja/server-side-connectors/zeta-global-events-connector/
---
## API情報

このコネクタは、次のベンダーAPIを使用します。

* API名：Zeta Global API
* APIバージョン：ver2
* APIエンドポイント：`https://api.zetaglobal.net/`
* ドキュメント：[Zeta Global API](https://docs.zetaglobal.com/reference/track-an-event-rest)

## 構成

Connector Marketplaceに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、認証モードを選択し、そのモードの構成を構成します。

* **Refresh Token**：（JWT認証）ZMPのリフレッシュトークン（ZMP > Settings > Integrations > Keys & Apps）。新しい構成ではこちらを使用してください。
* **Access Token**：（Basic認証）ZMPのアクセストークン。コネクタは、この値をHTTP Basic Authorizationヘッダーのパスワードとして送信します。ユーザー名は`api`に固定されています。既存のBasic認証構成は引き続き機能します。
* **Site ID**：ZMPのサイトID。コネクタは、APIリクエストパス（例：`https://api.zetaglobal.net/ver2/{site_id}/activities`）でこの値を使用します。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| Track Event | ✗ | ✓ |
| Track Events (Batch) | ✗ | ✓ |
| Track Event with Identify | ✗ | ✓ |

### Track Event

#### アクティビティデータ

Tealium属性を`activity`の最上位フィールドにマッピングします。

| パラメータ | 説明 |
| --- | --- |
| Event | （必須）イベント名。イベント名は、ZMPで構成されているイベント命名と一致する必要があります。 |
| Timestamp | ISO-8601形式のイベント時刻（例：`2026-08-07T15:56:00Z`）。エポックミリ秒は、422 Invalid date formatエラーで拒否されます。マッピングされていない場合、Zeta独自のサーバー時刻が構成されます。 |
| Sub-Site IDs | `activity.sub_site_ids`の最上位配列として送信される、1つ以上の子アカウントID。単一の値は、要素が1つの配列に正規化されます。 |

追加したカスタムキーは、最上位の`activity`オブジェクトに配置されます。カスタムキーで予約済みフィールド`event`、`timestamp`、`subscriber`、`identify_person`、`properties`、`sub_site_ids`を上書きすることはできません。

#### 購読者データ

Tealium属性を、イベントに関連付けられた人物の`activity.subscriber`フィールドにマッピングします。

| パラメータ | 説明 |
| --- | --- |
| UID | `activity.subscriber.uid`として送信される人物の一意の識別子。Zetaが複数のイベントを1つのプロファイルに関連付けられるように、UIDはイベント間で一貫している必要があります。UID、Unique Client IDのペア、またはBSINのうち、少なくとも1つが必要です。これらがいずれもないイベントはスキップされます。 |
| BSIN | 匿名訪問の暗号化されたZeta BSIN。通常はZync Cookieから取得されます。明示的にマッピングされていない場合、デフォルトで`cp.bsin`イベント属性が使用されます。マッピングされている場合、コネクタはZeta Identify APIから匿名ID（`anon_id`）を解決し、セッション内の後続イベントで使用します。`anon_id`が解決された場合、UIDは必要ありません。 |
| Unique Client ID Name | `subscriber.unique_client_id`エントリの識別子タイプ。**Unique Client ID Value**と一緒にマッピングします。識別子タイプは、使用前にZMPに登録する必要があります。未登録の名前は202レスポンスで受け入れられますが、通知なく破棄されます。 |
| Unique Client ID Value | `subscriber.unique_client_id`エントリの識別子値。**Unique Client ID Name**と一緒にマッピングします。 |

このアクションでは`identify_person`が構成されないため、購読者の名前フィールドと連絡先は使用できません。購読者の名前フィールドと連絡先をマッピングするには、Track Event with Identifyアクションを使用してください。

#### プロパティデータ

任意。Tealium属性を`activity.properties`内のキーにマッピングします。

| パラメータ | 説明 |
| --- | --- |
| Order ID | `properties.order_id`にマッピングされる注文識別子。 |
| Item ID | `properties.items[].id`にマッピングされる商品識別子。 |
| Item SKU | `properties.items[].sku`にマッピングされる商品のSKU。 |
| Item Resource Type | `properties.items[].resourceType`にマッピングされる商品のリソースタイプ。デフォルトは`product`です。 |
| Item Price | `properties.items[].price`にマッピングされる商品価格。 |
| Item Quantity | `properties.items[].quantity`にマッピングされる商品数量。 |
| Item Product Name | `properties.items[].productname`にマッピングされる商品名。 |
| Item Category | `properties.items[].category`にマッピングされる商品カテゴリ。 |
| Item Subcategory | `properties.items[].subcategory`にマッピングされる商品サブカテゴリ。 |
| Item Size | `properties.items[].size`にマッピングされる商品サイズ。 |
| Item URL | `properties.items[].url`にマッピングされる商品のURL。 |
| Disable E-commerce Automapping | デフォルトでは、TealiumのEコマース変数（`_corder`、`_cprod`、`_csku`、`_cprice`、`_cquan`、`_cprodname`、`_ccat`、`_ccat2`、`dom.url`）が`activity.properties`に自動的にマッピングされます。Eコマースの自動マッピングを無効にするには、このチェックボックスを選択します。明示的なProperties Dataマッピングは、常に自動マッピングより優先されます。 |

Itemフィールド（**Item ID**から**Item URL**まで）は、インデックス位置に基づいて結合され、`properties.items[]`内の各商品オブジェクトが作成されます。各Item属性は配列に解決される必要があり、すべての配列は同じ長さでなければなりません。

追加したカスタムキーは、`activity.properties`の下に配置されます。

**テンプレート**

フラットなキーと属性のマッピングでは表現できない、ネストされたJSON構造を作成するにはテンプレートを使用します。

| パラメータ | 説明 |
| --- | --- |
| Template — nested value | テンプレートをカスタムキーにマッピングし、レンダリングされたJSON（オブジェクト、配列、またはスカラー）を`properties`内のそのキーの下にネストします。 |
| Template — Items list | 商品オブジェクトのJSON配列をレンダリングするテンプレートを**Items**オプションにマッピングし、Zetaの商品フィールド名（`id`、`sku`、`resourceType`、`price`、`quantity`、`productname`、`category`、`subcategory`、`size`、`url`）を使用して、`properties.items[]`リスト全体を一度に構成します。マッピングされたItems listテンプレートは、個別のItemフィールドマッピングを置き換えます。マッピングされたItems listと個別のItemフィールドマッピングは、どちらもEコマースの自動マッピングより優先されます。自動マッピングで`items[]`が構成されるのは、商品が明示的にマッピングされていない場合のみです。 |

### Track Events (Batch)

#### バッチ制限

このアクションは、ベンダーへの大容量データ転送をサポートするために、バッチリクエストを使用します。並列処理により、イベントが順不同でベンダーに到達する場合があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまでキューに保持されます。

* リクエストの最大数：100
* 最も古いリクエストからの最大経過時間：10分
* リクエストの最大サイズ：1 MB

このアクションのアクティビティデータ、購読者データ、およびプロパティデータの構成は、[Track Event](#track-event)と同じです。

このバッチアクションでは`identify_person`が構成されないため、購読者の名前フィールドと連絡先は使用できません。購読者の名前フィールドと連絡先をマッピングするには、Track Event with Identifyアクションを使用してください。

### Track Event with Identify

#### アクティビティデータ

Tealium属性を`activity`の最上位フィールドにマッピングします。

| パラメータ | 説明 |
| --- | --- |
| Event | （必須）イベント名。イベント名は、ZMPで構成されているイベント命名と一致する必要があります。 |
| Timestamp | ISO-8601形式のイベント時刻（例：`2026-08-07T15:56:00Z`）。エポックミリ秒は、422 Invalid date formatエラーで拒否されます。マッピングされていない場合、Zeta独自のサーバー時刻が構成されます。 |
| Sub-Site IDs | `activity.sub_site_ids`の最上位配列として送信される、1つ以上の子アカウントID。単一の値は、要素が1つの配列に正規化されます。 |

追加したカスタムキーは、最上位の`activity`オブジェクトに配置されます。カスタムキーで予約済みフィールド`event`、`timestamp`、`subscriber`、`identify_person`、`properties`、`sub_site_ids`を上書きすることはできません。
#### サブスクライバーデータ

Tealium属性を、イベントに関連付けられた人物の`activity.subscriber`フィールドにマッピングします。

| パラメータ | 説明 |
| --- | --- |
| UID | `activity.subscriber.uid`として送信される、人物の一意の識別子。Zetaが複数のイベントを1つのプロファイルに関連付けられるよう、UIDはイベント間で一貫している必要があります。UID、一意のクライアントIDのペア、またはBSINのうち、少なくとも1つが必要です。これらが1つもないイベントはスキップされます。 |
| BSIN | 匿名訪問の暗号化されたZeta BSIN。通常はZync Cookieから取得されます。明示的にマッピングされていない場合、デフォルトで`cp.bsin`イベント属性が使用されます。マッピングされている場合、コネクタはZeta Identify APIから匿名ID（`anon_id`）を解決し、セッション内の後続イベントでそのIDを使用します。`anon_id`が解決された場合、UIDは必要ありません。 |
| 一意のクライアントID名 | `unique_client_ids`リスト内のエントリに使用する識別子タイプ。**一意のクライアントID値**と併せてマッピングします。1回の呼び出しにつき最大25組の識別子ペアを指定できます。識別子タイプは使用前にZMPへ登録する必要があります。未登録の名前も202レスポンスで受け付けられますが、通知なく破棄されます。 |
| 一意のクライアントID値 | `unique_client_ids`リスト内のエントリに使用する識別子の値。**一意のクライアントID名**と併せてマッピングします。 |
| 名 | 人物の名。このアクションでは`identify_person`が構成されるため、プロファイルに保存されます。 |
| 姓 | 人物の姓。このアクションでは`identify_person`が構成されるため、プロファイルに保存されます。 |
| 氏名 | 人物のフルネーム。このアクションでは`identify_person`が構成されるため、プロファイルに保存されます。 |

#### 連絡先データ

任意。Tealium属性を`subscriber.contacts[]`のフィールドにマッピングし、メールまたは電話チャネルをプロファイルに関連付けます。


<blockquote>
Zetaは、新しいプロファイルに対してのみ連絡先を関連付けます。既存のプロファイルでは、連絡先データセクションは無視されます。
</blockquote>


| パラメータ | 説明 |
| --- | --- |
| 連絡先の値 | （必須）連絡先のメールアドレスまたは電話番号。他の連絡先フィールドをマッピングする場合は、必ず指定する必要があります。 |
| 連絡先タイプ | 連絡先のタイプ：`email`または`phone`。デフォルトは`email`です。 |
| プリファレンス | 連絡先のプリファレンス（例：`standard`または`billing`）。デフォルトは`standard`です。追加のプリファレンスはZMPで構成できます。 |
| サブスクリプションステータス | サブスクリプションステータス：`new`、`active`、`inactive`、または空白。デフォルトは`active`です。空白またはnull値の場合、既存の連絡先では現在のステータスが維持され、新しい連絡先では`new`が構成されます。連絡先にメッセージが送信されるまで、`new`ステータスが維持されます。 |
| 強制的にアクティブ化 | 連絡先を作成する際、デフォルトの`new`ステータスを使用しないようにするには、これを選択します。 |
| 非アクティブの理由 | 非アクティブな連絡先が非アクティブである理由（例：`unsubscribed`）。 |
| ダブルオプトインステータス | ダブルオプトインステータス：`single`または`double`。 |
| 電話タイプ | 電話のタイプ：`mobile`または`landline`。電話の連絡先にのみ適用されます。 |
| 最終クリック日時 | メッセージが最後にクリックされた日時のタイムスタンプ（ISO-8601形式）。 |
| 最終開封日時 | メッセージが最後に開封された日時のタイムスタンプ（ISO-8601形式）。 |
| 最終送信日時 | メッセージが最後に送信された日時のタイムスタンプ（ISO-8601形式）。 |
| 登録日時 | 連絡先が登録された日付（ISO-8601形式、例：`2015-01-02T05:30:21Z`）。デフォルトは作成日です。 |

追加したカスタムキーは、コネクタによって連絡先の`contact_properties`オブジェクトに書き込まれます。

**テンプレート**

フラットなキーと属性のマッピングでは表現できない、ネストされたJSON構造を作成するには、テンプレートを使用します。

| パラメータ | 説明 |
| --- | --- |
| テンプレート — ネストされた値 | テンプレートをカスタムキーにマッピングし、レンダリングされたJSONを`contact_properties`内のそのキーの下にネストします。 |
| テンプレート — 連絡先リスト | 連絡先オブジェクトのJSON配列をレンダリングするテンプレートを**連絡先**オプションにマッピングし、Zetaの連絡先フィールド名を使用して`subscriber.contacts[]`リスト全体を一度に構成します。連絡先リストのテンプレートがマッピングされている場合、個別の連絡先フィールドのマッピングは置き換えられます。 |

#### プロパティデータ

任意。Tealium属性を`activity.properties`内のキーにマッピングします。

| パラメータ | 説明 |
| --- | --- |
| 注文ID | 注文識別子。`properties.order_id`にマッピングされます。 |
| 商品ID | 商品識別子。`properties.items[].id`にマッピングされます。 |
| 商品SKU | 商品SKU。`properties.items[].sku`にマッピングされます。 |
| 商品リソースタイプ | 商品のリソースタイプ。`properties.items[].resourceType`にマッピングされます。デフォルトは`product`です。 |
| 商品価格 | 商品の価格。`properties.items[].price`にマッピングされます。 |
| 商品数量 | 商品の数量。`properties.items[].quantity`にマッピングされます。 |
| 商品名 | 商品の名称。`properties.items[].productname`にマッピングされます。 |
| 商品カテゴリ | 商品のカテゴリ。`properties.items[].category`にマッピングされます。 |
| 商品サブカテゴリ | 商品のサブカテゴリ。`properties.items[].subcategory`にマッピングされます。 |
| 商品サイズ | 商品のサイズ。`properties.items[].size`にマッピングされます。 |
| 商品URL | 商品のURL。`properties.items[].url`にマッピングされます。 |
| Eコマース自動マッピングを無効化 | デフォルトでは、TealiumのEコマース変数（`_corder`、`_cprod`、`_csku`、`_cprice`、`_cquan`、`_cprodname`、`_ccat`、`_ccat2`、`dom.url`）が`activity.properties`に自動的にマッピングされます。Eコマースの自動マッピングを無効にするには、このチェックボックスを選択します。明示的なプロパティデータのマッピングは、常に自動マッピングより優先されます。 |

商品フィールド（**商品ID**から**商品URL**まで）は、インデックス位置に基づいて組み合わされ、`properties.items[]`内の各商品オブジェクトが作成されます。各商品属性は配列として解決される必要があり、すべての配列の長さが同じである必要があります。

追加したカスタムキーは、コネクタによって`activity.properties`の下に配置されます。

**テンプレート**

フラットなキーと属性のマッピングでは表現できない、ネストされたJSON構造を作成するには、テンプレートを使用します。

| パラメータ | 説明 |
| --- | --- |
| テンプレート — ネストされた値 | テンプレートをカスタムキーにマッピングし、レンダリングされたJSON（オブジェクト、配列、またはスカラー）を`properties`内のそのキーの下にネストします。 |
| テンプレート — 商品リスト | 商品オブジェクトのJSON配列をレンダリングするテンプレートを**商品**オプションにマッピングし、Zetaの商品フィールド名（`id`、`sku`、`resourceType`、`price`、`quantity`、`productname`、`category`、`subcategory`、`size`、`url`）を使用して`properties.items[]`リスト全体を一度に構成します。商品リストのテンプレートがマッピングされている場合、個別の商品フィールドのマッピングは置き換えられます。マッピングされた商品リストと個別の商品フィールドのマッピングは、どちらもEコマースの自動マッピングより優先されます。自動マッピングによって`items[]`が構成されるのは、商品が明示的にマッピングされていない場合のみです。 |