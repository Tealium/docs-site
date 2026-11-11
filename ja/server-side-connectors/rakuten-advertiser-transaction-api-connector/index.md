---
title: Rakuten Advertiser Transaction APIコネクタ構成ガイド
description: アフィリエイトトランザクションをレポートするためのRakuten Advertiser Transaction APIコネクタを構成します。
url: https://docs.tealium.com/ja/server-side-connectors/rakuten-advertiser-transaction-api-connector/
---


## API情報

このコネクタは、次のベンダーAPIを使用します。

* API名：Rakuten Advertiser Transactions API
* APIバージョン：v1
* APIエンドポイント：`https://api.linksynergy.com`
* ドキュメント：[Rakuten Advertising開発者ポータル](https://developers.rakutenadvertising.com/)

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の構成を行います。

* **Rakuten Advertiser ID：** Rakuten Advertiser ID。
* **Client ID：** Rakutenから提供されたOAuthクライアントID。
* **Client Secret：** Rakutenから提供されたOAuthクライアントシークレットキー。

コネクタを構成したら、**Done**をクリックします。

このコネクタは、OAuth 2.0クライアントクレデンシャル認証を使用します。クライアントIDとクライアントシークレットを、`https://api.linksynergy.com/token`でベアラートークンと交換します。ベアラートークンの有効期限は4時間です。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| トランザクションを送信 | ✗ | ✓ |
| 返金を送信 | ✗ | ✓ |

### トランザクションを送信

#### 注文データ

| パラメータ | 説明 |
| --- | --- |
| Transaction Timestamp | ユーザーがオンライン上でコミッション対象のアクションを完了したUTC時刻（ISO 8601形式：`YYYY-MM-DDTHH:MM:SS.SSSZ`）。マッピングされていない場合は、デフォルトでイベントのタイムスタンプが使用されます。 |
| Order ID | （必須）一意の注文ID。トランザクションに関する問い合わせへの回答に使用できるよう、できれば消費者にも表示されるIDを指定してください。 |
| Currency | （必須）注文の通貨コード。 |
| Click ID | リンクレスでレポートしない場合は必須。リダイレクト時または最終ランディングページでRakutenから送信される34文字のID。 |
| Landing Timestamp | リンクレスでレポートしない場合は必須。ユーザーがサイトにアクセスしたUTC時刻。このタイムスタンプはTransaction Timestampより前である必要があります。 |

#### 任意の注文データ

| パラメータ | 説明 |
| --- | --- |
| Alternative Order ID | レポートされた注文IDの代替バージョン。 |
| Commission Reason | トランザクションに対してコミッションが支払われない理由。Is Commissionableと併用します。 |
| Consumed Datetime | 予約されたサービスが利用された日付。 |
| Consumer Country | 消費者が居住する国。 |
| Consumer Operating System | コミッション対象のアクションが行われた時点での、消費者のデバイスのオペレーティングシステム。 |
| Consumer Region | 消費者が居住する地域。 |
| Conversion Type | 広告主が使用するコンバージョンアトリビューション方式。例：`post click`。 |
| Coupon | トランザクションで使用されたクーポンコードまたは割引コード。 |
| Credit Card Type | 購入に使用されたクレジットカードの種類。 |
| Customer ID | 顧客を表すID。 |
| Customer Rank | 顧客に割り当てられた広告主のランクまたはスコア。 |
| Customer Segment | 広告主が顧客に割り当てたセグメント。 |
| Customer State | 顧客が居住する州。 |
| Customer Status | 広告主が顧客に割り当てたステータス。例：`new`、`existing`。 |
| Event Datetime | イベントの日時。例：コンサート、スポーツイベント。 |
| Mobile Device ID | モバイルデバイスの広告ID。 |
| Order Status | 注文のステータス。 |
| Purchase Site | 購入先のドメイン。 |
| Tracking Source | トラッキングデータがRakutenに送信された方法。 |
| Traffic Source | コンバージョンイベントを発生させたトラフィックのソース。 |

#### 商品データ

| パラメータ | 説明 |
| --- | --- |
| Product Prices | （必須）商品価格のリスト。デフォルトでは、コネクタは送信前に各価格に対応する数量を乗算します。価格値を変更せずに送信するには、**Disable product prices calculation**チェックボックスをオンにします。 |
| Product SKUs | （必須）商品のSKUのリスト。 |
| Product Quantities | （必須）商品の数量のリスト。 |
| Product Names | （必須）商品名のリスト。 |

#### 任意の商品データ

| パラメータ | 説明 |
| --- | --- |
| Product Brands | 商品ブランドのリスト。 |
| Product Categories | 商品カテゴリのリスト。テンプレートを使用して、Rakuten向けの、より複雑な商品別カテゴリ配列を作成します。 |
| Product Category IDs | 商品カテゴリIDのリスト。テンプレートを使用して、Rakuten向けの、より複雑な商品別カテゴリ配列を作成します。 |
| Product Coupons | 商品単位のクーポンのリスト。 |
| Product IDs | 商品IDのリスト。 |
| Higher Commission Rates | より高いコミッション率が適用される商品を示すブール値のリスト。 |
| Product Sequences | 出荷に含まれる商品の順序を識別するリスト。 |
| Product Statuses | 商品ステータスのリスト。 |
| Is Commissionable | 各商品がコミッション対象かどうかを示すブール値のリスト。 |
| Product Margins | 商品単位のマージンのリスト。 |
| Marketplace Stores | マーケットプレイス環境で販売が行われたストアのリスト。 |
| Marketplace Store IDs | マーケットプレイス環境で販売が行われたストアIDのリスト。 |
| Is Tax Exempt | 各商品が免税対象かどうかを示すブール値のリスト。 |

#### 商品価格の計算を無効にする

Rakutenでは、商品価格を価格×数量として指定する必要があります。コネクタはこの計算を自動的に実行します。マッピングされた価格値を変更せずに送信するには、このチェックボックスをオンにします。

### 返金を送信

#### 返金データ

| パラメータ | 説明 |
| --- | --- |
| Transaction Timestamp | ユーザーが元のコミッション対象アクションを完了したUTC時刻（ISO 8601形式：`YYYY-MM-DDTHH:MM:SS.SSSZ`）。マッピングされていない場合は、デフォルトでイベントのタイムスタンプが使用されます。 |
| Order ID | （必須）返金対象トランザクションの一意の注文ID。 |
| Currency | （必須）注文の通貨コード。 |
| Click ID | （必須）リダイレクト時または最終ランディングページでRakutenから送信される34文字のID。 |
| Landing Timestamp | （必須）ユーザーがサイトにアクセスしたUTC時刻。このタイムスタンプはTransaction Timestampより前である必要があります。 |

#### 商品データ

| パラメータ | 説明 |
| --- | --- |
| Product Prices | （必須）商品価格のリスト。Rakutenの返金API要件に従い、コネクタは商品の金額を負の数として送信します。デフォルトでは、符号を変更する前に、各価格に対応する数量も乗算します。この乗算を無効にするには、**Disable product prices calculation**チェックボックスをオンにします。 |
| Product SKUs | （必須）商品のSKUのリスト。 |
| Product Quantities | （必須）商品の数量のリスト。 |
| Product Names | （必須）商品名のリスト。 |

#### 商品価格の計算を無効にする

Rakutenでは、商品価格を価格×数量として指定する必要があります。コネクタはこの計算を自動的に実行します。マッピングされた価格値を変更せずに送信するには、このチェックボックスをオンにします。

## 業種別の任意データ

Rakuten Advertising APIは、コネクタUIで名前付きパラメータとして使用できない、業種固有の任意データフィールドをサポートしています。これらのフィールドを送信するには、任意データをサポートする任意のコネクタアクションで、APIフィールド名をマッピングキーとして使用し、カスタムマッピングとして追加します。
### 金融

| APIフィールド | 説明 | 使用レベル |
| --- | --- | --- |
| `autopay` | 消費者が支払いを自動化するためにアカウントを構成したかどうかを示します。 | 注文レベル |
| `customer_segment_group` | 広告主が定義した、ユーザーを5つのグループのいずれかに分類するセグメントです。レポートでは五分位スコアとして表示されます。 | アイテムレベル |
| `designated_marketing_area` | 消費者向けオファーの指定マーケティング地域のIDです。 | 注文レベル |
| `estimated_aum` | アカウント開設後の消費者の推定運用資産額です。 | 注文レベル |
| `funded_amount` | 開設された各アカウントの更新後の合計残高です。 | アイテムレベル |
| `funded_amount_range` | 開設されたアカウントの残高を表す、広告主が定義した範囲です。 | アイテムレベル |
| `home_ownership` | 申請者が提出した住宅所有状況です。 | 注文レベル |
| `income_aum` | オンボーディング中に消費者が入力した所得に基づき、広告主が定義した運用資産額です。 | 注文レベル |
| `income_band` | 申請者が提出した所得のコード値です。 | 注文レベル |
| `loan_amount_requested` | 申請者が希望する融資額です。 | 注文レベル |
| `loan_approval_datetime` | 融資の承認日です。 | 注文レベル |
| `loan_apr` | 融資の年率（APR）です。 | 注文レベル |
| `loan_funded_datetime` | 融資の実行日です。 | 注文レベル |
| `loan_model_number` | オファーの提示に使用された事前審査モデルのモデル番号です。 | 注文レベル |
| `loan_offer_apr` | 事前審査モデルによって予測された融資の年率（APR）です。 | 注文レベル |
| `loan_offer_badge` | 事前審査モデルによって予測されたオファーのバッジタイプです。 | 注文レベル |
| `loan_offer_term` | 事前審査モデルによって予測された融資期間です。 | 注文レベル |
| `loan_origination_fee` | 融資の組成手数料です。 | 注文レベル |
| `loan_purpose` | 広告主が定義した融資目的です。 | 注文レベル |
| `loan_purpose_applicant` | 申請者が提出した融資目的のコード値です。 | 注文レベル |
| `loan_term_in_months` | 融資期間の月数です。 | 注文レベル |
| `monthly_housing_payment` | 申請者が提出した月額ホーム賃または住宅費のコード値です。 | 注文レベル |
| `publisher_lead_id` | 成約した融資をパブリッシャー側の記録と照合するために、パブリッシャーが生成したIDです。 | 注文レベル |

### 小売

| APIフィールド | 説明 | 使用レベル |
| --- | --- | --- |
| `artist_curation_id` | 顧客向けに商品をカスタマイズして選定する際に使用されるアーティストのIDです。 | 注文レベル |
| `commission_estimate` | マーケットプレイス広告主の推定コミッションです。パブリッシャーには表示されません。 | 注文レベル |
| `credit_card_last_four` | クレジットカード番号の下4桁です。カード連携オファーの識別子として使用されます。 | 注文レベル |
| `discount_amount` | 注文レベルで適用された割引額です。 | 注文レベル |
| `discount_amount` | アイテムレベルで適用された割引額です。 | アイテムレベル |
| `discount_type` | 注文レベルで使用された割引の種類です。 | 注文レベル |
| `discount_type` | アイテムレベルで使用された割引の種類です。 | アイテムレベル |
| `is_clearance` | 商品が在庫処分対象かどうかを示します。 | アイテムレベル |
| `is_marketplace` | アイテムがマーケットプレイスの商品かどうかを示します。 | アイテムレベル |
| `is_sale` | 商品がセール対象かどうかを示します。 | アイテムレベル |
| `markdown_rate` | アイテムの値下げ率です。0～100の値で表されます。 | アイテムレベル |
| `marketplace_store` | マーケットプレイス環境で販売が行われた加盟店の店舗名です。 | アイテムレベル |
| `marketplace_store_id` | マーケットプレイス環境で販売が行われた加盟店の店舗IDです。 | アイテムレベル |
| `o2o_bank_partner` | カード連携オファーのトラッキングに使用される提携銀行の名前です。 | 注文レベル |
| `o2o_store_address` | 店舗の住所です。 | 注文レベル |
| `o2o_store_city` | 店舗が所在する市区町村です。 | 注文レベル |
| `o2o_store_country` | 店舗が所在する国です。 | 注文レベル |
| `o2o_store_id` | 店舗IDです。 | 注文レベル |
| `o2o_store_name` | 店舗名です。 | 注文レベル |
| `o2o_store_state` | 店舗が所在する州です。 | 注文レベル |
| `o2o_store_zip` | 店舗所在地のZIPコードまたは郵便番号です。 | 注文レベル |
| `ship_country` | 注文の配送先の国です。 | 注文レベル |
| `shipment_id` | 一緒に発送または返品されるアイテムのグループを識別するIDです。 | アイテムレベル |
| `shipped_datetime` | アイテムが発送された日時、または発送予定日時です。 | 注文レベル |
| `store_category` | 購入が行われた店舗を表すカテゴリーです。 | 注文レベル |
| `store_id` | 購入が行われた店舗のIDです。 | 注文レベル |
| `subscription_id` | 商品サブスクリプションプランのIDです。 | アイテムレベル |
| `subscription_name` | 商品サブスクリプションプランの名前です。 | アイテムレベル |

### 旅行

| APIフィールド | 説明 | 使用レベル |
| --- | --- | --- |
| `accommodation_type` | 宿泊施設の種類です。 | アイテムレベル |
| `cancel_deadline_datetime` | 旅行者が予約をキャンセルできる期限です。 | 注文レベル |
| `check_in_datetime` | 旅行者のチェックイン日です。 | 注文レベル |
| `check_out_datetime` | 旅行者のチェックアウト日です。 | 注文レベル |
| `consumed_datetime` | 予約されたサービスが利用された日です。 | 注文レベル |
| `departure_country` | 旅行者が旅を開始する国です。 | アイテムレベル |
| `departure_location` | 都市、空港、クルーズ港など、旅行者が旅を開始する場所です。 | アイテムレベル |
| `destination_country` | 旅行者が旅を終える国です。 | アイテムレベル |
| `destination_location` | 都市、空港、クルーズ港など、旅行者が旅を終える場所です。 | アイテムレベル |
| `discount_amount` | 注文レベルで適用された割引額です。 | 注文レベル |
| `discount_amount` | アイテムレベルで適用された割引額です。 | アイテムレベル |
| `discount_type` | 注文レベルで使用された割引の種類です。 | 注文レベル |
| `discount_type` | アイテムレベルで使用された割引の種類です。 | アイテムレベル |
| `fare_type` | ファーストクラス、ビジネスクラス、エコノミークラスなどの旅行運賃タイプです。 | アイテムレベル |
| `is_weekend` | 予約期間が週末にかかっていたかどうかを示します。 | 注文レベル |
| `number_of_rooms` | 予約した客室数です。 | アイテムレベル |
| `paid_in_loyalty_points` | 顧客がロイヤルティポイントを使用して支払ったかどうかを示します。 | アイテムレベル |
| `property_type` | ホテルやモーテルなどの宿泊施設の種類です。 | アイテムレベル |
| `reservation_end_datetime` | 予約の終了日です。 | 注文レベル |
| `reservation_length_in_days` | 予約日数です。 | 注文レベル |
| `reservation_region` | 旅行予約に関連付けられた地域です。広告主が複数の拠点を持つ場合に役立ちます。 | アイテムレベル |
| `reservation_start_datetime` | 予約の開始日です。 | 注文レベル |
| `travel_reason` | 個人旅行や出張などの旅行目的です。 | 注文レベル |
| `travel_type` | 航空便、クルーズ、ホテル、レンタカー、アクティビティなどの旅行予約の種類です。 | アイテムレベル |
| `vehicle_type` | プレミアム、スタンダード、コンパクトなど、レンタカーに関連付けられた車両タイプです。 | アイテムレベル |