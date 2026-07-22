---
title: Microsoft Advertising Universal Event Tracking (UET) タグ構成ガイド
description: この記事では、Microsoft Advertising Universal Event Tracking (UET) タグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/microsoft-advertising-universal-event-tracking-uet-tag/
---
## タグのヒント

* マッピングを使用して:
  * 標準構成値を上書きします。
  * E-Commerce 拡張値を上書きします。
  * カスタムパラメータを渡します。
  * イベントトリガーを構成します。
* **Standard** タブで **Custom Property/Parameter** にパラメータをマッピングすると、そのパラメータはすべてのイベントに送信されます。特定のイベントにのみデータを送信するには、**Event Parameters** タブを使用します。
* 次の E-Commerce 拡張値をサポートします:
  * 注文ID。
  * 注文小計。
  * 注文送料。
  * 注文税金。
  * 注文通貨。
  * 注文クーポン/プロモーションコード。
  * 製品IDのリスト。
  * 名前のリスト。
  * ブランドのリスト。
  * カテゴリのリスト。
  * 数量のリスト。
  * 価格のリスト。

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を構成します:

* **Tag ID**: あなたのMicrosoft Advertisingタグ識別子。
* **ID Sync Beacon**: 内部ユーザーIDをMicrosoftサードパーティクッキーIDに持続させます。[Microsoft UET Conversion APIコネクタ](https://docs.tealium.com/microsoft-uet-conversion-api-connector/)を使用する場合に推奨されます。
* **Ad Storage Consent**: 広告保存のデフォルト同意を構成します。`ad_storage`パラメータを**Data Mappings**セクションでマッピングすることにより、この値を動的に更新します。
* **Automatically read from Tealium Consent Cookie**: `true`に構成すると、[Tealium consent manager](https://docs.tealium.com/about-consent-management/)に基づいて同意が構成されます。
* **Generate Event ID**: すべてのトラッキングイベントに対して自動的にイベントIDを生成します。[Microsoft UET Conversion APIコネクタ](https://docs.tealium.com/microsoft-uet-conversion-api-connector/)を使用する際の重複排除に推奨されます。

### Conversions API


<blockquote>
この機能にはアクティブな[Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/)が必要です。
</blockquote>


Microsoft UET Conversion APIをサポートするためには、**Generate Event ID**を`true`に構成します。**Generate Event ID**が有効になっている場合、このタグは各イベントに対して一意のイベントIDを生成し、それをTealium EventStreamに属性として送信し、Microsoft UET Conversion APIコネクタで使用し、`event_id`パラメータでMicrosoft Advertising UETタグに渡します。このイベントID属性は、コネクタでウェブベースのタグとサーバーサイドの統合を同期するためにマッピングされる場合があります。

タグは次の命名規則を使用してイベントIDを生成したイベント属性を送信します:

```nohl
microsoft_event_id_{EVENT_TYPE}_{TAG_UID}
```

たとえば、タグ#88からの購入イベントは次の属性と値を送信します:

```json
{
  "microsoft_event_id_purchase_88": "028b2ade7478..."
}
```

同じタグからのページロードイベントは次の属性と値を送信します:

```json
{
  "microsoft_event_id_pageload_88": "084b1cda7461..."
}
```
#### 重複排除

適切なイベント重複排除を確実に行うためには、Microsoft Advertising UETタグからのイベントIDをTealium Collectタグによって送信されるペイロードに含める必要があります。これを行うには、次の手順を使用します:

* **Tag Timing** ドロップダウンから **Prioritized** を選択します。
* **Bundle Flag** トグルを `On` に構成します。
* [Load Order Manager screen](https://docs.tealium.com/load-order-manager/)を使用して、Tealium Collectタグの前にMicrosoft Advertising UETタグを発火させます。Tealium Collectタグは最後に発火させることをお勧めします。
これらのイベントID属性の使用に関する情報については、[Microsoft UET Conversion APIコネクタ: 重複排除](https://docs.tealium.com/microsoft-uet-conversion-api-connector/#deduplication)を参照してください。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## 同意モード

このタグに対して同意モードを実装するには2つのオプションがあります:

* [クライアントサイド同意管理](https://docs.tealium.com/about-consent-management/)を使用し、Tealium同意クッキーを自動的に読み取ります。
* [JavaScript Code extension](https://docs.tealium.com/javascript-code-extension/)を追加して、同意管理プラットフォーム（CMP）からこのタグへの同意選択とカテゴリマッピングをマップします。

訪問が同意選択を行うと、タグは第一者および第三者クッキーに対して適切なアプローチを選択します:

* **Granted**: 第一者および第三者クッキーの両方を読み書きできます。
* **Denied**: 第一者クッキーは読み書きされず、第三者クッキーは詐欺およびスパム目的でのみ読み取り可能で、広告目的ではありません。

### クライアントサイド同意管理

このタグの同意モードをクライアントサイド同意管理を使用して実装するには、タグ構成で**Automatically read from Tealium Consent Cookie**を`true`に構成します。

### JavaScript Code extension

エンドユーザーの同意選択をMicrosoft同意モード構成にマッピングするには、JavaScript Code extensionを使用します。拡張機能を次のように構成します:

* **Scope** を **After Load Rules (default)** に構成します。
* **Occurrence** を **Run Always** に構成します。
* あなたのCMPのためのロジックで `CUSTOM_LOGIC` を置き換えることによって、次のJavaScriptコードテンプレートをカスタマイズします。
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

これらの正確な変数名を使用する場合、追加のマッピングは必要ありません。タグの最新バージョンはデフォルトでこれらの変数を使用します。特定のケースの属性に `ad_storage` パラメータをマッピングすることによってこれらの変数を上書きします。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは次のとおりです:
### 標準

|変数| 説明|
|---| ---|
|`tagid`|  <ul><li>タグID。</li><li>Microsoft Advertisingから提供されるタグ識別子。</li></ul> |
|`event_category`|  <ul><li>イベントカテゴリ。</li><li>追跡される要素またはオブジェクトに関する情報を送信します。</li><li>例：`Button`。</li></ul> |
|`event_action`|  <ul><li>イベントアクション。</li><li>ユーザーアクションを送信します。</li><li>例：`click`, `mousedown`。</li></ul> |
|`event_label`|  <ul><li>イベントラベル。</li><li>イベント目標に関する情報ラベルまたは詳細を送信します。</li><li>例：`Product demo`。</li></ul> |
|`event_value`|  <ul><li>イベント値。</li><li>イベント目標の数値を送信します。</li></ul> |
|`description`|  <ul><li>エラー説明。</li><li>ユーザーが経験したエラーの説明。</li></ul> |
|`fatal`|  <ul><li>エラー致命的。</li><li>ユーザーが経験したエラーが致命的かどうか。</li></ul> |
|`method`|  <ul><li>方法。</li><li>ユーザーのアクションに関連する方法。</li></ul> |
|`screen_name`|  <ul><li>スクリーン名。</li><li>ユーザーが現在表示しているスクリーンの名前。</li></ul> |
|`search_term`|  <ul><li>検索用語。</li><li>ユーザーの検索で使用される用語。</li></ul> |
|`content_type`|  <ul><li>コンテンツタイプ。</li><li>ユーザーが選択したコンテンツのタイプ。</li></ul> |
|`content_id`|  <ul><li>コンテンツID。</li><li>ユーザーが選択したコンテンツのID。</li></ul> |
|`promotion_creative_name`|  <ul><li>プロモーションクリエイティブ名のリスト。</li><li>プロモーションで使用されるクリエイティブ名の配列。</li></ul> |
|`promotion_creative_slot`|  <ul><li>プロモーションクリエイティブスロットのリスト。</li><li>プロモーションで使用されるクリエイティブスロット名の配列。</li></ul> |
|`promotion_id`|  <ul><li>プロモーションIDのリスト。</li><li>プロモーションで使用されるプロモーションIDの配列。</li></ul> |
|`promotion_name`|  <ul><li>プロモーション名のリスト。</li><li>プロモーションで使用されるプロモーション名の配列。</li></ul> |
| `enableAutoSpaTracking` | 自動SPAトラッキングを有効にする。 |
| `id_sync_beacon` | ID同期ビーコン。 |
| `customer_id` | Microsoftの顧客ID。 |
| `visitor_id` | 訪問ID。 |
| `user_id` | ユーザーID。 |
|`custom.myvar`|  <ul><li>カスタムプロパティ/パラメータ。</li><li>イベント用のカスタムプロパティ。</li><li>すべてのイベントで送信され、特定のイベントのプロパティを構成するためにイベントパラメータを使用します。</li><li>`myvar`をプロパティの名前に置き換えてください。</li></ul> |
| `generate_event_id` | `Boolean` | イベントIDを生成します。 |
| `event_id` | `String` | イベントID。 |

### E-Commerce

|変数| 説明|
|---| ---|
|`checkout_step`|  <ul><li>チェックアウトステップ。</li><li>ユーザーが現在進行中のチェックアウトプロセスのステップ。</li></ul> |
|`checkout_option`|  <ul><li>チェックアウトオプション。</li><li>ユーザーが選択した現在のチェックアウトオプション。</li></ul> |
|`order_id`|  <ul><li>注文ID。</li><li>デフォルトのeコマース値 `_corder` を上書きするために使用します。</li></ul> |
|`order_subtotal`|  <ul><li>小計。</li><li>デフォルトのeコマース値 `_csubtotal` を上書きするために使用します。</li></ul> |
|`order_shipping`|  <ul><li>送料。</li><li>デフォルトのeコマース値 `_cship` を上書きするために使用します。</li></ul> |
|`order_tax`|  <ul><li>税金。</li><li>デフォルトのeコマース値 `_ctax` を上書きするために使用します。</li></ul> |
|`order_currency`|  <ul><li>通貨。</li><li>デフォルトのeコマース値 `_ccurrency` を上書きするために使用します。</li></ul> |
|`order_coupon_code`|  <ul><li>プロモーションコード。</li><li>デフォルトのeコマース値 `_cpromo` を上書きするために使用します。</li></ul> |
|`product_id`|  <ul><li>配列</li><li>製品IDのリスト。</li><li>デフォルトのeコマース値 `_cprod` を上書きするために使用します。</li></ul> |
|`product_name`|  <ul><li>配列</li><li>名前のリスト。</li><li>デフォルトのeコマース値 `_cprodname` を上書きするために使用します。</li></ul> |
|`product_brand`|  <ul><li>配列</li><li>ブランドのリスト。</li><li>デフォルトのeコマース値 `_cbrand` を上書きするために使用します。</li></ul> |
|`product_category`|  <ul><li>配列</li><li>カテゴリのリスト。</li><li>デフォルトのeコマース値 `_ccat` を上書きするために使用します。</li></ul> |
|`product_quantity`|  <ul><li>配列</li><li>数量のリスト。</li><li>デフォルトのeコマース値 `_cquan` を上書きするために使用します。</li></ul> |
|`product_unit_price`|  <ul><li>配列</li><li>価格のリスト。</li><li>デフォルトのeコマース値 `_cprice` を上書きするために使用します。</li></ul> |
| 製品クリエイティブ名のリスト |  <ul><li>配列</li><li>製品に使用されるクリエイティブ名の配列。</li></ul> |
| 製品クリエイティブスロットのリスト |  <ul><li>配列</li><li>製品に使用されるクリエイティブスロットの配列。</li></ul> |
| 製品ロケーションIDのリスト |  <ul><li>配列</li><li>製品に使用されるロケーションIDの配列。</li></ul> |

### イベントとエンゲージメント

特定のイベントをページ上でトリガーするためにこれらの宛先にマッピングします。

イベントをトリガーするための次のステップを使用します：

1. リストからイベントを選択します。  
事前定義されたリストから選択するか、カスタムイベントを作成します。
  * カスタムイベントの場合、それを識別する名前を入力します。

1. **トリガー**フィールドにマッピングされる変数の値を入力します。
1. より多くのイベントをマッピングするには、プラス記号 (**+**) をクリックしてステップ1と2を繰り返します。
1. **適用**をクリックします。  
データレイヤーに提供された値が見つかったときにイベントがトリガーされます。

|変数| 説明|
|---| ---|
|`add_payment_info`|  <ul><li>支払情報の追加。</li><li>ユーザーが取引に新しい支払情報を追加しました。</li></ul> |
|`add_to_cart`|  <ul><li>カートに追加。</li><li>ユーザーがショッピングカートに一つ以上のアイテムを追加しました。</li></ul> |
|`add_to_wishlist`|  <ul><li>ウィッシュリストに追加。</li><li>ユーザーがウィッシュリストに一つ以上のアイテムを追加しました。</li></ul> |
|`begin_checkout`|  <ul><li>チェックアウトの開始。</li><li>ユーザーがチェックアウトプロセスを開始しました。</li></ul> |
|`checkout_progress`|  <ul><li>チェックアウトの進行。</li><li>ユーザーがチェックアウトの進行でステップを交換しました。</li></ul> |
|`exception`|  <ul><li>例外。</li><li>ユーザーが例外に遭遇しました。</li></ul> |
|`generate_lead`|  <ul><li>リードの生成。</li><li>ユーザーのアクションがリードを生成しました。</li></ul> |
|`login`|  <ul><li>ログイン。</li><li>ユーザーがログインしました。</li></ul> |
|`page_view`|  <ul><li>ページビュー。</li><li>ユーザーがページを閲覧しました。</li></ul> |
|`purchase`|  <ul><li>購入。</li><li>ユーザーが一つ以上の製品の購入を完了しました。</li></ul> |
|`refund`|  <ul><li>払い戻し。</li><li>ユーザーが一つ以上の製品に対して払い戻しを要求しました。</li></ul> |
|`remove_from_cart`|  <ul><li>カートから削除。</li><li>ユーザーがショッピングカートから一つ以上のアイテムを削除しました。</li></ul> |
|`screen_view`|  <ul><li>スクリーンビュー。</li><li>ユーザーがスクリーンを閲覧しました。</li></ul> |
|`search`|  <ul><li>検索。</li><li>ユーザーが検索しました。</li></ul> |
|`select_content`|  <ul><li>コンテンツの選択。</li><li>ユーザーが一つ以上のコンテンツアイテムを選択しました。</li></ul> |
|`set_checkout_option`|  <ul><li>チェックアウトオプションの構成。</li><li>ユーザーが現在のチェックアウトステップのためのチェックアウトオプションを選択しました。</li></ul> |
|`share`|  <ul><li>共有</li><li>ユーザーがコンテンツを共有しました。</li></ul> |
|`sign_up`|  <ul><li>サインアップ。</li><li>ユーザーがサインアップしました。</li></ul> |
|`timing_complete`|  <ul><li>タイミング完了。</li><li>ユーザーのページロードのタイミング情報。</li></ul> |
|`view_item`|  <ul><li>アイテム表示。</li><li>ユーザーが単一のアイテム、通常は詳細ページを閲覧しました。</li></ul> |
|`view_item_list`|  <ul><li>アイテムリスト表示。</li><li>ユーザーが一つ以上のアイテムが含まれるリストページを閲覧しました。</li></ul> |
|`view_promotion`|  <ul><li>プロモーション表示。</li><li>ユーザーがプロモーションをクリックしました。</li></ul> |
|`view_search_results`|  <ul><li>検索結果表示。</li><li>ユーザーが検索の結果を閲覧しました。</li></ul> |
| `update_consent` | <ul><li>同意の更新。</li></ul>  |
|`custom`|  <ul><li>カスタムイベント。</li><li>ユーザーがカスタムイベントに関連するアクションを開始しました。</li></ul> |
### 製品オーディエンスイベント

特定のイベントをページでトリガーするためにこれらのデスティネーションにマッピングします。

イベントをトリガーするには、以下の手順を使用します：

1. リストからイベントを選択します。  
事前定義されたリストから選択するか、カスタムイベントを作成します。
  * カスタムイベントの場合、それを識別する名前を入力します。

1. **トリガー** フィールドに、マッピングされる変数の値を入力します。
1. より多くのイベントをマッピングするには、プラス記号（**+**）をクリックして、手順1と2を繰り返します。
1. **適用**をクリックします。  
提供された値がデータレイヤーで見つかったときにイベントがトリガーされます。

|変数| 説明|
|---| ---|
|`retail`|  <ul><li>小売。</li><li>小売ベースのマーケティングのためのデータを送信します。</li></ul> |
|`travel`|  <ul><li>旅行。</li><li>旅行ベースのマーケティングのためのデータを送信します。</li></ul> |
|`hotel`|  <ul><li>ホテル。</li><li>ホテルベースのマーケティングのためのデータを送信します。</li></ul> |

### エンリッチメントされたコンバージョンデータ

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `em` | `String` | メール。 |
| `ph` | `String` | 電話。 |

### 同意管理

| 変数 | 説明 |
|:---------|:------------|
| `ad_storage` | 広告保存。 |

### イベントパラメータ

以前にマッピングされたイベントに追加データを渡したい場合は、これらのデスティネーションにマッピングします。


<blockquote>
パラメータは事前定義されたイベントでのみ使用されます。カスタムイベントでパラメータを渡す方法の詳細については、を参照してください。
</blockquote>


事前定義されたイベントにパラメータを渡すための以下の手順を使用します：

1. リストからイベントを選択します。
1. リストからパラメータを選択します。  
カスタムパラメータを使用する場合は、それを識別する名前を入力します。
1. **追加**をクリックします。

|変数| 説明|
|---| ---|
|`event_category`|  <ul><li>イベントカテゴリ。</li><li>現在のイベントのカテゴリ。</li><li>クリックされたボタンなど、要素やオブジェクトに関する情報を送信します。</li></ul> |
|`event_action`|  <ul><li>イベントアクション。</li><li>現在のイベントのアクション名。</li><li>クリックやマウスダウンなどのユーザーアクションを送信します。</li></ul> |
|`event_label`|  <ul><li>イベントラベル。</li><li>現在のイベントのラベル。</li><li>製品デモなど、製品目標に関する情報ラベルや詳細を送信します。</li></ul> |
|`event_value`|  <ul><li>イベント値。</li><li>現在のイベントの目標値を数値で送信します。</li></ul> |
|`custom`|  <ul><li>カスタムプロパティ/パラメータ。</li><li>現在のイベントに関連するカスタムプロパティ。</li></ul> |
|`description`|  <ul><li>エラー説明。</li><li>ユーザーが経験したエラーの説明。</li></ul> |
|`fatal`|  <ul><li>エラー致命的。</li><li>ユーザーが経験したエラーが致命的かどうか。</li></ul> |
|`method`|  <ul><li>方法。</li><li>ユーザーのアクションに関連する方法。</li></ul> |
|`screen_name`|  <ul><li>スクリーン名。</li><li>ユーザーが現在閲覧しているスクリーンの名前。</li></ul> |
|`search_term`|  <ul><li>検索用語。</li><li>ユーザーの検索で使用された用語。</li></ul> |
|`content_type`|  <ul><li>コンテンツタイプ。</li><li>ユーザーが選択したコンテンツのタイプ。</li></ul> |
|`content_id`|  <ul><li>コンテンツID。</li><li>ユーザーが選択したコンテンツのID。</li></ul> |
|`checkout_step`|  <ul><li>チェックアウトステップ。</li><li>ユーザーが現在いるチェックアウトプロセスのステップ。</li></ul> |
|`checkout_option`|  <ul><li>チェックアウトオプション。</li><li>ユーザーが選択した現在のチェックアウトオプション。</li></ul> |
|`order_id`|  <ul><li>注文ID。</li><li>デフォルトのeコマース値 `_corder` を上書きするために使用します。</li></ul> |
|`order_total`|  <ul><li>注文合計。</li><li>デフォルトのeコマース値 `_ctotal` を上書きするために使用します。</li></ul> |
|`order_subtotal`|  <ul><li>小計。</li><li>デフォルトのeコマース値 `_csubtotal` を上書きするために使用します。</li></ul> |
|`order_shipping`|  <ul><li>送料。</li><li>デフォルトのeコマース値 `_cship` を上書きするために使用します。</li></ul> |
|`order_tax`|  <ul><li>税額。</li><li>デフォルトのeコマース値 `_ctax` を上書きするために使用します。</li></ul> |
|`order_currency`|  <ul><li>通貨。</li><li>デフォルトのeコマース値 `_ccurrency` を上書きするために使用します。</li></ul> |
|`order_coupon_code`|  <ul><li>プロモーションコード。</li><li>デフォルトのeコマース値 `_cpromo` を上書きするために使用します。</li></ul> |
|`product_id`|  <ul><li>製品IDのリスト。</li><li>デフォルトのeコマース値 `_cprod` を上書きするために使用します。</li></ul> |
|`product_name`|  <ul><li>名前のリスト。</li><li>デフォルトのeコマース値 `_cprodname` を上書きするために使用します。</li></ul> |
|`product_brand`|  <ul><li>ブランドのリスト。</li><li>デフォルトのeコマース値 `_cbrand` を上書きするために使用します。</li></ul> |
|`product_category`|  <ul><li>カテゴリのリスト。</li><li>デフォルトのeコマース値 `_ccat` を上書きするために使用します。</li></ul> |
|`product_quantity`|  <ul><li>数量のリスト。</li><li>デフォルトのeコマース値 `_cquan` を上書きするために使用します。</li></ul> |
|`product_unit_price`|  <ul><li>価格のリスト。</li><li>デフォルトのeコマース値 `_cprice` を上書きするために使用します。</li></ul> |
|`product_creative_name`|  <ul><li>配列</li><li>製品クリエイティブ名のリスト。</li><li>製品に使用されるクリエイティブ名の配列。</li></ul> |
|`product_creative_slot`|  <ul><li>配列</li><li>製品クリエイティブスロットのリスト。</li><li>製品に使用されるクリエイティブスロットの配列。</li></ul> |
|`promotion_creative_name`|  <ul><li>配列</li><li>プロモーションクリエイティブ名のリスト。</li><li>プロモーションで使用されるクリエイティブ名の配列。</li></ul> |
|`promotion_creative_slot`|  <ul><li>配列</li><li>プロモーションクリエイティブスロットのリスト。</li><li>プロモーションで使用されるクリエイティブスロット名の配列。</li></ul> |
|`promotion_id`|  <ul><li>配列</li><li>プロモーションIDのリスト。</li><li>プロモーションで使用されるプロモーションIDの配列。</li></ul> |
|`promotion_name`|  <ul><li>配列</li><li>プロモーション名。</li><li>プロモーションで使用されるプロモーション名の配列。</li></ul> |
### 製品オーディエンスパラメータ

以前にマッピングしたイベントに追加データを渡したい場合は、これらの目的地にマッピングしてください。


<blockquote>
パラメータは事前定義されたイベントでのみ使用されます。カスタムイベントでパラメータを渡す方法についての詳細は、を参照してください。
</blockquote>


事前定義されたイベントでパラメータを渡すには、以下の手順を使用します：

1. リストからイベントを選択します。
1. リストからパラメータを選択します。
カスタムパラメータを使用する場合は、それを識別する名前を入力します。
1. **追加**をクリックします。

|変数| 説明|
|---| ---|
|`ecomm_prodid`|  <ul><li>商品ID。</li><li>ユーザーが現在見ているか選択した1つ以上のID。</li></ul> |
|`ecomm_pagetype`|  <ul><li>ページタイプ。</li><li>ユーザーが現在見ているページタイプ。</li></ul> |
|`ecomm_totalvalue`|  <ul><li>総価値。</li><li>ユーザーに現在関連付けられている総価値。</li></ul> |
|`ecomm_category`|  <ul><li>カテゴリ。</li><li>ユーザーが現在見ているカテゴリ。</li></ul> |
|`travel_destid`|  <ul><li>目的地ID。</li><li>ユーザーが選択した目的地のID。</li></ul> |
|`travel_originid`|  <ul><li>出発地ID。</li><li>ユーザーの出発地のID。</li></ul> |
|`travel_startdate`|  <ul><li>開始日。</li><li>ユーザーが旅行を開始したい日付。</li></ul> |
|`travel_enddate`|  <ul><li>終了日。</li><li>ユーザーが旅行を終了したい日付。</li></ul> |
|`travel_totalvalue`|  <ul><li>総価値。</li><li>ユーザーが開始したい旅行の総価値。</li></ul> |
|`hct_bpr`|  <ul><li>ホテル基本価格。</li><li>ユーザーが予約したいホテルの基本価格。</li></ul> |
|`hct_tpr`|  <ul><li>ホテル総価格。</li><li>税金や割引を含む、ユーザーが予約したいホテルの総価格。</li></ul> |
|`hct_bid`|  <ul><li>ホテル予約ID。</li><li>ユーザーの予約のID。</li></ul> |
|`hct_cid`|  <ul><li>ホテルチェックイン日。</li><li>ユーザーの滞在のチェックイン日。</li></ul> |
|`hct_cod`|  <ul><li>ホテルチェックアウト日。</li><li>ユーザーの滞在のチェックアウト日。</li></ul> |
|`hct_los`|  <ul><li>ホテル滞在期間。</li><li>ユーザーの滞在の総期間。</li></ul> |
|`hct_pid`|  <ul><li>ホテルパートナーID。</li><li>ユーザーが予約したいホテルのパートナーID。</li></ul> |
|`hct_pagetype`|  <ul><li>ホテルページタイプ。</li><li>ユーザーが現在見ているページタイプ。</li></ul> |

### 製品オーディエンス - 小売

| 変数               | 説明             |
| ------------------ | --------------- |
| `ecomm_prodid`     | <ul><li>商品ID。</li><li>ユーザーが現在見ているか選択した1つ以上のID。</li></ul>      |
| `ecomm_pagetype`   | <ul><li>ページタイプ。</li><li>ユーザーが現在見ているページタイプ。</li><li>`home`, `searchresults`, `category`, `product`, `cart`, `purchase`, `other`のいずれか。</li></ul> |
| `ecomm_totalvalue` | <ul><li>総価値。</li><li>ユーザーに現在関連付けられている総価値。</li></ul>            |
| `ecomm_category`   | <ul><li>カテゴリ。</li><li>ユーザーが現在見ているカテゴリ。</li></ul>   |

### 製品オーディエンス - 旅行

|変数| 説明|
|---| ---|
|`travel_destid`|  <ul><li>目的地ID。</li><li>ユーザーが選択した目的地のID。</li></ul> |
|`travel_originid`|  <ul><li>出発地ID。</li><li>ユーザーの出発地のID。</li></ul> |
|`travel_pagetype`|  <ul><li>ページタイプ。</li><li>ユーザーが現在見ているページタイプ。</li><li>`home`, `searchresults`, `offerdetail`, `conversionintent`, `conversion`, `cancel`, `other`のいずれか。</li></ul> |
|`travel_startdate`|  <ul><li>開始日。</li><li>ユーザーが旅行を開始したい日付。</li><li>日付形式は`YYYY-MM-DD`。</li></ul> |
|`travel_enddate`|  <ul><li>終了日。</li><li>ユーザーが旅行を終了したい日付。</li><li>日付形式は`YYYY-MM-DD`。</li></ul> |
|`travel_totalvalue`|  <ul><li>総価値。</li><li>ユーザーが開始したい旅行の総価値。</li></ul> |

### 製品オーディエンス - ホテル

|変数| 説明|
|---| ---|
|`hct_base_price`|  <ul><li>ホテル基本価格。</li><li>ユーザーが予約したいホテルの基本価格。</li></ul> |
|`hct_total_price`|  <ul><li>ホテル総価格。</li><li>税金や割引を含む、ユーザーが予約したいホテルの総価格。</li></ul> |
| `hct_checkin_date` |  <ul><li>ホテルチェックイン日。</li><li>ユーザーの滞在のチェックイン日。</li><li>日付形式は`YYYY-MM-DD`。</li></ul> |
| `hct_checkout_date` |  <ul><li>ホテルチェックアウト日。</li><li>ユーザーの滞在のチェックアウト日。</li><li>日付形式は`YYYY-MM-DD`。</li></ul> |
|`hct_length_of_stay`|  <ul><li>ホテル滞在期間。</li><li>ユーザーの滞在の総期間。</li></ul> |
|`hct_partner_hotel_id`|  <ul><li>ホテルパートナーID。</li><li>ユーザーが予約したいホテルのパートナーID。</li></ul> |
| `hct_booking_ref` |  <ul><li>予約参照番号（難読化済み）。</li></ul> |
| `hct_pagetype` |  <ul><li>ホテルページタイプ。</li><li>ユーザーが現在見ているページタイプ。</li><li>`home`, `searchresults`, `property`, `cart`, `purchase`, `cancel`, `other`のいずれか。</li></ul> |

## ベンダー文書

* [Microsoft Bing: 販売およびその他のコンバージョンの追跡](http://help.bingads.microsoft.com/#apex/3/en/n5012/2)
* [Microsoft Bing: UETとは何か、どのように役立つか？](https://help.bingads.microsoft.com/#apex/3/en/56681/0)
* [Microsoft Bing: よくある質問](http://help.bingads.microsoft.com/apex/index/3/en-us/53056)