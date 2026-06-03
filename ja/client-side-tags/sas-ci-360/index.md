---
title: SASカスタマーインテリジェンス360タグ構成ガイド
description: この記事では、SASカスタマーインテリジェンス360タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/sas-ci-360/
---
SASカスタマーインテリジェンス360は、そのデジタルインテリジェンス機能を通じてマーケティング分析とダイナミックなコンテンツのパーソナライゼーションを提供します。

## タグのヒント

マッピングを使用して：

* イベントトリガーの構成
* イベント固有のパラメータをイベント名にマッピング
* 標準の構成値を動的に上書き
* E-Commerce拡張値を動的に上書き

以下のE-Commerce拡張パラメータをサポートしています：

* 注文ID
* 注文合計
* 送料
* 税金
* 顧客の都市
* 顧客の国
* 顧客の郵便番号
* 商品IDのリスト
* 名前のリスト
* SKUのリスト
* 数量のリスト
* 価格のリスト
* カテゴリのリスト


## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、以下の構成を行います：

* **サーバー**：必須。この変数は、あなたの地域のサーバーアドレスで埋められるか、あなたのCNAME構成に基づいています。通常、これはあなたのドメイン名です（例：`https://www.[Domain].com`）。
* **テナントID**：必須。英数字の値（例：`111aaaaa1111111111111aaa`）。
* **Identity**：オプション。英数字の値（例：`111aaaaa1111111111111aaa`）。
* **Name**：Identity情報の位置。Identityトラッキングが有効化されている場合は必須。
* **Type**：既知のIdentityのタイプ。Identityトラッキングが有効化されている場合は必須。
* **Source**：Identity情報のソース。デフォルト値は`cookie`。
* **Obscure**：Identity名の値を隠す。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

| 変数 | 説明 |
|:---------|:------------|
| サーバー `server`  | 文字列 |
| テナントID `tenantID`  | 文字列 |
| Identity `identity`  | ブール値 |
| 名前 `name`  | 文字列 |
| タイプ `type`  | 文字列 |
| ソース `source`  | 文字列 |
| Obscure `obscure`  | ブール値 |

### E-Commerce

| 変数 | 説明 |
|:---------|:------------|
| 注文ID `orderId` (`_corder`を上書き)  | 数値、文字列 |
| 注文合計 `totalCartValue` (`_ctotal`を上書き)  | 数値、文字列 |
| 顧客の都市 `billingCity` (`_ccity`を上書き)  | 文字列 |
| 顧客の国 `billingCountry` (`_ccountry`を上書き)  | 文字列 |
| 顧客の郵便番号 `billingPostcode` (`_czip`を上書き)  | 文字列 |
| 顧客の地域 `billingRegion`  | 文字列 |
| 配送タイプ `deliveryType`  | 文字列 |
| 支払いタイプ `paymentType`  | 文字列 |
| 配送都市 `shippingCity`  | 文字列 |
| 送料 `shippingCost` (`_cship`を上書き)  | 文字列 |
| 配送国 `shippingCountry`  | 文字列 |
| 配送郵便番号 `shippingPostcode`  | 文字列 |
| 配送地域 `shippingRegion`  | 文字列 |
| 税金 `tax` (`_ctax`を上書き)  | 数値、文字列 |
| ID `id`  | 文字列 |
| 商品ID `productId` (`_cprod`を上書き)  | 配列 |
| 商品SKU `productSKU` (`_csku`を上書き)  | 配列 |
| 商品名 `productName` (`_cprodname`を上書き)  | 配列 |
| 商品の数量 `quantity` (`_cquan`を上書き)  | 配列 |
| 商品の価格 `unitPrice` (`_cprice`を上書き)  | [配列] |
| グループ `group` (`_ccat`を上書き)  | 配列 |
| カートID `cartId`  | [数値、文字列] |
| カート名 `cartName`  | 文字列 |
| カートタイプ `cartType`  | 文字列 |
| 割引メッセージ `savingsMessage`  | 配列 |
| 配送メッセージ `shippingMessage`  | 配列 |
| 在庫メッセージ `availabilityMessage`  | 配列 |
| スポット名 `spotName`  | 文字列 |

### クリック

| 変数 | 説明 |
|:---------|:------------|
| Altテキスト `altText`  | 文字列 |
| アンカーID `anchorId`  | 文字列 |
| アンカー名 `anchorName`  | ブール値 |
| 要素タグ名 `elementTagName`  | 文字列 |
| onClick `onClick`  | 文字列 |
| ターゲット内テキスト `targetInnerText`  | 文字列 |
| ターゲットセレクターパス `targetSelectorPath`  | 文字列 |
| Uri `uri`  | 文字列 |

### メディア

| 変数 | 説明 |
|:---------|:------------|
| 期間 `duration`  | 文字列 |
| プレーヤー `player`  | 文字列 |
| 位置 `position`  | ブール値 |
| Url `url`  | 文字列 |
| Uri `uri`  | 文字列 |

### プロモーション

