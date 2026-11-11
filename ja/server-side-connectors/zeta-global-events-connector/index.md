---
title: Zeta Global Eventsコネクタ構成ガイド
description: Event StreamingからZetaのTrack Event REST APIに行動イベントを送信するように、Zeta Global Eventsコネクタを構成します。
url: https://docs.tealium.com/ja/server-side-connectors/zeta-global-events-connector/
---
## API情報

このコネクタは、次のベンダーAPIを使用します。

* API名：Zeta Global API
* APIバージョン：ver2
* APIエンドポイント：`https://api.zetaglobal.net/`
* ドキュメント：[Zeta Global API](https://docs.zetaglobal.com/reference/track-an-event-rest)

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、認証モードを選択し、そのモードの構成を構成します。

* **リフレッシュトークン**：（JWT認証）ZMPリフレッシュトークン（ZMP > Settings > Integrations > Keys & Apps）。新しい構成ではこちらを使用してください。
* **アクセストークン**：（Basic認証）ZMPアクセストークン。コネクタは、この値をHTTP Basic Authorizationヘッダーのパスワードとして送信します。ユーザー名は`api`に固定されています。既存のBasic認証構成は引き続き機能します。
* **サイトID**：ZMPサイトID。コネクタはこの値をAPIリクエストパスで使用します（例：`https://api.zetaglobal.net/ver2/{site_id}/activities`）。

コネクタを構成したら、**完了**をクリックします。

## アクション

| アクション名 | ビジタープロファイル | イベントデータ |
| --- | :---: | :---: |
| イベントをトラッキング | ✗ | ✓ |
| イベントをトラッキング（バッチ） | ✗ | ✓ |
| 識別情報付きでイベントをトラッキング | ✗ | ✓ |

### イベントをトラッキング

#### アクティビティデータ

Tealium属性を`activity`の最上位フィールドにマッピングします。

| パラメータ | 説明 |
| --- | --- |
| イベント | （必須）イベント名。イベント名は、ZMPで構成されているイベントの命名と一致する必要があります。 |
| タイムスタンプ | ISO-8601形式のイベント時刻（例：`2026-08-07T15:56:00Z`）。エポックミリ秒は、422 Invalid date formatエラーで拒否されます。マッピングしない場合、Zeta独自のサーバー時刻が構成されます。 |
| サブサイトID | `activity.sub_site_ids`の最上位配列として送信される、1つ以上の子アカウントID。単一の値は、1要素の配列に正規化されます。 |

追加したカスタムキーは、最上位の`activity`オブジェクトに配置されます。カスタムキーで予約済みフィールドの`event`、`timestamp`、`subscriber`、`identify_person`、`properties`、`sub_site_ids`を上書きすることはできません。

#### サブスクライバーデータ

Tealium属性を、イベントに関連付けられた人物の`activity.subscriber`フィールドにマッピングします。

| パラメータ | 説明 |
| --- | --- |
| UID | `activity.subscriber.uid`として送信される人物の一意の識別子。Zetaが複数のイベントを1つのプロファイルとして解決できるように、UIDはイベント間で一貫している必要があります。UID、固有クライアントIDのペア、またはBSINのうち、少なくとも1つが必要です。これらがいずれもないイベントはスキップされます。 |
| BSIN | 匿名ビジターの暗号化されたZeta BSIN。通常はZync Cookieから取得されます。明示的にマッピングされていない場合は、デフォルトで`cp.bsin`イベント属性が使用されます。マッピングされている場合、コネクタはZeta Identify APIから匿名ID（`anon_id`）を解決し、セッション内の後続イベントで使用します。`anon_id`が解決されている場合、UIDは必要ありません。 |
| 固有クライアントID名 | `subscriber.unique_client_id`エントリの識別子タイプ。**固有クライアントID値**とともにマッピングします。識別子タイプは、使用前にZMPへ登録する必要があります。未登録の名前は202レスポンスで受け入れられますが、通知なしで破棄されます。 |
| 固有クライアントID値 | `subscriber.unique_client_id`エントリの識別子値。**固有クライアントID名**とともにマッピングします。 |

このアクションでは`identify_person`が構成されないため、サブスクライバーの名前フィールドと連絡先は使用できません。サブスクライバーの名前フィールドと連絡先をマッピングするには、「識別情報付きでイベントをトラッキング」アクションを使用してください。

#### プロパティデータ

任意。Tealium属性を`activity.properties`内のキーにマッピングします。

| パラメータ | 説明 |
| --- | --- |
| 注文ID | `properties.order_id`にマッピングされる注文識別子。 |
| アイテムID | `properties.items[].id`にマッピングされるアイテム識別子。 |
| アイテムSKU | `properties.items[].sku`にマッピングされるアイテムSKU。 |
| アイテムリソースタイプ | `properties.items[].resourceType`にマッピングされるアイテムのリソースタイプ。デフォルトは`product`です。 |
| アイテム価格 | `properties.items[].price`にマッピングされるアイテム価格。 |
| アイテム数量 | `properties.items[].quantity`にマッピングされるアイテム数量。 |
| アイテム商品名 | `properties.items[].productname`にマッピングされる商品名。 |
| アイテムカテゴリー | `properties.items[].category`にマッピングされるアイテムカテゴリー。 |
| アイテムサブカテゴリー | `properties.items[].subcategory`にマッピングされるアイテムサブカテゴリー。 |
| アイテムサイズ | `properties.items[].size`にマッピングされるアイテムサイズ。 |
| アイテムURL | `properties.items[].url`にマッピングされるアイテムURL。 |
| Eコマース自動マッピングを無効化 | デフォルトでは、TealiumのEコマース変数（`_corder`、`_cprod`、`_csku`、`_cprice`、`_cquan`、`_cprodname`、`_ccat`、`_ccat2`、`dom.url`）が`activity.properties`に自動的にマッピングされます。Eコマース自動マッピングを無効にするには、このチェックボックスを選択します。明示的なプロパティデータのマッピングは、常に自動マッピングより優先されます。 |

アイテムフィールド（**アイテムID**から**アイテムURL**まで）は、インデックス位置ごとに結合され、`properties.items[]`内の各アイテムオブジェクトが作成されます。各アイテム属性は配列として解決される必要があり、すべての配列の長さが同じである必要があります。

追加したカスタムキーは、`activity.properties`の下に配置されます。

**テンプレート**

フラットなキーと属性のマッピングでは表現できない、ネストされたJSON構造を構築するには、テンプレートを使用します。

| パラメータ | 説明 |
| --- | --- |
| テンプレート — ネストされた値 | テンプレートをカスタムキーにマッピングし、レンダリングされたJSON（オブジェクト、配列、またはスカラー）を`properties`内のそのキーの下にネストします。 |
| テンプレート — アイテムリスト | アイテムオブジェクトのJSON配列をレンダリングするテンプレートを**アイテム**オプションにマッピングし、Zetaのアイテムフィールド名（`id`、`sku`、`resourceType`、`price`、`quantity`、`productname`、`category`、`subcategory`、`size`、`url`）を使用して、`properties.items[]`リスト全体を一度に構成します。マッピングされたアイテムリストテンプレートは、個別のアイテムフィールドマッピングを置き換えます。マッピングされたアイテムリストと個別のアイテムフィールドマッピングは、どちらもEコマース自動マッピングより優先されます。自動マッピングによって`items[]`が構成されるのは、アイテムが明示的にマッピングされていない場合のみです。 |

### イベントをトラッキング（バッチ）

#### バッチ制限

このアクションは、ベンダーへの大量データ転送に対応するため、バッチリクエストを使用します。並列処理により、イベントが順不同でベンダーに到達する場合があります。順序が重要な場合は、イベントにシーケンス値を追加してください。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに保持されます。

* リクエストの最大数：100
* 最も古いリクエストからの最大経過時間：10分
* リクエストの最大サイズ：1 MB

このアクションのアクティビティデータ、サブスクライバーデータ、プロパティデータの構成は、[イベントをトラッキング](#track-event)と同じです。

このバッチアクションでは`identify_person`が構成されないため、サブスクライバーの名前フィールドと連絡先は使用できません。サブスクライバーの名前フィールドと連絡先をマッピングするには、「識別情報付きでイベントをトラッキング」アクションを使用してください。

### 識別情報付きでイベントをトラッキング

#### アクティビティデータ

Tealium属性を`activity`の最上位フィールドにマッピングします。

| パラメータ | 説明 |
| --- | --- |
| イベント | （必須）イベント名。イベント名は、ZMPで構成されているイベントの命名と一致する必要があります。 |
| タイムスタンプ | ISO-8601形式のイベント時刻（例：`2026-08-07T15:56:00Z`）。エポックミリ秒は、422 Invalid date formatエラーで拒否されます。マッピングしない場合、Zeta独自のサーバー時刻が構成されます。 |
| サブサイトID | `activity.sub_site_ids`の最上位配列として送信される、1つ以上の子アカウントID。単一の値は、1要素の配列に正規化されます。 |

追加したカスタムキーは、最上位の`activity`オブジェクトに配置されます。カスタムキーで予約済みフィールドの`event`、`timestamp`、`subscriber`、`identify_person`、`properties`、`sub_site_ids`を上書きすることはできません。
#### サブスクライバーデータ

Tealium 属性を、イベントに関連付けられた人物の `activity.subscriber` フィールドにマッピングします。

| パラメータ | 説明 |
| --- | --- |
| UID | 人物の一意の識別子。`activity.subscriber.uid` として送信されます。Zeta がイベントを同一のプロファイルに関連付けられるように、UID はイベント間で一貫している必要があります。UID、Unique Client ID のペア、BSIN のうち、少なくとも1つが必要です。いずれも含まれていないイベントはスキップされます。 |
| BSIN | 匿名訪問の暗号化された Zeta BSIN。通常は Zync Cookie から取得されます。明示的にマッピングされていない場合、デフォルトで `cp.bsin` イベント属性が使用されます。マッピングされている場合、コネクタは Zeta Identify API から匿名 ID（`anon_id`）を解決し、セッション内の後続イベントで使用します。`anon_id` が解決されている場合、UID は必要ありません。 |
| Unique Client ID Name | `unique_client_ids` リスト内のエントリに使用する識別子タイプ。**Unique Client ID Value** と併せてマッピングします。1回の呼び出しにつき最大25個の識別子ペアを指定できます。識別子タイプは、使用前に ZMP に登録する必要があります。未登録の名前も 202 レスポンスで受け入れられますが、通知なく破棄されます。 |
| Unique Client ID Value | `unique_client_ids` リスト内のエントリに使用する識別子の値。**Unique Client ID Name** と併せてマッピングします。 |
| First Name | 人物の名。このアクションでは `identify_person` が構成されるため、プロファイルに保持されます。 |
| Last Name | 人物の姓。このアクションでは `identify_person` が構成されるため、プロファイルに保持されます。 |
| Name | 人物の氏名。このアクションでは `identify_person` が構成されるため、プロファイルに保持されます。 |

#### 連絡先データ

任意。Tealium 属性を `subscriber.contacts[]` のフィールドにマッピングし、メールまたは電話チャネルをプロファイルに関連付けます。


<blockquote>
Zeta は、新規プロファイルにのみ連絡先を関連付けます。既存のプロファイルでは、Contacts Data セクションは無視されます。
</blockquote>


| パラメータ | 説明 |
| --- | --- |
| Contact Value | （必須）連絡先のメールアドレスまたは電話番号。他の Contact フィールドをマッピングする場合は必須です。 |
| Contact Type | 連絡先のタイプ：`email` または `phone`。デフォルトは `email` です。 |
| Preferences | 連絡先の構成（例：`standard` または `billing`）。デフォルトは `standard` です。追加の構成は ZMP で構成できます。 |
| Subscription Status | 購読ステータス：`new`、`active`、`inactive`、または空白。デフォルトは `active` です。空白または null 値の場合、既存の連絡先では現在のステータスが維持され、新規の連絡先では `new` が構成されます。`new` ステータスは、その連絡先にメッセージが送信されるまで維持されます。 |
| Force Active | 連絡先を作成するときに、デフォルトの `new` ステータスを使用せずに済むようにするには、これを選択します。 |
| Inactivity Reason | 連絡先が非アクティブになっている理由（例：`unsubscribed`）。 |
| Double Opt In Status | ダブルオプトインのステータス：`single` または `double`。 |
| Phone Type | 電話のタイプ：`mobile` または `landline`。電話の連絡先にのみ適用されます。 |
| Last Clicked | 最後にメッセージがクリックされた時刻。ISO-8601 形式で指定します。 |
| Last Opened | 最後にメッセージが開封された時刻。ISO-8601 形式で指定します。 |
| Last Sent | 最後にメッセージが送信された時刻。ISO-8601 形式で指定します。 |
| Signed Up At | 連絡先が登録された日付。ISO-8601 形式で指定します（例：`2015-01-02T05:30:21Z`）。デフォルトは作成日です。 |

追加したカスタムキーは、コネクタによって連絡先の `contact_properties` オブジェクトに書き込まれます。

**テンプレート**

テンプレートを使用すると、フラットなキーと属性のマッピングでは表現できない、ネストされた JSON 構造を構築できます。

| パラメータ | 説明 |
| --- | --- |
| Template — nested value | テンプレートをカスタムキーにマッピングし、レンダリングされた JSON を `contact_properties` 内のそのキーの下にネストします。 |
| Template — Contacts list | 連絡先オブジェクトの JSON 配列をレンダリングするテンプレートを **Contacts** オプションにマッピングし、Zeta の連絡先フィールド名を使用して `subscriber.contacts[]` リスト全体を一度に構成します。Contacts リストのテンプレートがマッピングされている場合、個別の連絡先フィールドのマッピングは置き換えられます。 |

#### プロパティデータ

任意。Tealium 属性を `activity.properties` 内のキーにマッピングします。

| パラメータ | 説明 |
| --- | --- |
| Order ID | 注文識別子。`properties.order_id` にマッピングされます。 |
| Item ID | アイテム識別子。`properties.items[].id` にマッピングされます。 |
| Item SKU | アイテムの SKU。`properties.items[].sku` にマッピングされます。 |
| Item Resource Type | アイテムのリソースタイプ。`properties.items[].resourceType` にマッピングされます。デフォルトは `product` です。 |
| Item Price | アイテムの価格。`properties.items[].price` にマッピングされます。 |
| Item Quantity | アイテムの数量。`properties.items[].quantity` にマッピングされます。 |
| Item Product Name | 商品名。`properties.items[].productname` にマッピングされます。 |
| Item Category | アイテムのカテゴリ。`properties.items[].category` にマッピングされます。 |
| Item Subcategory | アイテムのサブカテゴリ。`properties.items[].subcategory` にマッピングされます。 |
| Item Size | アイテムのサイズ。`properties.items[].size` にマッピングされます。 |
| Item URL | アイテムの URL。`properties.items[].url` にマッピングされます。 |
| Disable E-commerce Automapping | デフォルトでは、Tealium の E コマース変数（`_corder`、`_cprod`、`_csku`、`_cprice`、`_cquan`、`_cprodname`、`_ccat`、`_ccat2`、`dom.url`）が `activity.properties` に自動的にマッピングされます。E コマースの自動マッピングを無効にするには、このチェックボックスを選択します。明示的な Properties Data のマッピングは、常に自動マッピングより優先されます。 |

Item フィールド（**Item ID** から **Item URL** まで）は、インデックス位置に基づいて結合され、`properties.items[]` 内の各アイテムオブジェクトが構築されます。各 Item 属性は配列に解決される必要があり、すべての配列の長さが同じでなければなりません。

追加したカスタムキーは、コネクタによって `activity.properties` の下に配置されます。

**テンプレート**

テンプレートを使用すると、フラットなキーと属性のマッピングでは表現できない、ネストされた JSON 構造を構築できます。

| パラメータ | 説明 |
| --- | --- |
| Template — nested value | テンプレートをカスタムキーにマッピングし、レンダリングされた JSON（オブジェクト、配列、またはスカラー）を `properties` 内のそのキーの下にネストします。 |
| Template — Items list | アイテムオブジェクトの JSON 配列をレンダリングするテンプレートを **Items** オプションにマッピングし、Zeta のアイテムフィールド名（`id`、`sku`、`resourceType`、`price`、`quantity`、`productname`、`category`、`subcategory`、`size`、`url`）を使用して `properties.items[]` リスト全体を一度に構成します。Items リストのテンプレートがマッピングされている場合、個別の Item フィールドのマッピングは置き換えられます。マッピングされた Items リストと個別の Item フィールドのマッピングは、どちらも E コマースの自動マッピングより優先されます。アイテムが明示的にマッピングされていない場合にのみ、自動マッピングによって `items[]` が構成されます。 |