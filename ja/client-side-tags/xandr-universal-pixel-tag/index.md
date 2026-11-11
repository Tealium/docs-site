---
title: Xandr Universal Pixelタグ構成ガイド
description: この記事では、タグ管理アカウントでXandr Universal Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/xandr-universal-pixel-tag/
---
## タグに関するヒント

* 複数のPixel IDをカンマ区切りのリストで入力できます。
* 注文IDが構成されると、購入トラッキングが自動的に実行されます。購入の自動トラッキングを無効にするには、マッピングを使用して`automatic_purchase_tracking`宛先を切り替えます。
* PageViewトラッキングは自動的に実行されます。PageViewの自動トラッキングを無効にするには、マッピングを使用して`automatic_pageview_tracking`宛先を切り替えます。
* デフォルトでは、PageViewイベントは追加データなしで実行されます。PageViewイベントでデータを渡す場合は、マッピングツールボックスの「イベント固有のパラメータ」タブで、使用する変数をマッピングする必要があります。
* 次のEコマース拡張機能パラメータをサポートしています。
  * 注文ID（`_corder`）
  * 商品IDのリスト（`_cprod`）
  * 商品名のリスト（`_cprodname`）
  * 商品カテゴリーのリスト（`_ccat`）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **Pixel ID**
  * Xandr Universal Pixel IDを入力します。
  * 複数のIDをカンマ区切りのリストで入力できます。
* **広告保存の同意**：広告保存に対するデフォルトの同意を構成します。**データマッピング**セクションで`ad_storage`パラメータをマッピングすることで、この値を動的に更新できます。
* **Tealium同意Cookieから自動的に読み取る**：trueに構成すると、[Tealium同意マネージャー](https://docs.tealium.com/about-consent-management/)に基づいて同意が構成されます。

## 同意モード

このタグに同意モードを実装する方法は2つあります。

* [クライアント側の同意管理](https://docs.tealium.com/about-consent-management/)を使用し、Tealium同意Cookieを自動的に読み取ります。
* [JavaScriptコード拡張機能](https://docs.tealium.com/javascript-code-extension/)を追加し、同意管理プラットフォーム（CMP）の同意選択とカテゴリーマッピングをこのタグにマッピングします。

訪問が同意を選択すると、タグはファーストパーティCookieとサードパーティCookieに対して適切な処理を選択します。

* **許可**：ファーストパーティCookieとサードパーティCookieの両方を読み書きできます。
* **拒否**：ファーストパーティCookieは読み書きされません。サードパーティCookieは広告目的では使用されず、不正行為やスパム対策の目的でのみ読み取られます。

### クライアント側の同意管理

クライアント側の同意管理を使用してこのタグに同意モードを実装するには、タグ構成で**Tealium同意Cookieから自動的に読み取る**を`true`に構成します。

### JavaScriptコード拡張機能

エンドユーザーの同意選択をXandrの同意モード構成にマッピングするには、JavaScriptコード拡張機能を使用します。拡張機能を次のように構成します。

* **スコープ**を**ロードルールの後（デフォルト）**に構成します。
* **実行頻度**を**常に実行**に構成します。
* CMP用のJavaScriptコードを入力します。次のコードテンプレート内の`CUSTOM_LOGIC`をベンダー固有のロジックに置き換えることで、CMPに合わせてカスタマイズできます。

```js
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = CUSTOM_LOGIC ? 'granted' : 'denied';
```

たとえば、次のコードはOneTrust用です。

```js
// After Load Rules - Run Always
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = b.consent_decision.indexOf('C0004') !== -1  ? 'granted' : 'denied';
```

これらの変数名をそのまま使用する場合、追加のマッピングは必要ありません。最新バージョンのタグでは、これらの変数がデフォルトで使用されます。個別のユースケースに応じて、`ad_storage`パラメータを属性にマッピングし、これらの変数を上書きできます。

## データマッピング

データマッピングでは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### タグ構成

| 変数                      | 型              | 説明                                  |
|---------------------------|-----------------|---------------------------------------|
| `pixel_id`                | 文字列          | Universal Pixel ID。                  |
| `auto_pageview_tracking`  | 真偽値、文字列  | PageViewの自動トラッキングを切り替えます。 |
| `auto_purchase_tracking`  | 真偽値、文字列  | 購入の自動トラッキングを切り替えます。 |
| `base_url`                | 文字列          | ベースURL。                           |

### Eコマース

| 変数          | 型     | 説明                                        |
|---------------|--------|---------------------------------------------|
| `item_type`   | 配列   | 商品カテゴリーのリスト（`_ccat`を上書き）。 |
| `item_id`     | 配列   | 商品IDのリスト（`_cprod`を上書き）。        |
| `item_name`   | 配列   | 商品名のリスト（`_cprodname`を上書き）。    |

### イベント

| 変数                 | 説明                       |
|----------------------|----------------------------|
| `AddPaymentInfo`     | 支払い情報の追加。         |
| `AddToCart`          | カートへの追加。           |
| `InitiateCheckout`   | チェックアウトの開始。     |
| `ItemView`           | 商品の表示。               |
| `LandingPage`        | ランディングページ。       |
| `Lead`               | リード。                   |
| `PageView`           | ページビュー。             |
| `Purchase`           | 購入。                     |
| `Custom`             | カスタムイベント。         |

### イベント固有のパラメータ

| 変数                | 説明                       |
|---------------------|----------------------------|
| `item_type`         | 商品タイプ。               |
| `item_id`           | 商品ID。                   |
| `item_name`         | 商品名。                   |
| `Custom_Parameter`  | カスタムパラメータ。       |
| `AddPaymentInfo`    | 支払い情報の追加。         |
| `AddToCart`         | カートへの追加。           |
| `InitiateCheckout`  | チェックアウトの開始。     |
| `ItemView`          | 商品の表示。               |
| `LandingPage`       | ランディングページ。       |
| `Lead`              | リード。                   |
| `Purchase`          | 購入。                     |
| `Custom_Event`      | カスタムイベント。         |