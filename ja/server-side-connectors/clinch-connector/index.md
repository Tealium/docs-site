---
title: Clinchコネクタ構成ガイド
description: この記事では、Clinchコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/clinch-connector/
---
## API情報

このコネクタは、次のベンダーAPIを使用します。

* API名：Clinch API
* APIバージョン：1.0
* APIエンドポイント：`https://trkweb.clinch.co/trk`

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の項目を構成します。

* **クライアントID**  
  * （必須）クライアントID。（`cid`）
* **データソースID**  
  * （必須）データソースID。（`dsid`）

コネクタを構成したら、**完了**をクリックします。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| イベントを送信 | ✓ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### イベントを送信

#### 技術パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| `referrer` | イベントの発生元ページのURL。 |
| `timestamp` | UTCでのイベントのタイムスタンプ。 |
| `tcf` | IAB（Interactive Advertising Bureau）を使用したGDPR同意文字列。 |
| `user_ip` | ユーザーのIPアドレス。 |
| `user_agent` | ユーザーエージェント。 |

#### イベントタイプ

イベントタイプを選択します。次の値を使用できます。

| **イベントタイプ** | **説明** |
| --- | --- |
| `PageView` | ページビュー。 | 
| `HomePage` | ホームページの表示。|
| `Landing` | ランディングページの表示。|
| `Search` | 検索結果ページの表示。|
| `Category` | カテゴリページの表示。 |
| `Details` | 商品詳細ページの表示。|
| `DetailsExit` | 商品詳細ページからの離脱。 |
| `AddToCart` | カートへの追加。 |
| `RemFromCart` | カートからの削除。 |
| `CartPage` | カートページの表示。 |
| `AddToWishList`| ウィッシュリストへの追加。 |
| `Checkout` | チェックアウトの開始、またはチェックアウトの任意のステップ。 |
| `conv` | 購入、またはその他の個別のコンバージョンイベント。 | 
| `Registration` | 登録。コンバージョンとしても扱われます。 |
| `OfflineConv` | 店舗での購入などのオフラインコンバージョン。 |
| `Other` | その他のイベント。 |

#### イベントパラメータ

| **パラメータ** | **説明** |
| --- | --- |
| `stype` | イベントのセカンダリタイプ（通常はコンバージョンイベントで指定）。 |
| `product` | イベントに商品またはカテゴリが含まれる場合の商品タイプ。たとえば、`Ecommerce`、`Flight`、`Hotel`、`Package`、`Car`など。 |

#### IDパラメータ

| **パラメータ** | **説明** |
| --- | --- |
| クライアントエンコード済みID | クライアントエンコード済みID。指定しない場合、`clinchClickId`はスキップされます。 |
| `clinch-sid` | ClinchとのCookie同期によって取得するか、WebサイトのファーストパーティCookie `clinch-sid`から読み取ったClinch Cookie ID。 |
| `clinchClickId` | `clinchClickId_{client_enc_id}`に必要な値は、Cookie `clinchId_{client_enc_id}`のファーストパーティCookie値です。 |
| メールアドレス | （SHA256でハッシュ化済み）SHA256ですでにハッシュ化されているメールアドレスを指定します。 |
| メールアドレス | （SHA256ハッシュを適用）プレーンテキストのメールアドレスを指定します。コネクタは、この値の前後の空白を削除し、小文字に変換してから、SHA256を使用してハッシュ化します。 |
| `atsEnvelop` | LiveRamp Authenticated Traffic Solution（ATS）のエンベロープ。 |
| `uid2_0` | `UID2.0`識別子。 |
| `did` | ADIDやIDFAなど、リセット可能なモバイル広告ID。 |

#### コンテンツ（Eコマース）

| **パラメータ** | **説明** |
| --- | --- |
| `ids` | 表示された商品IDをカンマで区切った文字列。これらのIDは、商品フィード内の商品IDと一致する必要があります。 |
| `category` | 商品カテゴリ。この値は、商品フィード内のカテゴリと一致する必要があります。 |
| `recommended` | 推奨商品IDをカンマで区切った文字列。ユーザーが操作した商品ではなく、Webサイトまたはベンダーのレコメンデーションエンジンがユーザーに提案する可能性のある商品のIDです。これらの値は、商品フィード内の商品IDと一致する必要があります。 |
| `term` | 検索イベントの検索語句。 |

