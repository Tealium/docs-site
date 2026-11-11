---
title: SAS Customer Intelligence 360タグ構成ガイド
description: この記事では、SAS Customer Intelligence 360タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/sas-ci-360/
---
SAS Customer Intelligence 360は、デジタルインテリジェンス機能を通じて、マーケティング分析と動的なコンテンツのパーソナライゼーションを提供します。

## タグに関するヒント

マッピングは、次の目的で使用します。

* イベントトリガーを構成する
* イベント固有のパラメーターをイベント名にマッピングする
* 標準構成値を動的に上書きする
* Eコマース拡張機能の値を動的に上書きする

次のEコマース拡張機能パラメーターをサポートしています。

* 注文ID
* 注文合計
* 配送料
* 税額
* 顧客の市区町村
* 顧客の国
* 顧客の郵便番号
* 製品IDのリスト
* 名前のリスト
* SKUのリスト
* 数量のリスト
* 価格のリスト
* カテゴリーのリスト

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を行います。

* **サーバー**: （必須）この変数には、リージョンのサーバーアドレス、またはCNAME構成に基づくアドレスが入力されます。通常はドメイン名です（例：`https://www.[Domain].com`）。
* **テナントID**: （必須）英数字の値（例：`111aaaaa1111111111111aaa`）。
* **ID**: （任意）英数字の値（例：`111aaaaa1111111111111aaa`）。
* **名前**: ID情報の保存場所。IDトラッキングが有効な場合は必須です。
* **タイプ**: 既知のIDのタイプ。IDトラッキングが有効な場合は必須です。
* **ソース**: ID情報のソース。デフォルト値は`cookie`です。
* **難読化**: ID名の値を難読化します。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| サーバー `server`  | 文字列 |
| テナントID `tenantID`  | 文字列 |
| ID `identity`  | ブール値 |
| 名前 `name`  | 文字列 |
| タイプ `type`  | 文字列 |
| ソース `source`  | 文字列 |
| 難読化 `obscure`  | ブール値 |

### Eコマース

| 変数 | 説明 |
|:---------|:------------|
| 注文ID `orderId`（`_corder`を上書き） | 数値、文字列 |
| 注文合計 `totalCartValue`（`_ctotal`を上書き） | 数値、文字列 |
| 顧客の市区町村 `billingCity`（`_ccity`を上書き） | 文字列 |
| 顧客の国 `billingCountry`（`_ccountry`を上書き） | 文字列 |
| 顧客の郵便番号 `billingPostcode`（`_czip`を上書き） | 文字列 |
| 顧客の地域 `billingRegion`  | 文字列 |
| 配送タイプ `deliveryType`  | 文字列 |
| 支払いタイプ `paymentType`  | 文字列 |
| 配送先の市区町村 `shippingCity`  | 文字列 |
| 配送料 `shippingCost`（`_cship`を上書き） | 文字列 |
| 配送先の国 `shippingCountry`  | 文字列 |
| 配送先の郵便番号 `shippingPostcode`  | 文字列 |
| 配送先の地域 `shippingRegion`  | 文字列 |
| 税額 `tax`（`_ctax`を上書き） | 数値、文字列 |
| ID `id`  | 文字列 |
| 製品ID `productId`（`_cprod`を上書き） | 配列 |
| 製品SKU `productSKU`（`_csku`を上書き） | 配列 |
| 製品名 `productName`（`_cprodname`を上書き） | 配列 |
| 製品数量 `quantity`（`_cquan`を上書き） | 配列 |
| 製品価格 `unitPrice`（`_cprice`を上書き） | ［配列］ |
| グループ `group`（`_ccat`を上書き） | 配列 |
| カートID `cartId`  | ［数値、文字列］ |
| カート名 `cartName`  | 文字列 |
| カートタイプ `cartType`  | 文字列 |
| 割引メッセージ `savingsMessage`  | 配列 |
| 配送メッセージ `shippingMessage`  | 配列 |
| 在庫状況メッセージ `availabilityMessage`  | 配列 |
| スポット名 `spotName`  | 文字列 |

### クリック

| 変数 | 説明 |
|:---------|:------------|
| 代替テキスト `altText`  | 文字列 |
| アンカーID `anchorId`  | 文字列 |
| アンカー名 `anchorName`  | ブール値 |
| 要素タグ名 `elementTagName`  | 文字列 |
| onClick `onClick`  | 文字列 |
| ターゲットの内部テキスト `targetInnerText`  | 文字列 |
| ターゲットのセレクターパス `targetSelectorPath`  | 文字列 |
| URI `uri`  | 文字列 |

### メディア

| 変数 | 説明 |
|:---------|:------------|
| 再生時間 `duration`  | 文字列 |
| プレーヤー `player`  | 文字列 |
| 位置 `position`  | ブール値 |
| URL `url`  | 文字列 |
| URI `uri`  | 文字列 |