| 変数 | 説明 |
|:---------|:------------|
| レコードタイプ `recordType`  | 文字列 |
| クリエイティブ名 `creativeName`  | 文字列 |
| 配置ID `placementId`  | 文字列 |
| トラッキングコード `trackingCode`  | 文字列 |

### ロード

| 変数 | 説明 |
|:---------|:------------|
| ページタイトル `pageTitle`  | 文字列 |
| リファラー `referrer`  | 文字列 |
| Uri `uri`  | 文字列 |

### Identity

| 変数 | 説明 |
|:---------|:------------|
| ログインID `loginId`  | 文字列 |
| ログインイベントタイプ `loginEventType`  | 文字列 |
| フィールドを難読化 `obfuscateFields`  | 文字列 |

### カスタム

| 変数 | 説明 |
|:---------|:------------|
| customName `customName`  | 文字列 |
| customGroupName `customGroupName`  | 文字列 |
| customRevenue `customRevenue`  | 文字列 |

### イベントトリガー
イベントをマッピングするには、[イベントマッピングの作成]()を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| カート、カート閲覧者クション (`cart-cartview`) | `cart-cartview` |
| カート、チェックアウトアクション (`cart-checkout`) | `cart-checkout` |
| カート、購入アクション (`cart-purchase`) | `cart-purchase` |
| カートアクション、追加アクション (`cartaction-add`) | `cartaction-add` |
| カートアクション、更新アクション (`cartaction-update`) | `cartaction-update` |
| カートアクション、削除アクション (`cartaction-remove`) | `cartaction-remove` |
| メディア、終了アクション (`media-end`) | `media` |
| メディア、開始アクション (`media-start`) | `media` |
| メディア、停止アクション (`media-stop`) | `media` |
| 変更 (`change`) | `change` |
| クリック (`click`) | `click` |
| クリックスルー (`clickthrough`) | `clickthrough` |
| コンテンツ変更 (`contentchange`) | `contentchange` |
| Identityブロッキングのアタッチ (`attachIdentityBlocking`) | `attachIdentityBlocking` |
| Identityのアタッチ (`attachIdentity`) | `attachIdentity` |
| Identityクロスチャネルのデタッチ (`detachIdentityCrossChannel`) | `detachIdentityCrossChannel` |
| Identityのデタッチ (`detachIdentity`) | `detachIdentity` |
| ドキュメント (`document`) | `document` |
| インプレッション (`impression`) | `impression` |
| インプレッション閲覧者ブル (`impressionViewable`) | `impressionViewable` |
| 内部検索 (`internalSearch`) | `internalSearch` |
| JS Var変更 (`jsvarchange`) | `jsvarchange` |
| ロード (`load`) | `load` |
| 商品ビュー (`productView`) | `productView` |
| プロモーション (`promotion`) | `promotion` |
| 提出 (`submit`) | `submit` |
| 可視性変更 (`visibilityChange`) | `visibilityChange` |
| カスタム (`custom`) | `custom` |

### イベント固有のパラメータ
イベントをマッピングするには、[イベントマッピングの作成]()を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| カート、カート閲覧者クション (`cart-cartview`) | `cart-cartview` |
| カート、チェックアウトアクション (`cart-checkout`) | `cart-checkout` |
| カート、購入アクション (`cart-purchase`) | `cart-purchase` |
| カートアクション、追加アクション (`cartaction-add`) | `cartaction-add` |
| カートアクション、更新アクション (`cartaction-update`) | `cartaction-update` |
| カートアクション、削除アクション (`cartaction-remove`) | `cartaction-remove` |
| メディア、終了アクション (`media-end`) | `media` |
| メディア、開始アクション (`media-start`) | `media` |
| メディア、停止アクション (`media-stop`) | `media` |
| 変更 (`change`) | `change` |
| クリック (`click`) | `click` |
| クリックスルー (`clickthrough`) | `clickthrough` |
| コンテンツ変更 (`contentchange`) | `contentchange` |
| Identityブロッキングのアタッチ (`attachIdentityBlocking`) | `attachIdentityBlocking` |
| Identityのアタッチ (`attachIdentity`) | `attachIdentity` |
| Identityクロスチャネルのデタッチ (`detachIdentityCrossChannel`) | `detachIdentityCrossChannel` |
| Identityのデタッチ (`detachIdentity`) | `detachIdentity` |
| ドキュメント (`document`) | `document` |
| インプレッション (`impression`) | `impression` |
| インプレッション閲覧者ブル (`impressionViewable`) | `impressionViewable` |
| 内部検索 (`internalSearch`) | `internalSearch` |
| JS Var変更 (`jsvarchange`) | `jsvarchange` |
| ロード (`load`) | `load` |
| 商品ビュー (`productView`) | `productView` |
| プロモーション (`promotion`) | `promotion` |
| 提出 (`submit`) | `submit` |
| 可視性変更 (`visibilityChange`) | `visibilityChange` |
| カスタム (`custom`) | `custom` |


