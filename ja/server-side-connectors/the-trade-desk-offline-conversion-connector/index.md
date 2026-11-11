---
title: The Trade Desk オフラインコンバージョンコネクタ構成ガイド
description: この記事では、The Trade Desk（TheTradeDesk）オフラインコンバージョンコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/the-trade-desk-offline-conversion-connector/
---
## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、以下の項目を構成します。

* **Agency Secret Key**：The Trade Desk から提供される秘密鍵。
* **Merchant ID**：（任意）The Trade Desk のマーチャントアカウントに関連付けられた ID。この ID は The Trade Desk から提供されます。

コネクタを構成したら、**Done** をクリックします。

## アクション

| **アクション名** | **訪問プロファイル** | **イベントデータ** |
|---| ---| ---|
| オフラインコンバージョンを送信 | ✓ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

以下のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### オフラインコンバージョンを送信

#### バッチ制限

このコネクタは、ベンダーへの大量データ転送をサポートするために、リクエストをバッチ処理します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。以下のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに格納されます。

* リクエストの最大数：1000
* 最も古いリクエストからの最大経過時間：10 分
* リクエストの最大サイズ：1 MB

#### データプロバイダー ID

|**パラメータ**| **説明**|
|---| ---|
| Data Provider ID | TTD システム内のデータプロバイダー ID。この値は、The Trade Desk のテクニカルアカウントマネージャーから提供されます。 |

#### データ ID

* Trade Desk ID、デバイス広告 ID、Unified ID、または IdentityLink をマッピングします。
* 複数がマッピングされている場合は、Trade Desk ID、デバイス広告 ID、Unified ID、IdentityLink の優先順位で、最初の空でない ID が選択されます。
* デバイス広告 ID は、iOS IDFA または Android Advertising ID（AAID）で表されます。
* ダッシュを含めて 36 文字の GUID である、未加工（ハッシュ化されていない）の IDFA および AAID のみが受け入れられます。

|**パラメータ**| **説明**|
|---| ---|
| The Trade Desk ID（TDID）（`TDID`） | このユーザーの、ダッシュを含む 36 文字の The Trade Desk GUID。 |
| デバイス広告 ID（`DAID`） | このユーザーの未加工のデバイス ID。ダッシュを含む 36 文字の GUID 形式で送信されます。iOS IDFA または Android の AAID を使用します。 |
| Unified ID（`UID2`） | UID2 とも呼ばれる未加工の UID2 値。この値では大文字と小文字が区別されます。未加工の UID2 は、UID2 API を使用して生成および管理されます。 |
| UID2 トークン（暗号化された広告トークン） | 暗号化された UID2 広告トークン。このトークンでは大文字と小文字が区別されます。 |
| IdentityLink（`IDL`） | 49 文字または 70 文字の RampID（旧称 IdentityLink）。The Trade Desk 専用にマッピングされた LiveRamp の RampID である必要があります。 |

#### アイテムデータ

|**パラメータ**| **説明**|
|---| ---|
| Tracking Tag ID | （必須）Tracking tag API を使用して作成された Tracking tag ID。例：`abc1234` |
| Conversion Timestamp | （必須）UTC 形式のコンバージョン日時。オフラインコンバージョンが発生した時刻です。例：`2019-02-07T13:25:00Z` |
| Impression ID | ダッシュを含む 36 文字の未加工（ハッシュ化されていない）GUID。 |
| Monetary value | 金額。例：`0.02` |
| Monetary currency | 金額の通貨。例：`USD` |
| Country | 国。例：`United States`。 |
| Region | 地域。例：`New York`。 |
| Metro Area | 都市圏。例：`501` |
| City | 市区町村。例：`Brooklyn`。|
| Postal Code | 郵便番号。例：`'11223'`。 |
| Event Name | イベントタイプはパートナープラットフォームによって定義されます。詳細については、[The Trade Desk：イベントマッピング](https://partner.thetradedesk.com/v3/portal/data/doc/post-providerapi-offlineconversion#event-mapping)を参照してください。 |
| Order ID | トランザクションまたはコンバージョンイベントの一意の識別子。最大長は 64 文字です。 |

#### 追加データ

|**パラメータ**| **説明**|
|---| ---|
| `TD1 - TD10` | カテゴリやその他の分類に使用する任意のレポートフィールド。最大長は 64 文字です。|

#### 明細項目

マーチャントの商品カタログの明細情報を含むプロパティです。これらのマッピングでは、配列属性を使用できます。

|**パラメータ**| **説明**|
|---| ---|
| Item Code | アイテム識別子（SKU など）。 |
| Item Name | アイテムコードに関連付けられた名前。最大長は 150 文字です。 |
| Item Quantity | そのアイテムコードについて、注文に含まれるアイテムの数量。 |
| Item Price | アイテムの単価。 |
| Item Category | アイテムのカテゴリ ID。 |