### プロモーション

| 変数 | 説明 |
|:---------|:------------|
| レコードタイプ `recordType`  | 文字列 |
| クリエイティブ名 `creativeName`  | 文字列 |
| 配置ID `placementId`  | 文字列 |
| トラッキングコード `trackingCode`  | 文字列 |

### 読み込み

| 変数 | 説明 |
|:---------|:------------|
| ページタイトル `pageTitle`  | 文字列 |
| 参照元 `referrer`  | 文字列 |
| URI `uri`  | 文字列 |

### ID

| 変数 | 説明 |
|:---------|:------------|
| ログインID `loginId`  | 文字列 |
| ログインイベントタイプ `loginEventType`  | 文字列 |
| 難読化するフィールド `obfuscateFields`  | 文字列 |

### カスタム

| 変数 | 説明 |
|:---------|:------------|
| `customName` | 文字列 |
| `customGroupName` | 文字列 |
| `customRevenue` | 文字列 |

### イベントトリガー

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| カート、カート表示アクション（`cart-cartview`） | `cart-cartview` |
| カート、チェックアウトアクション（`cart-checkout`） | `cart-checkout` |
| カート、購入アクション（`cart-purchase`） | `cart-purchase` |
| カートアクション、追加アクション（`cartaction-add`） | `cartaction-add` |
| カートアクション、更新アクション（`cartaction-update`） | `cartaction-update` |
| カートアクション、削除アクション（`cartaction-remove`） | `cartaction-remove` |
| メディア、終了アクション（`media-end`） | `media` |
| メディア、開始アクション（`media-start`） | `media` |
| メディア、停止アクション（`media-stop`） | `media` |
| 変更（`change`） | `change` |
| クリック（`click`） | `click` |
| クリックスルー（`clickthrough`） | `clickthrough` |
| コンテンツ変更（`contentchange`） | `contentchange` |
| IDのブロッキング付き関連付け（`attachIdentityBlocking`） | `attachIdentityBlocking` |
| IDの関連付け（`attachIdentity`） | `attachIdentity` |
| クロスチャネルIDの関連付け解除（`detachIdentityCrossChannel`） | `detachIdentityCrossChannel` |
| IDの関連付け解除（`detachIdentity`） | `detachIdentity` |
| ドキュメント（`document`） | `document` |
| インプレッション（`impression`） | `impression` |
| 表示可能なインプレッション（`impressionViewable`） | `impressionViewable` |
| 内部検索（`internalSearch`） | `internalSearch` |
| JS変数の変更（`jsvarchange`） | `jsvarchange` |
| 読み込み（`load`） | `load` |
| 製品表示（`productView`） | `productView` |
| プロモーション（`promotion`） | `promotion` |
| 送信（`submit`） | `submit` |
| 表示状態の変更（`visibilityChange`） | `visibilityChange` |
| カスタム（`custom`） | `custom` |
### イベント固有のパラメータ
イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| カート、カート表示アクション（`cart-cartview`） | `cart-cartview` |
| カート、チェックアウトアクション（`cart-checkout`） | `cart-checkout` |
| カート、購入アクション（`cart-purchase`） | `cart-purchase` |
| カートアクション、追加アクション（`cartaction-add`） | `cartaction-add` |
| カートアクション、更新アクション（`cartaction-update`） | `cartaction-update` |
| カートアクション、削除アクション（`cartaction-remove`） | `cartaction-remove` |
| メディア、終了アクション（`media-end`） | `media` |
| メディア、開始アクション（`media-start`） | `media` |
| メディア、停止アクション（`media-stop`） | `media` |
| 変更（`change`） | `change` |
| クリック（`click`） | `click` |
| クリックスルー（`clickthrough`） | `clickthrough` |
| コンテンツ変更（`contentchange`） | `contentchange` |
| ID のブロッキング付き関連付け（`attachIdentityBlocking`） | `attachIdentityBlocking` |
| ID の関連付け（attachIdentity） | `attachIdentity` |
| クロスチャネルでの ID の関連付け解除（`detachIdentityCrossChannel`） | `detachIdentityCrossChannel` |
| ID の関連付け解除（`detachIdentity`） | `detachIdentity` |
| ドキュメント（`document`） | `document` |
| インプレッション（`impression`） | `impression` |
| 閲覧者ブルインプレッション（`impressionViewable`） | `impressionViewable` |
| 内部検索（`internalSearch`） | `internalSearch` |
| JS 変数変更（`jsvarchange`） | `jsvarchange` |
| 読み込み（`load`） | `load` |
| 商品表示（`productView`） | `productView` |
| プロモーション（`promotion`） | `promotion` |
| 送信（`submit`） | `submit` |
| 表示状態の変更（`visibilityChange`） | `visibilityChange` |
| カスタム（`custom`） | `custom` |