#### コンテンツ（旅行）

| **パラメータ** | **説明** |
| --- | --- |
| `from` | 出発地の都市または空港のデータコード。このコードは、商品フィード内の都市コードまたは空港コードと一致する必要があります。 |
| `to` | 目的地の都市または空港のデータコード。このコードは、商品フィード内の都市コードまたは空港コードと一致する必要があります。 |
| `depart` | `ISO 8601`形式の出発日。例：`2023-09-21`。 |
| `return` | `ISO 8601`形式の帰着日。例：`2023-09-21`。 |
| `city` | ホテル商品の都市コード。このコードは、ホテルフィード内の都市パラメータと一致する必要があります。 |
| `ids` | ホテルIDをカンマで区切ったリスト。 |

#### コンテンツ（自動車）

| **パラメータ** | **説明** |
| --- | --- |
| `postal_code` | 車両所在地の郵便番号。 |
| `make` | 車両のメーカー。 |
| `model` | 車両のモデル。 |
| `year` | 車両の製造年。 |
| `state_of_vehicle` | 車両の現在の状態。 |
| `exterior_color` | 車両の外装色。 |
| `transmission` | 車両のトランスミッションの種類。 |
| `body_style` | 車両のボディスタイル。 |
| `fuel_type` | 車両が使用する燃料の種類。 |
| `drivetrain` | 車両の駆動方式。 |
| `price` | 車両の価格。 |
| `preferred_price_range` | 車両の希望価格範囲。 |

#### 購入イベントパラメータ

| **パラメータ** | **説明** |
| --- | --- |
| `orderId` | 購入注文IDまたは確認ID。 |
| `amount` | 合計金額。 |
| `currency` | 3文字の通貨コード。 |

#### プライバシーと同意

| **パラメータ** | **説明** |
| --- | --- |
| `tcf_string` | GDPR TCF（Transparency and Consent Framework）文字列。 |
| `ccpa_string` | CCPAプライバシー文字列。このパラメータは非推奨であり、Global Privacy Platform（GPP）に置き換えられました。代わりに`gpp_string`を使用してください。 |
| `gpp_string` | GPP同意文字列。 |

#### その他

1つ以上の属性を選択します。コネクタは、これらの属性をカンマ区切りのリストとしてClinchのユーザープロファイルに送信します。

## 例

### Eコマースカテゴリの例

次の表は、ユーザーがオンラインストアのカテゴリページを表示したイベントのパラメータ例を示しています。カテゴリは`mens-shoes`で、ユーザーは3つの商品を表示しています。このイベントには、ハッシュ化されたメール識別子`hem`が含まれています。

| パラメータ | 値の例 |
| --------- | ------------- |
| `cid`| `ter634` |
| `dsid`| `53ter45` |
| `product`| `ecommerce` |
| `type`| `Category` |
| `ids`| `111,222,333` |
| `timestamp`| `1664064000` |
| `hem`| `a64d47276a22f4eb7ee9e4203d2c627d` |
| `referrer`| `https://myonlinestore.com/category/mens-shoes` |

### 自動車カテゴリの例

次の表は、ユーザーがWebサイト上の自動車ページを表示し、カテゴリが`car`であるイベントのパラメータ例を示しています。このイベントには、ハッシュ化されたメール識別子`hem`が含まれています。

| パラメータ | 値の例 |
| --------- | ------------- |
| `cid` | `ogv7Q1` |
| `dsid` | `whbb7YK` |
| `product` | `car` |
| `timestamp` | `1664064000` |
| `type` | `details` |
| `ids` | `123ABC456,789SDX023` |
| `postal_code` | `90210` |
| `make` | `Toyota` |
| `model` | `Corolla` |
| `year` | `2020` |
| `state_of_vehicle` | `New` |
| `exterior_color` | `Blue` |
| `transmission` | `Automatic` |
| `body_style` | `Sedan` |
| `fuel_type` | `Gasoline` |
| `drivetrain` | `FWD` |
| `price` | `20000` |
| `currency` | `USD` |
| `preferred_price_range` | `[15000, 25000]` |
| `hem` | `a64d47276a22f4eb7ee9e4203d2c627d` |