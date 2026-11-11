---
title: Microsoft Advertising ユニバーサル イベント トラッキング（UET）タグ構成ガイド
description: この記事では、Microsoft Advertising ユニバーサル イベント トラッキング（UET）タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/microsoft-advertising-universal-event-tracking-uet-tag/
---
## タグに関するヒント

* マッピングを使用して、以下を行います。
  * 標準構成値を上書きする。
  * Eコマース拡張機能の値を上書きする。
  * カスタムパラメータを渡す。
  * イベントトリガーを構成する。
* **Standard**タブでパラメータを**Custom Property/Parameter**にマッピングすると、そのパラメータがすべてのイベントとともに送信されます。特定のイベントにのみデータを送信するには、**Event Parameters**タブを使用します。
* 以下のEコマース拡張機能の値をサポートしています。
  * 注文ID。
  * 注文小計。
  * 注文の配送料。
  * 注文の税額。
  * 注文の通貨。
  * 注文のクーポン／プロモーションコード。
  * 商品IDのリスト。
  * 名前のリスト。
  * ブランドのリスト。
  * カテゴリのリスト。
  * 数量のリスト。
  * 価格のリスト。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、以下の構成を構成します。

* **Tag ID**：Microsoft Advertisingのタグ識別子。
* **ID Sync Beacon**：内部ユーザーIDをMicrosoftのサードパーティCookie IDに永続化します。[Microsoft Advertising Conversion APIコネクタ](https://docs.tealium.com/microsoft-advertising-conversion-api-connector/)を使用する場合に推奨されます。
* **Ad Storage Consent**：広告保存に対するデフォルトの同意を構成します。**Data Mappings**セクションで`ad_storage`パラメータをマッピングすることにより、この値を動的に更新できます。
* **Automatically read from Tealium Consent Cookie**：`true`に構成すると、[Tealium同意管理](https://docs.tealium.com/about-consent-management/)に基づいて同意が構成されます。
* **Generate Event ID**：トラッキングイベントごとにイベントIDを自動生成します。[Microsoft Advertising Conversion APIコネクタ](https://docs.tealium.com/microsoft-advertising-conversion-api-connector/)を使用する場合の重複除外に推奨されます。

### Conversions API


<blockquote>
この機能を使用するには、有効な[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)が必要です。
</blockquote>


Microsoft Advertising Conversion APIをサポートするには、**Generate Event ID**を`true`に構成します。**Generate Event ID**を有効にすると、このタグはトラッキング対象の各イベントに一意のイベントIDを生成し、Microsoft Advertising Conversion APIコネクタで使用するための属性としてイベントストリーミングに送信するとともに、`event_id`パラメータでMicrosoft Advertising UETタグに渡します。このイベントID属性をコネクタでマッピングすることで、Webベースのタグとサーバーサイド統合を同期できます。

タグは、以下の命名規則に従って生成されたイベント属性を使用してイベントIDを送信します。

```nohl
microsoft_event_id_{EVENT_TYPE}_{TAG_UID}
```

たとえば、タグ#88の購入イベントでは、以下の属性と値が送信されます。

```json
{
  "microsoft_event_id_purchase_88": "028b2ade7478..."
}
```

同じタグのページ読み込みイベントでは、以下の属性と値が送信されます。

```json
{
  "microsoft_event_id_pageload_88": "084b1cda7461..."
}
```

#### 重複除外

イベントを適切に重複除外するには、Microsoft Advertising UETタグのイベントIDを、Tealium Collectタグによって送信されるペイロードに含める必要があります。これを行うには、以下の手順を実行します。

* **Tag Timing**ドロップダウンから**Prioritized**を選択します。
* **Bundle Flag**トグルを`On`に構成します。
* [Load Order Manager画面](https://docs.tealium.com/load-order-manager/)を使用して、Microsoft Advertising UETタグがTealium Collectタグより先に実行されるようにします。Tealium Collectタグは最後に実行することを推奨します。

これらのイベントID属性の使用方法については、[Microsoft Advertising Conversion APIコネクタ：重複除外](https://docs.tealium.com/microsoft-advertising-conversion-api-connector/#deduplication)を参照してください。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## 同意モード

このタグに同意モードを実装する方法は2つあります。

* [クライアントサイドの同意管理](https://docs.tealium.com/about-consent-management/)を使用し、Tealium同意Cookieを自動的に読み取ります。
* [JavaScriptコード拡張機能](https://docs.tealium.com/javascript-code-extension/)を追加し、同意管理プラットフォーム（CMP）の同意選択とカテゴリマッピングをこのタグにマッピングします。

訪問が同意を選択すると、タグはファーストパーティCookieとサードパーティCookieに対して適切な処理を選択します。

* **Granted**：ファーストパーティCookieとサードパーティCookieの両方を読み書きできます。
* **Denied**：ファーストパーティCookieは読み書きされません。サードパーティCookieは広告目的ではなく、不正行為およびスパム対策の目的に限り、読み取り専用で使用されます。

### クライアントサイドの同意管理

クライアントサイドの同意管理を使用してこのタグに同意モードを実装するには、タグ構成で**Automatically read from Tealium Consent Cookie**を`true`に構成します。

### JavaScriptコード拡張機能

エンドユーザーの同意選択をMicrosoftの同意モード構成にマッピングするには、JavaScriptコード拡張機能を使用します。拡張機能を以下のように構成します。

* **Scope**を**After Load Rules (default)**に構成します。
* **Occurrence**を**Run Always**に構成します。
* 使用しているCMPのJavaScriptコードを入力します。以下のコードテンプレート内の`CUSTOM_LOGIC`をベンダー固有のロジックに置き換えることで、CMPに合わせてカスタマイズできます。

```js
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = CUSTOM_LOGIC ? 'granted' : 'denied';
```

たとえば、以下はOneTrust用のコードです。

```js
// After Load Rules - Run Always
b.consent_decision = (tealiumConsentRegister && tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = b.consent_decision.indexOf('C0004') !== -1  ? 'granted' : 'denied';
```

これらとまったく同じ変数名を使用する場合、追加のマッピングは必要ありません。最新バージョンのタグでは、これらの変数がデフォルトで使用されます。個別のユースケースに応じて`ad_storage`パラメータを属性にマッピングすることで、これらの変数を上書きできます。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは以下のとおりです。
### 標準

|変数| 説明|
|---| ---|
|`tagid`|  <ul><li>タグ ID。</li><li>Microsoft Advertising から提供されたタグ識別子。</li></ul> |
|`event_category`|  <ul><li>イベントカテゴリ。</li><li>追跡対象の要素またはオブジェクトに関する情報を送信します。</li><li>例：`Button`。</li></ul> |
|`event_action`|  <ul><li>イベントアクション。</li><li>ユーザーのアクションを送信します。</li><li>例：`click`、`mousedown`。</li></ul> |
|`event_label`|  <ul><li>イベントラベル。</li><li>イベント目標に関する情報を示すラベルまたは詳細を送信します。</li><li>例：`Product demo`。</li></ul> |
|`event_value`|  <ul><li>イベント値。</li><li>イベント目標の数値を送信します。</li></ul> |
|`description`|  <ul><li>エラーの説明。</li><li>ユーザーが遭遇したエラーの説明。</li></ul> |
|`fatal`|  <ul><li>致命的エラー。</li><li>ユーザーが遭遇したエラーが致命的かどうか。</li></ul> |
|`method`|  <ul><li>メソッド。</li><li>ユーザーのアクションに関連付けられたメソッド。</li></ul> |
|`screen_name`|  <ul><li>画面名。</li><li>ユーザーが現在表示している画面に関連付けられた名前。</li></ul> |
|`search_term`|  <ul><li>検索語句。</li><li>ユーザーの検索で使用された語句。</li></ul> |
|`content_type`|  <ul><li>コンテンツタイプ。</li><li>ユーザーが選択したコンテンツのタイプ。</li></ul> |
|`content_id`|  <ul><li>コンテンツ ID。</li><li>ユーザーが選択したコンテンツの ID。</li></ul> |
|`promotion_creative_name`|  <ul><li>プロモーションクリエイティブ名のリスト。</li><li>プロモーションで使用されるクリエイティブ名の配列。</li></ul> |
|`promotion_creative_slot`|  <ul><li>プロモーションクリエイティブスロットのリスト。</li><li>プロモーションで使用されるクリエイティブスロット名の配列。</li></ul> |
|`promotion_id`|  <ul><li>プロモーション ID のリスト。</li><li>プロモーションで使用されるプロモーション ID の配列。</li></ul> |
|`promotion_name`|  <ul><li>プロモーション名のリスト。</li><li>プロモーションで使用されるプロモーション名の配列。</li></ul> |
| `enableAutoSpaTracking` | SPA の自動追跡を有効にします。 |
| `id_sync_beacon` | ID 同期ビーコン。 |
| `customer_id` | Microsoft 顧客 ID。 |
| `visitor_id` | 訪問 ID。 |
| `user_id` | ユーザー ID。 |
|`custom.myvar`|  <ul><li>カスタムプロパティ／パラメーター。</li><li>イベント用のカスタムプロパティ。</li><li>すべてのイベントとともに送信されます。特定のイベントにプロパティを構成するには、イベントパラメーターを使用します。</li><li>`myvar` をプロパティ名に置き換えてください。</li></ul> |
| `generate_event_id` | `Boolean` | イベント ID を生成します。 |
| `event_id` | `String` | イベント ID。 |

### E コマース

|変数| 説明|
|---| ---|
|`checkout_step`|  <ul><li>チェックアウトのステップ。</li><li>ユーザーが現在実行しているチェックアウトプロセスのステップ。</li></ul> |
|`checkout_option`|  <ul><li>チェックアウトオプション。</li><li>ユーザーが現在選択しているチェックアウトオプション。</li></ul> |
|`order_id`|  <ul><li>注文 ID。</li><li>デフォルトの E コマース値 `_corder` を上書きするために使用します。</li></ul> |
|`order_subtotal`|  <ul><li>小計。</li><li>デフォルトの E コマース値 `_csubtotal` を上書きするために使用します。</li></ul> |
|`order_shipping`|  <ul><li>配送料。</li><li>デフォルトの E コマース値 `_cship` を上書きするために使用します。</li></ul> |
|`order_tax`|  <ul><li>税額。</li><li>デフォルトの E コマース値 `_ctax` を上書きするために使用します。</li></ul> |
|`order_currency`|  <ul><li>通貨。</li><li>デフォルトの E コマース値 `_ccurrency` を上書きするために使用します。</li></ul> |
|`order_coupon_code`|  <ul><li>プロモーションコード。</li><li>デフォルトの E コマース値 `_cpromo` を上書きするために使用します。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>商品 ID のリスト。</li><li>デフォルトの E コマース値 `_cprod` を上書きするために使用します。</li></ul> |
|`product_name`|  <ul><li>配列</li><li>名前のリスト。</li><li>デフォルトの E コマース値 `_cprodname` を上書きするために使用します。</li></ul> |
|`product_brand`|  <ul><li>配列</li><li>ブランドのリスト。</li><li>デフォルトの E コマース値 `_cbrand` を上書きするために使用します。</li></ul> |
|`product_category`|  <ul><li>配列</li><li>カテゴリのリスト。</li><li>デフォルトの E コマース値 `_ccat` を上書きするために使用します。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト。</li><li>デフォルトの E コマース値 `_cquan` を上書きするために使用します。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト。</li><li>デフォルトの E コマース値 `_cprice` を上書きするために使用します。</li></ul> |
| 商品クリエイティブ名のリスト |  <ul><li>配列</li><li>商品に使用されるクリエイティブ名の配列。</li></ul> |
| 商品クリエイティブスロットのリスト |  <ul><li>配列</li><li>商品に使用されるクリエイティブスロットの配列。</li></ul> |
| 商品ロケーション ID のリスト |  <ul><li>配列</li><li>商品に使用されるロケーション ID の配列。</li></ul> |

### イベントとエンゲージメント

ページ上で特定のイベントをトリガーするには、これらの送信先にマッピングします。

イベントをトリガーするには、次の手順を実行します。

1. リストからイベントを選択します。  
事前定義されたリストから選択するか、カスタムイベントを作成します。
  * カスタムイベントの場合は、イベントを識別するための名前を入力します。

1. **トリガー**フィールドに、マッピングする変数の値を入力します。
1. さらにイベントをマッピングするには、プラス記号（**+**）をクリックし、手順 1 と 2 を繰り返します。
1. **適用**をクリックします。  
指定された値がデータレイヤー内で見つかると、イベントがトリガーされます。

|変数| 説明|
|---| ---|
|`add_payment_info`|  <ul><li>支払い情報を追加。</li><li>ユーザーがトランザクションに新しい支払い情報を追加しました。</li></ul> |
|`add_to_cart`|  <ul><li>カートに追加。</li><li>ユーザーがショッピングカートに 1 つ以上の商品を追加しました。</li></ul> |
|`add_to_wishlist`|  <ul><li>ウィッシュリストに追加。</li><li>ユーザーがウィッシュリストに 1 つ以上の商品を追加しました。</li></ul> |
|`begin_checkout`|  <ul><li>チェックアウトを開始。</li><li>ユーザーがチェックアウトプロセスを開始しました。</li></ul> |
|`checkout_progress`|  <ul><li>チェックアウトの進行状況。</li><li>ユーザーがチェックアウトプロセス内のステップを移動しました。</li></ul> |
|`exception`|  <ul><li>例外。</li><li>ユーザーが例外に遭遇しました。</li></ul> |
|`generate_lead`|  <ul><li>リードを生成。</li><li>ユーザーのアクションによってリードが生成されました。</li></ul> |
|`login`|  <ul><li>ログイン。</li><li>ユーザーがログインしました。</li></ul> |
|`page_view`|  <ul><li>ページビュー。</li><li>ユーザーがページを閲覧しました。</li></ul> |
|`purchase`|  <ul><li>購入。</li><li>ユーザーが 1 つ以上の商品の購入を完了しました。</li></ul> |
|`refund`|  <ul><li>返金。</li><li>ユーザーが 1 つ以上の商品について返金をリクエストしました。</li></ul> |
|`remove_from_cart`|  <ul><li>カートから削除。</li><li>ユーザーがショッピングカートから 1 つ以上の商品を削除しました。</li></ul> |
|`screen_view`|  <ul><li>画面ビュー。</li><li>ユーザーが画面を表示しました。</li></ul> |
|`search`|  <ul><li>検索。</li><li>ユーザーが検索しました。</li></ul> |
|`select_content`|  <ul><li>コンテンツを選択。</li><li>ユーザーが 1 つ以上のコンテンツ項目を選択しました。</li></ul> |
|`set_checkout_option`|  <ul><li>チェックアウトオプションを構成。</li><li>ユーザーが現在のチェックアウトステップでチェックアウトオプションを選択しました。</li></ul> |
|`share`|  <ul><li>共有</li><li>ユーザーがコンテンツを共有しました。</li></ul> |
|`sign_up`|  <ul><li>登録。</li><li>ユーザーが登録しました。</li></ul> |
|`timing_complete`|  <ul><li>タイミング完了。</li><li>ユーザーのページ読み込みに関するタイミング情報。</li></ul> |
|`view_item`|  <ul><li>商品を表示。</li><li>ユーザーが単一の商品（多くの場合は詳細ページ）を表示しました。</li></ul> |
|`view_item_list`|  <ul><li>商品リストを表示。</li><li>ユーザーが 1 つ以上の商品を含むリストページを表示しました。</li></ul> |
|`view_promotion`|  <ul><li>プロモーションを表示。</li><li>ユーザーがプロモーションをクリックしました。</li></ul> |
|`view_search_results`|  <ul><li>検索結果を表示。</li><li>ユーザーが検索結果を表示しました。</li></ul> |
| `update_consent` | <ul><li>同意を更新。</li></ul>  |
|`custom`|  <ul><li>カスタムイベント。</li><li>ユーザーがカスタムイベントに関連するアクションを開始しました。</li></ul> |
### 商品オーディエンスイベント

ページ上で特定のイベントをトリガーするには、これらの送信先にマッピングします。

イベントをトリガーするには、次の手順を実行します。

1. リストからイベントを選択します。  
定義済みリストから選択するか、カスタムイベントを作成します。
  * カスタムイベントの場合は、イベントを識別するための名前を入力します。

1. **トリガー**フィールドに、マッピングする変数の値を入力します。
1. さらにイベントをマッピングするには、プラス記号（**+**）をクリックし、手順1と2を繰り返します。
1. **適用**をクリックします。  
指定した値がデータレイヤーで見つかると、イベントがトリガーされます。

|変数| 説明|
|---| ---|
|`retail`|  <ul><li>小売。</li><li>小売業向けマーケティングのデータを送信します。</li></ul> |
|`travel`|  <ul><li>旅行。</li><li>旅行業向けマーケティングのデータを送信します。</li></ul> |
|`hotel`|  <ul><li>ホテル。</li><li>ホテル業向けマーケティングのデータを送信します。</li></ul> |

### 拡張コンバージョンデータ

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `em` | `String` | メールアドレス。 |
| `ph` | `String` | 電話番号。 |

### 同意管理

| 変数 | 説明 |
|:---------|:------------|
| `ad_storage` | 広告保存。 |

### イベントパラメーター

先にマッピングしたイベントとともに追加データを渡す場合は、これらの送信先にマッピングします。


<blockquote>
パラメーターは定義済みイベントでのみ使用されます。カスタムイベントでパラメーターを渡す方法の詳細については、を参照してください。
</blockquote>


定義済みイベントでパラメーターを渡すには、次の手順を実行します。

1. リストからイベントを選択します。
1. リストからパラメーターを選択します。  
カスタムパラメーターを使用する場合は、パラメーターを識別するための名前を入力します。
1. **追加**をクリックします。

|変数| 説明|
|---| ---|
|`event_category`|  <ul><li>イベントカテゴリー。</li><li>現在のイベントのカテゴリー。</li><li>クリックされたボタンなど、要素またはオブジェクトに関する情報を送信します。</li></ul> |
|`event_action`|  <ul><li>イベントアクション。</li><li>現在のイベントのアクション名。</li><li>クリックやマウスダウンなどのユーザーアクションを送信します。</li></ul> |
|`event_label`|  <ul><li>イベントラベル。</li><li>現在のイベントのラベル。</li><li>商品目標に関する商品デモなどの情報ラベルや詳細を送信します。</li></ul> |
|`event_value`|  <ul><li>イベント値。</li><li>現在のイベントにおけるイベント目標の数値を送信します。</li></ul> |
|`custom`|  <ul><li>カスタムプロパティ／パラメーター。</li><li>現在のイベントに関連付けられたカスタムプロパティ。</li></ul> |
|`description`|  <ul><li>エラーの説明。</li><li>ユーザーが遭遇したエラーの説明。</li></ul> |
|`fatal`|  <ul><li>致命的エラー。</li><li>ユーザーが遭遇したエラーが致命的かどうか。</li></ul> |
|`method`|  <ul><li>メソッド。</li><li>ユーザーのアクションに関連付けられたメソッド。</li></ul> |
|`screen_name`|  <ul><li>画面名。</li><li>ユーザーが現在表示している画面に関連付けられた名前。</li></ul> |
|`search_term`|  <ul><li>検索語句。</li><li>ユーザーの検索で使用された語句。</li></ul> |
|`content_type`|  <ul><li>コンテンツタイプ。</li><li>ユーザーが選択したコンテンツのタイプ。</li></ul> |
|`content_id`|  <ul><li>コンテンツID。</li><li>ユーザーが選択したコンテンツのID。</li></ul> |
|`checkout_step`|  <ul><li>チェックアウト手順。</li><li>ユーザーが現在行っているチェックアウトプロセスの手順。</li></ul> |
|`checkout_option`|  <ul><li>チェックアウトオプション。</li><li>ユーザーが現在選択しているチェックアウトオプション。</li></ul> |
|`order_id`|  <ul><li>注文ID。</li><li>デフォルトのEコマース値`_corder`を上書きする場合に使用します。</li></ul> |
|`order_total`|  <ul><li>注文合計。</li><li>デフォルトのEコマース値`_ctotal`を上書きする場合に使用します。</li></ul> |
|`order_subtotal`|  <ul><li>小計。</li><li>デフォルトのEコマース値`_csubtotal`を上書きする場合に使用します。</li></ul> |
|`order_shipping`|  <ul><li>配送料。</li><li>デフォルトのEコマース値`_cship`を上書きする場合に使用します。</li></ul> |
|`order_tax`|  <ul><li>税額。</li><li>デフォルトのEコマース値`_ctax`を上書きする場合に使用します。</li></ul> |
|`order_currency`|  <ul><li>通貨。</li><li>デフォルトのEコマース値`_ccurrency`を上書きする場合に使用します。</li></ul> |
|`order_coupon_code`|  <ul><li>プロモーションコード。</li><li>デフォルトのEコマース値`_cpromo`を上書きする場合に使用します。</li></ul> |
|`product_id`|  <ul><li>商品IDのリスト。</li><li>デフォルトのEコマース値`_cprod`を上書きする場合に使用します。</li></ul> |
|`product_name`|  <ul><li>名前のリスト。</li><li>デフォルトのEコマース値`_cprodname`を上書きする場合に使用します。</li></ul> |
|`product_brand`|  <ul><li>ブランドのリスト。</li><li>デフォルトのEコマース値`_cbrand`を上書きする場合に使用します。</li></ul> |
|`product_category`|  <ul><li>カテゴリーのリスト。</li><li>デフォルトのEコマース値`_ccat`を上書きする場合に使用します。</li></ul> |
|`product_quantity`|  <ul><li>数量のリスト。</li><li>デフォルトのEコマース値`_cquan`を上書きする場合に使用します。</li></ul> |
|`product_unit_price`|  <ul><li>価格のリスト。</li><li>デフォルトのEコマース値`_cprice`を上書きする場合に使用します。</li></ul> |
|`product_creative_name`|  <ul><li>配列</li><li>商品クリエイティブ名のリスト。</li><li>商品に使用されるクリエイティブ名の配列。</li></ul> |
|`product_creative_slot`|  <ul><li>配列</li><li>商品クリエイティブスロットのリスト。</li><li>商品に使用されるクリエイティブスロットの配列。</li></ul> |
|`promotion_creative_name`|  <ul><li>配列</li><li>プロモーションクリエイティブ名のリスト。</li><li>プロモーションで使用されるクリエイティブ名の配列。</li></ul> |
|`promotion_creative_slot`|  <ul><li>配列</li><li>プロモーションクリエイティブスロットのリスト。</li><li>プロモーションで使用されるクリエイティブスロット名の配列。</li></ul> |
|`promotion_id`|  <ul><li>配列</li><li>プロモーションIDのリスト。</li><li>プロモーションで使用されるプロモーションIDの配列。</li></ul> |
|`promotion_name`|  <ul><li>配列</li><li>プロモーション名。</li><li>プロモーションで使用されるプロモーション名の配列。</li></ul> |
### 商品オーディエンスのパラメーター

先にマッピングしたイベントとともに追加データを渡す場合は、これらの送信先にマッピングします。


<blockquote>
パラメーターは定義済みイベントでのみ使用されます。カスタムイベントとともにパラメーターを渡す方法について詳しくは、を参照してください。
</blockquote>


定義済みイベントとともにパラメーターを渡すには、次の手順を実行します。

1. リストからイベントを選択します。
1. リストからパラメーターを選択します。  
カスタムパラメーターを使用する場合は、その識別に使用する名前を入力します。
1. **追加**をクリックします。

|変数| 説明|
|---| ---|
|`ecomm_prodid`|  <ul><li>商品 ID。</li><li>現在ユーザーに表示されている、またはユーザーが選択した 1 つ以上の ID。</li></ul> |
|`ecomm_pagetype`|  <ul><li>ページタイプ。</li><li>現在ユーザーに表示されているページのタイプ。</li></ul> |
|`ecomm_totalvalue`|  <ul><li>合計金額。</li><li>現在ユーザーに関連付けられている合計金額。</li></ul> |
|`ecomm_category`|  <ul><li>カテゴリー。</li><li>現在ユーザーに表示されているカテゴリー。</li></ul> |
|`travel_destid`|  <ul><li>目的地 ID。</li><li>ユーザーが選択した目的地の ID。</li></ul> |
|`travel_originid`|  <ul><li>出発地 ID。</li><li>ユーザーの出発地の ID。</li></ul> |
|`travel_startdate`|  <ul><li>旅行開始日。</li><li>ユーザーが旅行を開始する日付。</li></ul> |
|`travel_enddate`|  <ul><li>旅行終了日。</li><li>ユーザーが旅行を終了する日付。</li></ul> |
|`travel_totalvalue`|  <ul><li>合計金額。</li><li>ユーザーが予定している旅行の合計金額。</li></ul> |
|`hct_bpr`|  <ul><li>ホテルの基本料金。</li><li>ユーザーが予約しようとしているホテルの基本料金。</li></ul> |
|`hct_tpr`|  <ul><li>ホテルの合計料金。</li><li>ユーザーが予約しようとしているホテルの、税金と割引を含む合計料金。</li></ul> |
|`hct_bid`|  <ul><li>ホテル予約 ID。</li><li>ユーザーの予約の ID。</li></ul> |
|`hct_cid`|  <ul><li>ホテルのチェックイン日。</li><li>ユーザーの宿泊におけるチェックイン日。</li></ul> |
|`hct_cod`|  <ul><li>ホテルのチェックアウト日。</li><li>ユーザーの宿泊におけるチェックアウト日。</li></ul> |
|`hct_los`|  <ul><li>ホテルの宿泊期間。</li><li>ユーザーの合計宿泊期間。</li></ul> |
|`hct_pid`|  <ul><li>ホテルパートナー ID。</li><li>ユーザーが予約しようとしているホテルのパートナー ID。</li></ul> |
|`hct_pagetype`|  <ul><li>ホテルページのタイプ。</li><li>現在ユーザーに表示されているページのタイプ。</li></ul> |

### 商品オーディエンス - 小売

| 変数           | 説明             |
| ------------------ | --------------- |
| `ecomm_prodid`     | <ul><li>商品 ID。</li><li>現在ユーザーに表示されている、またはユーザーが選択した 1 つ以上の ID。</li></ul>      |
| `ecomm_pagetype`   | <ul><li>ページタイプ。</li><li>現在ユーザーに表示されているページのタイプ。</li><li>`home`、`searchresults`、`category`、`product`、`cart`、`purchase`、または `other` のいずれか。</li></ul> |
| `ecomm_totalvalue` | <ul><li>合計金額。</li><li>現在ユーザーに関連付けられている合計金額。</li></ul>            |
| `ecomm_category`   | <ul><li>カテゴリー。</li><li>現在ユーザーに表示されているカテゴリー。</li></ul>   |

### 商品オーディエンス - 旅行

|変数| 説明|
|---| ---|
|`travel_destid`|  <ul><li>目的地 ID。</li><li>ユーザーが選択した目的地の ID。</li></ul> |
|`travel_originid`|  <ul><li>出発地 ID。</li><li>ユーザーの出発地の ID。</li></ul> |
|`travel_pagetype`|  <ul><li>ページタイプ。</li><li>現在ユーザーに表示されているページのタイプ。</li><li>`home`、`searchresults`、`offerdetail`、`conversionintent`、`conversion`、`cancel`、または `other` のいずれか。</li></ul> |
|`travel_startdate`|  <ul><li>旅行開始日。</li><li>ユーザーが旅行を開始する日付。</li><li>日付形式は `YYYY-MM-DD` です。</li></ul> |
|`travel_enddate`|  <ul><li>旅行終了日。</li><li>ユーザーが旅行を終了する日付。</li><li>日付形式は `YYYY-MM-DD` です。</li></ul> |
|`travel_totalvalue`|  <ul><li>合計金額。</li><li>ユーザーが予定している旅行の合計金額。</li></ul> |

### 商品オーディエンス - ホテル

|変数| 説明|
|---| ---|
|`hct_base_price`|  <ul><li>ホテルの基本料金。</li><li>ユーザーが予約しようとしているホテルの基本料金。</li></ul> |
|`hct_total_price`|  <ul><li>ホテルの合計料金。</li><li>ユーザーが予約しようとしているホテルの、税金と割引を含む合計料金。</li></ul> |
| `hct_checkin_date` |  <ul><li>ホテルのチェックイン日。</li><li>ユーザーの宿泊におけるチェックイン日。</li><li>日付形式は `YYYY-MM-DD` です。</li></ul> |
| `hct_checkout_date` |  <ul><li>ホテルのチェックアウト日。</li><li>ユーザーの宿泊におけるチェックアウト日。</li><li>日付形式は `YYYY-MM-DD` です。</li></ul> |
|`hct_length_of_stay`|  <ul><li>ホテルの宿泊期間。</li><li>ユーザーの合計宿泊期間。</li></ul> |
|`hct_partner_hotel_id`|  <ul><li>ホテルパートナー ID。</li><li>ユーザーが予約しようとしているホテルのパートナー ID。</li></ul> |
| `hct_booking_ref` |  <ul><li>難読化された予約参照番号。</li></ul> |
| `hct_pagetype` |  <ul><li>ホテルページのタイプ。</li><li>現在ユーザーに表示されているページのタイプ。</li><li>`home`、`searchresults`、`property`、`cart`、`purchase`、`cancel`、または `other` のいずれか。</li></ul> |

## ベンダーのドキュメント

* [Microsoft Bing：売上およびその他のコンバージョンのトラッキング](http://help.bingads.microsoft.com/#apex/3/en/n5012/2)
* [Microsoft Bing：UET とは何か、どのように役立つのか](https://help.bingads.microsoft.com/#apex/3/en/56681/0)
* [Microsoft Bing：よくある質問](http://help.bingads.microsoft.com/apex/index/3/en-us/53056)