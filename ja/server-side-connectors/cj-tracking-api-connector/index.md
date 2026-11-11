---
title: CJ Tracking APIコネクタ構成ガイド
description: この記事では、CJ Tracking APIコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/cj-tracking-api-connector/
---
CJでは、WebトラッキングイベントにUniversal TagとTracking APIを併用することを推奨しています。これは、それぞれがCJのサービスをサポートまたはエンリッチメントするためです。Tracking APIを使用するには、CJ側でバックエンドの変更が必要となるため、Client Integrationチームとの連携が必要です。詳細については、CJアカウントチームまたは`support@cj.com`にお問い合わせください。

## API情報

このコネクタでは、次のベンダーAPIを使用します。

* API名：CJ API
* APIエンドポイント：
    * トレースなし（本番エンドポイント）：`https://tracking.api.cj.com/graphql/`
    * トレースあり（テストエンドポイント）：`https://tracking.api.cj.com/graphqltest/`
* ドキュメント：[CJ API](https://developers.cj.com/graphql/reference/private/Tracking)

## バッチ制限

このコネクタでは、ベンダーへの大量のデータ転送に対応するため、バッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに格納されます。

* リクエストの最大数：10,000
* 最も古いリクエストからの最大経過時間：10分
* リクエストの最大サイズ：100 MB

## コネクタアクション

| **アクション名** | **訪問プロファイル** | **イベントデータ** |
|:----------------|:-------------------|:----------------|
| 注文データの送信 | ✗  | ✓ |
| 注文の修正データを送信 | ✗ | ✓ |
| 注文のキャンセルを送信 | ✗ | ✓ |

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/ja/server-side/connectors/manage/)の記事を参照してください。

コネクタを追加した後、次の構成を構成します。

