---
title: CJ トラッキング API コネクタ構成ガイド
description: この記事では、CJ トラッキング API コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/cj-tracking-api-connector/
---
CJでは、ウェブトラッキングイベントに対して Universal Tag と Tracking API を同時に使用することを推奨しています。これは、それぞれが CJ のオファリングをサポートまたはエンリッチメントするためです。Tracking API の使用には、CJ側でのバックエンドの変更が必要であり、クライアント統合チームとの協力が必要です。詳細については、CJアカウントチームまたは `support@cj.com` にお問い合わせください。

## API 情報

このコネクタは以下のベンダー API を使用します：

* API 名: CJ API
* API エンドポイント：
    * トレースなし（ライブエンドポイント）: `https://tracking.api.cj.com/graphql/`
    * トレースあり（テストエンドポイント）: `https://tracking.api.cj.com/graphqltest/`
* ドキュメント: [CJ API](https://developers.cj.com/graphql/reference/private/Tracking)

## バッチ制限

このコネクタは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数: 10,000
* 最古のリクエストからの最大時間: 10分
* リクエストの最大サイズ: 100 MB

## コネクタアクション

| **アクション名** | **AudienceStream** | **EventStream** |
|:----------------|:-------------------|:----------------|
| 注文データ送信 | ✗  | ✓ |
| 注文再声明送信 | ✗ | ✓ |
| 注文キャンセル送信 | ✗ | ✓ |

## 構成の構成

コネクタマーケットプレイスにアクセスして新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/ja/server-side/connectors/manage/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **パーソナルアクセストークン**  
必須。あなたの CJ トラッキング API パーソナルアクセストークン。[CJ パーソナルアクセストークン](https://developers.cj.com/account/personal-access-tokens)ページにアクセスしてアカウントにログインし、パーソナルアクセストークンを生成してください。

コネクタの構成が完了したら、**完了**をクリックします。

## アクション構成 — パラメータとオプション

コネクタアクションの構成を続けるには、**続行**をクリックします。アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション — 注文データ送信


#### パラメータ

| **パラメータ**  | **宛先**  | **説明** |
|:----------|:-----------|:---------------|
| エンタープライズID | `enterpriseId`  | 必須。CJのクライアント統合チームによって割り当てられた一意のクライアントID。     |
| アクショントラッカーID | `actionTrackerId` | 必須。行動に対してCJのクライアント統合チームによって与えられた静的値。   |
| CJイベント  | `ciEvent` | 必須。CJによって定義された相関イベントID（CJクリックIDとしても知られています）。     |
| 注文ID  | `orderId` | 必須。クライアントによって定義された注文識別子。     |
| イベント時間  | `eventTime` | 必須。イベントのタイムスタンプ。      |
| 注文金額  | `amount`  | 必須。注文の合計金額。      |
| 注文割引  | `discount`  | 注文に適用された割引。      |
| クーポンコード | `coupon`  | 注文に適用されたクーポンコード。     |
| 通貨  | `currency`  | 注文に使用された通貨。     |
| 商品価格  | `unitPrice` | 注文内の各商品の単価の配列。    |
| 商品SKU  | `sku` | 注文内の各商品のSKUの配列。      |
| 商品数量  | `quantity`  | 注文された各商品の数量の配列。     |
| 商品割引 | `discount`  | 商品の単価に適用された商品割引の金額の配列。   |
| 広告主の業種 |   | サポートされる値は：`Retail`, `Finance`, `Travel`, `NetworkServices`。   |
| 付随支出 | `ancillarySpend`  | 取引における付随的な支出額（広告主のみの属性）。     |
| 年会費  | `annualFee` | この商品に関連する年会費。      |
| 申請状況  | `applicationStatus` | 取引がCJに送信された時点での申請の状況を特定します。   |
| Apr | `apr` | 申請承認時のAPR。      |
| 転送APR  | `aprTransfer` | 転送のAPR。      |
| 転送APR期間 | `aprTransferTime` | 転送APRの期間（月）。      |
| 予約日  | `bookingDate` | 予約が行われた日付の形式 `YYYY-MM-DD`。     |
| 予約状況  | `bookingStatus` | 予約の状況。例：`confirmed`, `pending`など。     |
| 税後予約価値  | `bookingValuePostTax` | 税後の予約価値。     |
| 税前予約価値 | `bookingValuePreTax`  | 税前の予約価値。      |
| ブランド | `brand` | 購入された商品または商品のブランド。     |
| ブランドID  | `brandId` | 商品予約のブランド識別子。      |
| ビジネスユニット | `businessUnit`  | 顧客が購入したビジネスユニット。     |
| キャンペーンID | `campaignId`  | 広告主固有のマーケティングキャンペーンID。      |
| キャンペーン名 | `campaignName`  | 広告主固有のマーケティングキャンペーン名。      |
| カードカテゴリ | `cardCategory`  | カードカテゴリの名前。     |
| 車オプション | `carOptions`  | 取引中に選択されたその他の車オプション。例：`insurance`。     |
| キャッシュアドバンス手数料  | `cashAdvanceFee`  | この商品に関連するキャッシュアドバンス手数料。      |
| カテゴリ  | `category`  | 商品のカテゴリ。例えば、顧客がパーソナルキャッシュバッククレジットカードを申し込む場合：`service_type=cc&item_type=personal&category=cashback`）。  |
| 市  | `city`  | ホテルまたはイベントの場所の都市名。     |
| クラス | `class` | 予約または購入された商品のクラス評価。     |
| 確認番号 | `confirmationNumber`  | プロバイダーの確認番号。例えば、航空会社からのフライト確認番号。   |
| 契約期間 | `contractLength`  | 契約の期間（月）。      |
| 契約タイプ | `contractType`  | 広告主固有の契約の説明。     |
| 国コード  | `countryCode` | 取引が行われた国。     |
| クーポン割引 | `couponDiscount`  | 使用されたクーポンから割引された金額。     |
| クーポンタイプ | `couponType`  | 使用されたクーポンのタイプ。      |
| クレジットライン | `creditLine`  | 顧客に拡張されたクレジットの金額。      |
| クレジット品質  | `creditQuality` | 顧客のクレジットの品質。サポートされる値は：300-579=非常に悪い, 580-669=普通, 670-739=良い, 740-799=非常に良い, 800-850=優れている。  |
| クレジットレポート | `creditReport`  | 顧客がクレジットレポートを受け取ったか、購入したか、無料レポートを得たか、またはレポーティングサービスの試用を開始したかどうか。  |
| クルーズタイプ | `cruiseType`  | クルーズのタイプ。例：`Alaskan`, `Caribbean`など。    |
| 顧客国  | `customerCountry` | 購入する顧客がいる国、ISO 3166-1 alpha 2国コードを使用してフォーマットされます。例：`US`, `UK`, `AU`, `FR`。   |
| 顧客セグメント  | `customerSegment` | 広告主固有の顧客セグメント。     |
| 顧客ステータス | `customerStatus`  | 顧客が新規または既存か。     |
| 顧客タイプ | `customerType`  | 顧客のタイプ。例：`company`, `individual consumer`, `business`, `leisure`。    |
| 配送  | `delivery`  | 配送方法。       |
| 説明 | `description` | 商品またはカードの説明。      |
| 目的地都市  | `destinationCity` | 目的地の都市名。      |
| 目的地国 | `destinationCountry`  | サービスの目的地の国、ISO 3166-1 alpha 2国コードを使用してフォーマットされます。例：`US`, `UK`, `AU`, `FR`。   |
| 目的地ID  | `destinationId` | サービスの目的地ID、通常は広告主が定義した目的地の都市または州/県を表すコードです。例：`728660`。 |
| 目的地州 | `destinationState`  | サービスの目的地の州/県、ISO 3166-2州コードを使用してフォーマットされます。   |
| 国内  | `domestic`  | 顧客がアメリカ合衆国に居住しているかどうか。     |
| 降車Iata  | `dropoffIata` | 降車が空港である場合のIATAコード。    |
| 降車ID  | `dropoffId` | 降車場所のレンタカー代理店の一意のID。     |
| 期間  | `duration`  | イベントまたは商品の期間（日数）、例えばホテル滞在の夜数や試用サブスクリプションの期間。   |
| 終了日時 | `endDateTime` | チェックアウト日時、出発日時など。    |
| フライト運賃タイプ  | `flightFareType`  | フライト運賃のタイプ。例：`Gotta Get Away`。     |
| フライトオプション  | `flightOptions` | フライトパッケージに選択されたその他のオプション。例：`wiki`。    |
| フライトタイプ | `flightType`  | フライトのタイプ。例：`direct`, `layover`, `overnight`。     |
| フライヤーマイル | `flyerMiles`  | このフライトから獲得されたフライヤーマイル。      |
| 資金供給額 | `fundedAmount`  | アカウントの資金供給額。     |
| 資金供給通貨 | `fundedCurrency`  | アカウントの初期資金の通貨。      |
| ジャンル | `genre` | エンターテイメントのカテゴリまたはジャンル。例：`books`, `movies`, `streaming`, `music`など。このパラメータは取引レベルのみです。  |
| ゲスト  | `guests`  | ゲストの数。       |
| Iata  | `iata`  | フライトスケジュールの各都市のコードをコンマ区切りのリストで、コンマはURLエンコードされなければなりません。    |
| 紹介APR  | `introductoryApr` | 購入のための紹介APR。紹介APRが全体のAPRと異ならない場合は、**APR**パラメータを使用します。   |
| 紹介APR期間 | `introductoryAprTime` | 紹介APRの期間（月）。      |
| 商品ID | `itemId`  | 購入された商品のID。複数の商品がある場合、パラメータはコンマ区切りのリストを使用します。   |
| 商品名 | `itemName`  | 購入された商品の名前。     |
| 商品タイプ | `itemType`  | 商品のタイプ。例えば、顧客がパーソナルキャッシュバッククレジットカードを申し込む場合：`service_type=cc&item_type=personal&category=cashback`）。 |
| 旅程ID  | `itineraryId` | 予約の旅程ID。     |
| ライフステージ | `lifestage` | 一般的な人口統計（新しい移動者、学生、小規模企業など）で、カードがどのように、なぜ使用されるかを示します。  |
| 場所  | `location`  | 広告主固有のIDまたは名前で、顧客が訪れるか訪れた店舗または場所を特定するために使用できます。  |
| ロイヤルティ獲得  | `loyaltyEarned` | 顧客のロイヤルティステータスのレベル。     |
| ロイヤリティ初回登録 | `loyaltyFirstTimeSignup`  | この注文が消費者のロイヤリティプログラムへの参加につながった場合。     |
| ロイヤリティレベル | `loyaltyLevel`  | ロイヤリティポイントが使用された場合。      |
| ロイヤリティ使用 | `loyaltyRedeemed` | ロイヤリティポイントが獲得された場合。      |
| ロイヤリティステータス  | `loyaltyStatus` | 顧客の会員ステータス。      |
| マージン  | `margin`  | 取引の利益率を示す広告主のみの属性。   |
| マーケティングチャネル | `marketingChannel`  |  マーケティングチャネル。     |
| 最低残高 | `minimumBalance`  | 口座の最低現金残高要件の値。    |
| 最低預金 | `minimumDeposit`  | 最低預金額。     |
| 最低滞在期間 | `minimumStayDuration` | 最低滞在期間（日数）。      |
| キャンセル不可 | `noCancellation`  | 取引にキャンセル不可ポリシーが存在する場合、`yes`または`no`。     |
| 注文小計  | `orderSubtotal` | 注文の小計。      |
| 出発都市 | `originCity`  | サービスの出発都市名（例：ニューヨーク）。     |
| 出発国  | `originCountry` | サービスの出発国コード。ISO 3166-1 alpha 2国コードを使用してフォーマットされます。例：`US`, `UK`, `AU`, `FR`。   |
| 出発州  | `originState` | サービスの出発州/省。ISO 3166-2州コードを使用してフォーマットされます。     |
| 予約時税込支払額  | `paidAtBookingPostTax`  | 税込みで予約時に支払われた金額。     |
| 予約時税抜支払額 | `paidAtBookingPreTax` | 税抜きで予約時に支払われた金額。      |
| 支払いモデル | `paymentMethod` | 使用された支払いモデル。例：`advertiser-specific`。     |
| ピックアップIATA | `pickupIata`  | 空港ピックアップ場所のIATAコード。     |
| ピックアップID | `pickupId`  | ピックアップに使用されるレンタカー代理店の一意の場所ID。     |
| プラットフォームID | `platformId`  | 顧客が使用しているデバイス。例：`mobile`, `tablet`など。   |
| 販売地点 | `pointOfSale` | 顧客の販売地点。     |
| 港  | `port`  | クルーズの出発港。     |
| 予約注文  | `preorder`  | 顧客が販売可能になる前に商品を購入した場合。    |
| 前払い | `prepaid` | 顧客が取引を前払いした場合、`yes`または`no`。     |
| 事前承認  | `prequalify`  | 申込者がカードに事前承認された場合。      |
| プロモーション | `promotion` | 適用されたプロモーション。例：`summer sale`。     |
| プロモーション金額  | `promotionAmount` | プロモーションに関連する数値額。例：プロモーションが$500キャッシュバックの場合、この値は`promotion=dollars&promotion_amt=500`） |
| プロモーション条件閾値 | `promotionConditionThreshold` | 割引を得るために必要な閾値。     |
| プロモーション条件タイプ  | `promotionConditionType`  | プロモーション条件のタイプ。      |
| プロモーション終了  | `promotionEnds` | プロモーションが終了する日付。ISO 8601標準を使用してフォーマットされます。例：`2022-12-25T15:30:50.111Z`。    |
| プロモーション開始  | `promotionStarts` | プロモーションが開始する日付。ISO 8601標準を使用してフォーマットされます。例：`2022-12-25T15:30:50.111Z`。  |
| プロモーションタイプ  | `promotionType` | プロモーションのタイプ。       |
| 数量  | `quantity`  | 特定のSKUの数量、単純なアクションのみ。アイテムベースのアクションを使用する場合は、`QTYx`を使用します。   |
| 評価  | `rating`  | 予約または購入されたアイテムの星評価。      |
| 部屋タイプ | `roomType`  | ホテルまたはクルーズで予約された部屋のタイプ。      |
| 部屋数 | `rooms` | 予約された部屋の数。     |
| サービスタイプ  | `serviceType` | 顧客が登録または購入した金融サービスのタイプ。    |
| 船名 | `shipName`  | クルーズ船の名前。      |
| 開始日時 | `startDateTime` | 予約または購入されたアイテムのチェックイン日時、到着日時、または同様の開始時間。    |
| 州 | `state` | 店舗が位置する州または県を定義します。ISO 3166-2州コードを使用してフォーマットされます。例：アラスカのコードは`US-AK`、バンコクは`TH-10`。 |
| サブスクリプション料金  | `subscriptionFee` | 無料トライアル登録時に提示されるサブスクリプション料金。     |
| サブスクリプション期間 | `subscriptionLength`  | 製品の期間。例：`indefinite`, `1 month`, `3 months`, `6 months`）。    |
| 税額  | `taxAmount` | 税額。      |
| 税タイプ  | `taxType` | 税のタイプ。      |
| 転送手数料  | `transferFee` | クレジットカードの転送手数料額。      |
| 旅行タイプ | `travelType`  | 予約される旅行のタイプ。例：`air`, `car`, `activities`, `cruise`, `events`, `hotel`, `package`, `restaurants`, `travel guides`, `vacation rental`, `other`。  |
| 旅行タイプ | `tripType`  | 予約または購入された旅行のタイプ。例：片道、往復、複数都市、往復とホテル。    |
| アップセル  | `upsell`  | 顧客がトライアルからサブスクリプションに変更した場合。     |
| CJユーザー |   | CJユーザーID。       |

### アクション - 注文再声明の送信

このアクションでは、CJトラッキングに注文再声明を送信します。注文再声明では、既にロックされていない、またはクローズされていない手数料対象の注文に対して属性を変更したり、追加したりすることができます。このアクションは注文の現在の状態を完全に上書きし、再声明に含まれる情報のみを持つように注文を更新します。

#### パラメータ

| パラメータ                  | 宛先        | 必須？ | 説明 |
|----------------------------|-------------------|-----------|-------------|
| エンタープライズID | `enterpriseId`      | 必須  | CJのクライアント統合チームによって割り当てられた一意のクライアントID。 |
| アクショントラッカーID          | `actionTrackerId`   | 必須  | CJのクライアント統合チームによって与えられたアクションに対する静的値。 |
| 注文ID                   | `orderId`           | 必須  | クライアントによって定義された注文識別子。 |
| 更新時間  | `updateTime`        | 必須  | UTC ISO 8601形式の日時で、UTCオフセットのゾーン指定子として`Z`が使用され、JSONでは文字列としてレンダリングされます。例：`1970-03-27T12:13:14-05:00`または`1970-03-27T12:18:14Z`。 |
| CJイベント    | `cjEvent`           | 任意  | CJによって定義された相関イベントID（CJクリックIDとも呼ばれます）。 |
| 注文金額               | `amount`            | 任意  | 注文の合計金額。 |
| 注文割引             | `discount`          | 任意  | 注文に適用された割引。 |
| 垂直パラメータ        | `verticalParameters` | 任意  | 再声明に関連する特定の垂直分野をキャプチャするための追加情報。 |
| カスタムパラメータ          | `customParameters`  | 任意  | 配列内にアイテムが存在する場合、値はnullにできません。 |
| アイテム                      | `items`             | 任意  | 配列内にアイテムが存在する場合、値はnullにできません。 |
| クーポンコード                | `coupon`            | 任意  | 注文に適用されたクーポンコード。 |
| 通貨                   | `currency`          | 任意  | 注文に使用された通貨。例：`USD`。 |
| バイパスチャネル             | `bypassChannel`     | 任意  | トランザクションの帰属プロセスをカスタマイズします。例：`Channel=CJ`。値は次のいずれかになります：<ul><li>`CJ`</li><li>`Direct`</li><li>`Affiliate_other`</li><li>`Display`</li><li>`Social`</li><li>`Search`</li><li>`Email`</li><li>`Other`</li></ul> |
| ステータス                     | `status`            | 任意  | 注文のステータス。値は`Pending`または`Accepted`になります。 |
| 訂正の理由      | `correctionReason`  | 任意  | 値は次のいずれかになります：<ul><li>`InvalidCreditCard`</li><li>`UnqualifiedLead`</li><li>`CannotShipSoldOut`</li><li>`DuplicateOrder`</li><li>`ReturnedMerchandise`</li><li>`Other`</li></ul> |

### アクション - 注文キャンセルの送信

このアクションは、既存の注文をキャンセルし、その注文に対して手数料や料金を支払いたくないことをCJに伝えます。この概念は、CJが従来「完全訂正」と呼んでいたものに似ています。
#### パラメータ

| パラメータ             | 宛先               | 必須？    | 説明 |
|-----------------------|-------------------|-----------|-------------|
| エンタープライズID   | `enterpriseId`    | 必須      | CJのクライアント統合チームによって割り当てられたユニークなクライアントID。 |
| アクショントラッカーID | `actionTrackerId` | 必須      | 行動に対してCJのクライアント統合チームが与える静的な値。 |
| 注文ID               | `orderId`         | 必須      | クライアントが定義する注文識別子。 |
| 更新時間             | `updateTime`      | 必須      | UTC ISO 8601形式の日時で、UTCオフセットのゾーン指定子として`Z`が使用され、JSONでは文字列として表現されます。例：`1970-03-27T12:13:14-05:00`または`1970-03-27T12:18:14Z`。 |
| キャンセル理由       | `correctionReason`| 任意      | 値は以下のいずれかになります：<ul><li>`InvalidCreditCard`</li><li>`UnqualifiedLead`</li><li>`CannotShipSoldOut`</li><li>`DuplicateOrder`</li><li>`ReturnedMerchandise`</li><li>`Other`</li></ul> |
| ステータス           | `status`          | 任意      | キャンセルを要求する注文がオープンエンドロックを使用している場合、ステータスを`Declined`に構成する必要があります。 |

## ベンダー文書

追加情報については、以下のベンダー文書を参照してください：

* [CJ トラッキング API 概要](https://developers.cj.com/docs/advertiser-api-tracking/api-overview)
* [注文再声明](https://developers.cj.com/docs/advertiser-api-tracking/restatements)
* [注文キャンセル](https://developers.cj.com/docs/advertiser-api-tracking/cancellations)