* **Personal Access Token**  
（必須）CJ Tracking APIのパーソナルアクセストークン。[CJのパーソナルアクセストークン](https://developers.cj.com/account/personal-access-tokens)ページに移動してアカウントにログインし、パーソナルアクセストークンを生成します。

コネクタの構成が完了したら、**完了**をクリックします。

## アクション構成 — パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### アクション — 注文データの送信
#### パラメーター

| **パラメーター**  | **送信先**  | **説明** |
|:----------|:-----------|:---------------|
| エンタープライズID | `enterpriseId`  | （必須）CJのクライアント統合チームによって割り当てられる一意のクライアントID。 |
| アクショントラッカーID | `actionTrackerId` | （必須）実行されたアクションに対してCJのクライアント統合チームから提供される固定値。 |
| CJイベント | `ciEvent` | （必須）CJが定義する、イベントを関連付けるためのID（CJクリックIDとも呼ばれます）。 |
| 注文ID | `orderId` | （必須）クライアントが定義する注文識別子。 |
| イベント時刻 | `eventTime` | （必須）イベントのタイムスタンプ。 |
| 注文金額 | `amount`  | （必須）注文の合計金額。 |
| 注文の割引額 | `discount`  | 注文に適用された割引額。 |
| クーポンコード | `coupon`  | 注文に適用されたクーポンコード。 |
| 通貨 | `currency`  | 注文で使用された通貨。 |
| 商品価格 | `unitPrice` | 注文に含まれる各商品の単価の配列。 |
| 商品SKU | `sku` | 注文に含まれる各商品のSKUの配列。 |
| 商品数量 | `quantity`  | 各商品の注文数量の配列。 |
| 商品の割引額 | `discount`  | 商品の単価に適用された割引額の配列。 |
| 広告主の業種 |   | サポートされる値は、`Retail`、`Finance`、`Travel`、`NetworkServices`です。 |
| 付随支出額 | `ancillarySpend`  | 取引に伴う付随支出額（広告主専用属性）。 |
| 年会費 | `annualFee` | この商品に関連付けられた年会費。 |
| 申請ステータス | `applicationStatus` | 取引がCJに送信された時点での申請ステータスを示します。 |
| APR | `apr` | 申請承認時のAPR。 |
| 残高移行APR | `aprTransfer` | 残高移行に対するAPR。 |
| 残高移行APR期間 | `aprTransferTime` | 残高移行APRの適用期間（月単位）。 |
| 予約日 | `bookingDate` | 予約が行われた日付。形式は`YYYY-MM-DD`です。 |
| 予約ステータス | `bookingStatus` | 予約のステータス。例：`confirmed`、`pending`など。 |
| 税引後予約金額 | `bookingValuePostTax` | 税金適用後の予約金額。 |
| 税引前予約金額 | `bookingValuePreTax`  | 税金適用前の予約金額。 |
| ブランド | `brand` | 購入された商品のブランド。 |
| ブランドID | `brandId` | 予約された商品のブランド識別子。 |
| ビジネスユニット | `businessUnit`  | 顧客が購入に利用したビジネスユニット。 |
| キャンペーンID | `campaignId`  | 広告主固有のマーケティングキャンペーンID。 |
| キャンペーン名 | `campaignName`  | 広告主固有のマーケティングキャンペーン名。 |
| カードカテゴリー | `cardCategory`  | カードカテゴリーの名前。 |
| 車両オプション | `carOptions`  | 取引時に選択されたその他の車両オプション。例：`insurance`。 |
| キャッシング手数料 | `cashAdvanceFee`  | この商品に関連付けられたキャッシング手数料。 |
| カテゴリー | `category`  | 商品のカテゴリー。たとえば、顧客が個人向けキャッシュバッククレジットカードに申し込む場合：`service_type=cc&item_type=personal&category=cashback`）。 |
| 市区町村 | `city`  | ホテルまたはイベントの所在地の市区町村名。 |
| クラス | `class` | 予約または購入された商品のクラス評価。 |
| 確認番号 | `confirmationNumber`  | プロバイダーの確認番号。たとえば、航空会社が発行するフライト確認番号。 |
| 契約期間 | `contractLength`  | 契約期間（月単位）。 |
| 契約タイプ | `contractType`  | 広告主固有の契約の説明。 |
| 国コード | `countryCode` | 取引が行われた国。 |
| クーポン割引額 | `couponDiscount`  | 使用されたクーポンによる割引額。 |
| クーポンタイプ | `couponType`  | 使用されたクーポンのタイプ。 |
| 与信限度額 | `creditLine`  | 顧客に供与された与信額。 |
| 信用度 | `creditQuality` | 顧客の信用度。サポートされる値は、300～579＝非常に低い、580～669＝普通、670～739＝良好、740～799＝非常に良好、800～850＝極めて良好です。 |
| 信用調査レポート | `creditReport`  | 顧客が信用調査レポートを受領または購入したか、無料レポートを取得したか、あるいはレポートサービスのトライアルを開始したかを示します。 |
| クルーズタイプ | `cruiseType`  | クルーズのタイプ。例：`Alaskan`、`Caribbean`など。 |
| 顧客の国 | `customerCountry` | 購入する顧客が所在する国。ISO 3166-1 alpha-2国コードを使用します。例：`US`、`UK`、`AU`、`FR`。 |
| 顧客セグメント | `customerSegment` | 広告主固有の顧客セグメント。 |
| 顧客ステータス | `customerStatus`  | 顧客が新規顧客か既存顧客かを示します。 |
| 顧客タイプ | `customerType`  | 顧客のタイプ。例：`company`、`individual consumer`、`business`、`leisure`。 |
| 配送 | `delivery`  | 配送方法。 |
| 説明 | `description` | 商品またはカードの説明。 |
| 目的地の市区町村 | `destinationCity` | 目的地の市区町村名。 |
| 目的地の国 | `destinationCountry`  | サービスの目的地となる国。ISO 3166-1 alpha-2国コードを使用します。例：`US`、`UK`、`AU`、`FR`。 |
| 目的地ID | `destinationId` | サービスの目的地ID。通常は、目的地の市区町村または州／県を表す、広告主が定義したコードです。例：`728660`。 |
| 目的地の州 | `destinationState`  | サービスの目的地となる州／県。ISO 3166-2の州コードを使用します。 |
| 国内 | `domestic`  | 顧客が米国に居住しているかどうかを示します。 |
| 返却場所のIATAコード | `dropoffIata` | 返却場所が空港の場合、その場所のIATAコード。 |
| 返却場所ID | `dropoffId` | 返却場所にあるレンタカー営業所の一意のID。 |
| 期間 | `duration`  | イベントまたは商品の期間（日単位）。ホテルの宿泊日数やトライアルサブスクリプションの期間など。 |
| 終了日時 | `endDateTime` | チェックアウト日時、出発日時など。 |
| 航空運賃タイプ | `flightFareType`  | 航空運賃のタイプ。例：`Gotta Get Away`。 |
| フライトオプション | `flightOptions` | フライトパッケージで選択されたその他のオプション。例：`wiki`。 |
| フライトタイプ | `flightType`  | フライトのタイプ。例：`direct`、`layover`、`overnight`。 |
| フライトマイル | `flyerMiles`  | このフライトでフライトマイルを獲得したかどうかを示します。 |
| 入金額 | `fundedAmount`  | アカウントへの入金額。 |
| 入金通貨 | `fundedCurrency`  | アカウントへの初回入金に使用された通貨。 |
| ジャンル | `genre` | エンターテインメントのカテゴリーまたはジャンル。例：`books`、`movies`、`streaming`、`music`など。このパラメーターは取引レベルでのみ使用できます。 |
| ゲスト数 | `guests`  | ゲストの人数。 |
| IATA | `iata`  | フライトスケジュールに含まれる各都市のコードをカンマ区切りで指定します。カンマはURLエンコードする必要があります。 |
| 導入時APR | `introductoryApr` | 購入に対する導入時APR。導入時APRが通常のAPRと異ならない場合は、**APR**パラメーターを使用します。 |
| 導入時APR期間 | `introductoryAprTime` | 導入時APRの適用期間（月単位）。 |
| 商品ID | `itemId`  | 購入された商品のID。複数の商品がある場合、このパラメーターではカンマ区切りのリストを使用します。 |
| 商品名 | `itemName`  | 購入された商品の名前。 |
| 商品タイプ | `itemType`  | 商品のタイプ。たとえば、顧客が個人向けキャッシュバッククレジットカードに申し込む場合：`service_type=cc&item_type=personal&category=cashback`）。 |
| 旅程ID | `itineraryId` | 予約旅程ID。 |
| ライフステージ | `lifestage` | カードがどのように、またなぜ使用されるかを示す一般的な顧客属性（転居したばかりの人、学生、中小企業など）。 |
| 所在地 | `location`  | 顧客が訪問する、または訪問した店舗や場所を識別するために使用できる、広告主固有のIDまたは名前。 |
| 獲得ロイヤルティ | `loyaltyEarned` | 顧客のロイヤルティステータスのレベル。 |
| ロイヤルティ初回登録 | `loyaltyFirstTimeSignup`  | この注文によって消費者がロイヤルティプログラムに参加したかどうか。 |
| ロイヤルティレベル | `loyaltyLevel`  | ロイヤルティポイントが使用されたかどうか。 |
| ロイヤルティ獲得 | `loyaltyRedeemed` | ロイヤルティポイントが獲得されたかどうか。 |
| ロイヤルティステータス | `loyaltyStatus` | 顧客の会員ステータス。 |
| 利益率 | `margin`  | 取引の利益率を示す、広告主専用の属性。 |
| マーケティングチャネル | `marketingChannel`  | マーケティングチャネル。 |
| 最低残高 | `minimumBalance`  | 口座に必要な最低現金残高の値。 |
| 最低入金額 | `minimumDeposit`  | 最低入金額。 |
| 最低滞在日数 | `minimumStayDuration` | 必要な最低滞在日数（日単位）。 |
| キャンセル不可 | `noCancellation`  | 取引にキャンセル不可ポリシーが適用されるかどうか。`yes` または `no`。 |
| 注文小計 | `orderSubtotal` | 注文の小計。 |
| 出発都市 | `originCity`  | ニューヨークなど、サービスの出発都市名。 |
| 出発国 | `originCountry` | ISO 3166-1 alpha 2の国コード形式で指定された、サービスの出発国コード。例：`US`、`UK`、`AU`、`FR`。 |
| 出発州 | `originState` | ISO 3166-2の州コード形式で指定された、サービスの出発州／都道府県。 |
| 予約時支払額（税引後） | `paidAtBookingPostTax`  | 予約時に支払われた税込金額。 |
| 予約時支払額（税引前） | `paidAtBookingPreTax` | 予約時に支払われた税引前金額。 |
| 支払いモデル | `paymentMethod` | 使用された支払いモデル。例：`advertiser-specific`。 |
| 乗車場所のIATAコード | `pickupIata`  | 空港の乗車場所を表すIATAコード。 |
| 乗車場所ID | `pickupId`  | 乗車に使用されるレンタカー会社の一意な拠点ID。 |
| プラットフォームID | `platformId`  | 顧客が使用しているデバイス。例：`mobile`、`tablet` など。 |
| 販売地点 | `pointOfSale` | 顧客の販売地点。 |
| 港 | `port`  | クルーズの出発港。 |
| 予約販売 | `preorder`  | 商品が販売可能になる前に顧客が購入したかどうか。 |
| 前払い | `prepaid` | 顧客が取引金額を前払いしたかどうか。`yes` または `no`。 |
| 事前審査通過 | `prequalify`  | 申込者がカードの事前審査を通過したかどうか。 |
| プロモーション | `promotion` | 適用されたプロモーション。例：`summer sale`。 |
| プロモーション金額 | `promotionAmount` | プロモーションに関連付けられた数値金額。たとえば、プロモーションが500ドルのキャッシュバックの場合、この値は `promotion=dollars&promotion_amt=500`） |
| プロモーション条件のしきい値 | `promotionConditionThreshold` | 割引を受けるために必要なしきい値。 |
| プロモーション条件タイプ | `promotionConditionType`  | プロモーション条件のタイプ。 |
| プロモーション終了日時 | `promotionEnds` | ISO 8601規格の形式で指定されたプロモーションの終了日時。例：`2022-12-25T15:30:50.111Z`。 |
| プロモーション開始日時 | `promotionStarts` | ISO 8601規格の形式で指定されたプロモーションの開始日時。例：`2022-12-25T15:30:50.111Z`。 |
| プロモーションタイプ | `promotionType` | プロモーションのタイプ。 |
| 数量 | `quantity`  | 指定されたSKUの数量（シンプルアクションのみ）。アイテムベースのアクションを使用している場合は、`QTYx` を使用します。 |
| 評価 | `rating`  | 予約または購入されたアイテムの星評価。 |
| 客室タイプ | `roomType`  | ホテルまたはクルーズで予約された客室のタイプ。 |
| 客室数 | `rooms` | 予約された客室数。 |
| サービスタイプ | `serviceType` | 顧客が申し込んだ、または購入した金融サービスのタイプ。 |
| 船名 | `shipName`  | クルーズ船の名前。 |
| 開始日時 | `startDateTime` | 予約または購入されたアイテムのチェックイン日時、到着日時、または同様の開始日時。 |
| 州 | `state` | 店舗が所在する州または都道府県を、ISO 3166-2の州コード形式で定義します。たとえば、アラスカ州のコードは `US-AK`、バンコクは `TH-10` です。 |
| サブスクリプション料金 | `subscriptionFee` | 無料トライアルへの登録時に表示されるサブスクリプション料金。 |
| サブスクリプション期間 | `subscriptionLength`  | 製品の利用期間。例：`indefinite`、`1 month`、`3 months`、`6 months`）。 |
| 税額 | `taxAmount` | 税額。 |
| 税タイプ | `taxType` | 税のタイプ。 |
| 振込手数料 | `transferFee` | クレジットカードの振込手数料額。 |
| 旅行タイプ | `travelType`  | 予約される旅行のタイプ。例：`air`、`car`、`activities`、`cruise`、`events`、`hotel`、`package`、`restaurants`、`travel guides`、`vacation rental`、`other`。 |
| 旅程タイプ | `tripType`  | 予約または購入された旅程のタイプ。例：片道、往復、複数都市、往復とホテル。 |
| アップセル | `upsell`  | 顧客がトライアルからサブスクリプションに移行したかどうか。 |
| CJユーザー |   | CJユーザーID。 |

### アクション - 注文の再提示を送信する

このアクションを使用すると、注文の再提示をCJ Trackingに送信できます。注文の再提示では、まだロックまたはクローズされていないコミッション対象の注文について、属性を変更または追加できます。このアクションは注文の現在の状態を完全に上書きし、再提示で指定された情報のみが含まれるように注文を更新します。

#### パラメーター

| パラメーター | 送信先 | 必須？ | 説明 |
|----------------------------|-------------------|-----------|-------------|
| エンタープライズID | `enterpriseId`      | 必須 | CJのClient Integrationチームによって割り当てられる一意のクライアントID。 |
| アクショントラッカーID | `actionTrackerId`   | 必須 | 実行されたアクションについて、CJのClient Integrationチームから提供される静的な値。 |
| 注文ID | `orderId`           | 必須 | クライアントが定義する注文識別子。 |
| 更新日時 | `updateTime`        | 必須 | UTCオフセットのゾーン指定子として `Z` を使用し、JSONでは文字列として表現されるUTC ISO 8601形式の日時。例：`1970-03-27T12:13:14-05:00` または `1970-03-27T12:18:14Z`。 |
| CJイベント | `cjEvent`           | 任意 | CJが定義する、関連付け用のイベントID（CJクリックIDとも呼ばれます）。 |
| 注文金額 | `amount`            | 任意 | 注文の合計金額。 |
| 注文割引 | `discount`          | 任意 | 注文に適用された割引。 |
| 業種別パラメーター | `verticalParameters` | 任意 | 再提示に関連する特定の業種を記録するための追加情報。 |
| カスタムパラメーター | `customParameters`  | 任意 | 配列内にアイテムが存在する場合、値をnullにすることはできません。 |
| アイテム | `items`             | 任意 | 配列内にアイテムが存在する場合、値をnullにすることはできません。 |
| クーポンコード | `coupon`            | 任意 | 注文に適用されたクーポンコード。 |
| 通貨 | `currency`          | 任意 | 注文に使用された通貨。例：`USD`。 |
| チャネルのバイパス | `bypassChannel`     | 任意 | 取引のアトリビューションプロセスをカスタマイズします。例：`Channel=CJ`。値には次のいずれかを指定できます：<ul><li>`CJ`</li><li>`Direct`</li><li>`Affiliate_other`</li><li>`Display`</li><li>`Social`</li><li>`Search`</li><li>`Email`</li><li>`Other` |
| ステータス | `status`            | 任意 | 注文のステータス。値には `Pending` または `Accepted` を指定できます。 |
| 修正理由 | `correctionReason`  | 任意 | 値には次のいずれかを指定できます：<ul><li>`InvalidCreditCard`</li><li>`UnqualifiedLead`</li><li>`CannotShipSoldOut`</li><li>`DuplicateOrder`</li><li>`ReturnedMerchandise`</li><li>`Other`</li></ul> |

### アクション - 注文のキャンセルを送信する

このアクションは、既存の注文をキャンセルし、その注文に対するコミッションまたは手数料を支払わないことをCJに通知します。この概念は、CJが従来「完全修正」と呼んでいたものに似ています。
#### パラメーター

| パラメーター             | 送信先      | 必須か | 説明 |
|-----------------------|-----------------|-----------|-------------|
| エンタープライズID        | `enterpriseId`    | 必須  | CJのクライアントインテグレーションチームによって割り当てられた一意のクライアントID。 |
| アクショントラッカーID    | `actionTrackerId` | 必須  | 実行されたアクションに対して、CJのクライアントインテグレーションチームから提供される固定値。 |
| 注文ID            | `orderId`        | 必須  | クライアントが定義する注文識別子。 |
| 更新日時        | `updateTime`      | 必須  | UTCオフセットのゾーン指定子として `Z` を使用したUTC ISO 8601形式の日時。JSONでは文字列として表現されます。例：`1970-03-27T12:13:14-05:00` または `1970-03-27T12:18:14Z`。 |
| キャンセル理由 | `correctionReason` | 任意  | 値には次のいずれかを指定できます：<ul><li>`InvalidCreditCard`</li><li>`UnqualifiedLead`</li><li>`CannotShipSoldOut`</li><li>``DuplicateOrder</li><li>`ReturnedMerchandise`</li><li>`Other`</li></ul> |
| ステータス              | `status`         | 任意  | キャンセルする注文でオープンエンドロックを使用している場合は、キャンセルリクエストのステータスを `Declined` に構成する必要があります。 |

## ベンダーのドキュメント

詳細については、以下のベンダードキュメントを参照してください。

* [CJ Tracking APIの概要](https://developers.cj.com/docs/advertiser-api-tracking/api-overview)
* [注文の修正](https://developers.cj.com/docs/advertiser-api-tracking/restatements)
* [注文のキャンセル](https://developers.cj.com/docs/advertiser-api-tracking/cancellations)