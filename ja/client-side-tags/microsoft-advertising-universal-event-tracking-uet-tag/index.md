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

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加する際には、以下の構成を構成します:

* **Tag ID**: あなたのMicrosoft Advertisingタグ識別子。
* **ID Sync Beacon**: 内部ユーザーIDをMicrosoftサードパーティクッキーIDに持続させます。[Microsoft UET Conversion APIコネクタ]()を使用する場合に推奨されます。
* **Ad Storage Consent**: 広告保存のデフォルト同意を構成します。`ad_storage`パラメータを**Data Mappings**セクションでマッピングすることにより、この値を動的に更新します。
* **Automatically read from Tealium Consent Cookie**: `true`に構成すると、[Tealium consent manager]()に基づいて同意が構成されます。
* **Generate Event ID**: すべてのトラッキングイベントに対して自動的にイベントIDを生成します。[Microsoft UET Conversion APIコネクタ]()を使用する際の重複排除に推奨されます。

### Conversions API

 この機能にはアクティブな[Tealium Collect tag]()が必要です。 

Microsoft UET Conversion APIをサポートするためには、**Generate Event ID**を`true`に構成します。**Generate Event ID**が有効になっている場合、このタグは各イベントに対して一意のイベントIDを生成し、それをTealium EventStreamに属性として送信し、Microsoft UET Conversion APIコネクタで使用し、`event_id`パラメータでMicrosoft Advertising UETタグに渡します。このイベントID属性は、コネクタでウェブベースのタグとサーバーサイドの統合を同期するためにマッピングされる場合があります。

タグは次の命名規則を使用してイベントIDを生成したイベント属性を送信します:

```nohl
microsoft_event_id_{EVENT_TYPE}_{TAG_UID}
```

たとえば、タグ#88からの購入イベントは次の属性と値を送信します:

```json
{
  &#34;microsoft_event_id_purchase_88&#34;: &#34;028b2ade7478...&#34;
}
```

同じタグからのページロードイベントは次の属性と値を送信します:

```json
{
  &#34;microsoft_event_id_pageload_88&#34;: &#34;084b1cda7461...&#34;
}
```
#### 重複排除

適切なイベント重複排除を確実に行うためには、Microsoft Advertising UETタグからのイベントIDをTealium Collectタグによって送信されるペイロードに含める必要があります。これを行うには、次の手順を使用します:

* **Tag Timing** ドロップダウンから **Prioritized** を選択します。
* **Bundle Flag** トグルを `On` に構成します。
* [Load Order Manager screen]()を使用して、Tealium Collectタグの前にMicrosoft Advertising UETタグを発火させます。Tealium Collectタグは最後に発火させることをお勧めします。
これらのイベントID属性の使用に関する情報については、[Microsoft UET Conversion APIコネクタ: 重複排除]()を参照してください。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## 同意モード

このタグに対して同意モードを実装するには2つのオプションがあります:

* [クライアントサイド同意管理]()を使用し、Tealium同意クッキーを自動的に読み取ります。
* [JavaScript Code extension]()を追加して、同意管理プラットフォーム（CMP）からこのタグへの同意選択とカテゴリマッピングをマップします。

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
b.consent_decision = (tealiumConsentRegister &amp;&amp; tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = CUSTOM_LOGIC ? &#39;granted&#39; : &#39;denied&#39;;
```

たとえば、次のコードはOneTrust用です。
```js
// After Load Rules - Run Always
b.consent_decision = (tealiumConsentRegister &amp;&amp; tealiumConsentRegister.currentDecision) || [];
b.microsoft_ad_storage_consent = b.consent_decision.indexOf(&#39;C0004&#39;) !== -1  ? &#39;granted&#39; : &#39;denied&#39;;
```

これらの正確な変数名を使用する場合、追加のマッピングは必要ありません。タグの最新バージョンはデフォルトでこれらの変数を使用します。特定のケースの属性に `ad_storage` パラメータをマッピングすることによってこれらの変数を上書きします。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは次のとおりです:
### 標準

|変数| 説明|
|---| ---|
|`tagid`|  &lt;ul&gt;&lt;li&gt;タグID。&lt;/li&gt;&lt;li&gt;Microsoft Advertisingから提供されるタグ識別子。&lt;/li&gt;&lt;/ul&gt; |
|`event_category`|  &lt;ul&gt;&lt;li&gt;イベントカテゴリ。&lt;/li&gt;&lt;li&gt;追跡される要素またはオブジェクトに関する情報を送信します。&lt;/li&gt;&lt;li&gt;例：`Button`。&lt;/li&gt;&lt;/ul&gt; |
|`event_action`|  &lt;ul&gt;&lt;li&gt;イベントアクション。&lt;/li&gt;&lt;li&gt;ユーザーアクションを送信します。&lt;/li&gt;&lt;li&gt;例：`click`, `mousedown`。&lt;/li&gt;&lt;/ul&gt; |
|`event_label`|  &lt;ul&gt;&lt;li&gt;イベントラベル。&lt;/li&gt;&lt;li&gt;イベント目標に関する情報ラベルまたは詳細を送信します。&lt;/li&gt;&lt;li&gt;例：`Product demo`。&lt;/li&gt;&lt;/ul&gt; |
|`event_value`|  &lt;ul&gt;&lt;li&gt;イベント値。&lt;/li&gt;&lt;li&gt;イベント目標の数値を送信します。&lt;/li&gt;&lt;/ul&gt; |
|`description`|  &lt;ul&gt;&lt;li&gt;エラー説明。&lt;/li&gt;&lt;li&gt;ユーザーが経験したエラーの説明。&lt;/li&gt;&lt;/ul&gt; |
|`fatal`|  &lt;ul&gt;&lt;li&gt;エラー致命的。&lt;/li&gt;&lt;li&gt;ユーザーが経験したエラーが致命的かどうか。&lt;/li&gt;&lt;/ul&gt; |
|`method`|  &lt;ul&gt;&lt;li&gt;方法。&lt;/li&gt;&lt;li&gt;ユーザーのアクションに関連する方法。&lt;/li&gt;&lt;/ul&gt; |
|`screen_name`|  &lt;ul&gt;&lt;li&gt;スクリーン名。&lt;/li&gt;&lt;li&gt;ユーザーが現在表示しているスクリーンの名前。&lt;/li&gt;&lt;/ul&gt; |
|`search_term`|  &lt;ul&gt;&lt;li&gt;検索用語。&lt;/li&gt;&lt;li&gt;ユーザーの検索で使用される用語。&lt;/li&gt;&lt;/ul&gt; |
|`content_type`|  &lt;ul&gt;&lt;li&gt;コンテンツタイプ。&lt;/li&gt;&lt;li&gt;ユーザーが選択したコンテンツのタイプ。&lt;/li&gt;&lt;/ul&gt; |
|`content_id`|  &lt;ul&gt;&lt;li&gt;コンテンツID。&lt;/li&gt;&lt;li&gt;ユーザーが選択したコンテンツのID。&lt;/li&gt;&lt;/ul&gt; |
|`promotion_creative_name`|  &lt;ul&gt;&lt;li&gt;プロモーションクリエイティブ名のリスト。&lt;/li&gt;&lt;li&gt;プロモーションで使用されるクリエイティブ名の配列。&lt;/li&gt;&lt;/ul&gt; |
|`promotion_creative_slot`|  &lt;ul&gt;&lt;li&gt;プロモーションクリエイティブスロットのリスト。&lt;/li&gt;&lt;li&gt;プロモーションで使用されるクリエイティブスロット名の配列。&lt;/li&gt;&lt;/ul&gt; |
|`promotion_id`|  &lt;ul&gt;&lt;li&gt;プロモーションIDのリスト。&lt;/li&gt;&lt;li&gt;プロモーションで使用されるプロモーションIDの配列。&lt;/li&gt;&lt;/ul&gt; |
|`promotion_name`|  &lt;ul&gt;&lt;li&gt;プロモーション名のリスト。&lt;/li&gt;&lt;li&gt;プロモーションで使用されるプロモーション名の配列。&lt;/li&gt;&lt;/ul&gt; |
| `enableAutoSpaTracking` | 自動SPAトラッキングを有効にする。 |
| `id_sync_beacon` | ID同期ビーコン。 |
| `customer_id` | Microsoftの顧客ID。 |
| `visitor_id` | 訪問ID。 |
| `user_id` | ユーザーID。 |
|`custom.myvar`|  &lt;ul&gt;&lt;li&gt;カスタムプロパティ/パラメータ。&lt;/li&gt;&lt;li&gt;イベント用のカスタムプロパティ。&lt;/li&gt;&lt;li&gt;すべてのイベントで送信され、特定のイベントのプロパティを構成するためにイベントパラメータを使用します。&lt;/li&gt;&lt;li&gt;`myvar`をプロパティの名前に置き換えてください。&lt;/li&gt;&lt;/ul&gt; |
| `generate_event_id` | `Boolean` | イベントIDを生成します。 |
| `event_id` | `String` | イベントID。 |

### E-Commerce

|変数| 説明|
|---| ---|
|`checkout_step`|  &lt;ul&gt;&lt;li&gt;チェックアウトステップ。&lt;/li&gt;&lt;li&gt;ユーザーが現在進行中のチェックアウトプロセスのステップ。&lt;/li&gt;&lt;/ul&gt; |
|`checkout_option`|  &lt;ul&gt;&lt;li&gt;チェックアウトオプション。&lt;/li&gt;&lt;li&gt;ユーザーが選択した現在のチェックアウトオプション。&lt;/li&gt;&lt;/ul&gt; |
|`order_id`|  &lt;ul&gt;&lt;li&gt;注文ID。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_corder` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;小計。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_csubtotal` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`order_shipping`|  &lt;ul&gt;&lt;li&gt;送料。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_cship` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`order_tax`|  &lt;ul&gt;&lt;li&gt;税金。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_ctax` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`order_currency`|  &lt;ul&gt;&lt;li&gt;通貨。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_ccurrency` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`order_coupon_code`|  &lt;ul&gt;&lt;li&gt;プロモーションコード。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_cpromo` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品IDのリスト。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_cprod` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;名前のリスト。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_cprodname` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_brand`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;ブランドのリスト。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_cbrand` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;カテゴリのリスト。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_ccat` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;数量のリスト。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_cquan` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;価格のリスト。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_cprice` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
| 製品クリエイティブ名のリスト |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品に使用されるクリエイティブ名の配列。&lt;/li&gt;&lt;/ul&gt; |
| 製品クリエイティブスロットのリスト |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品に使用されるクリエイティブスロットの配列。&lt;/li&gt;&lt;/ul&gt; |
| 製品ロケーションIDのリスト |  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品に使用されるロケーションIDの配列。&lt;/li&gt;&lt;/ul&gt; |

### イベントとエンゲージメント

特定のイベントをページ上でトリガーするためにこれらの宛先にマッピングします。

イベントをトリガーするための次のステップを使用します：

1. リストからイベントを選択します。  
事前定義されたリストから選択するか、カスタムイベントを作成します。
  * カスタムイベントの場合、それを識別する名前を入力します。

1. **トリガー**フィールドにマッピングされる変数の値を入力します。
1. より多くのイベントをマッピングするには、プラス記号 (**&#43;**) をクリックしてステップ1と2を繰り返します。
1. **適用**をクリックします。  
データレイヤーに提供された値が見つかったときにイベントがトリガーされます。

|変数| 説明|
|---| ---|
|`add_payment_info`|  &lt;ul&gt;&lt;li&gt;支払情報の追加。&lt;/li&gt;&lt;li&gt;ユーザーが取引に新しい支払情報を追加しました。&lt;/li&gt;&lt;/ul&gt; |
|`add_to_cart`|  &lt;ul&gt;&lt;li&gt;カートに追加。&lt;/li&gt;&lt;li&gt;ユーザーがショッピングカートに一つ以上のアイテムを追加しました。&lt;/li&gt;&lt;/ul&gt; |
|`add_to_wishlist`|  &lt;ul&gt;&lt;li&gt;ウィッシュリストに追加。&lt;/li&gt;&lt;li&gt;ユーザーがウィッシュリストに一つ以上のアイテムを追加しました。&lt;/li&gt;&lt;/ul&gt; |
|`begin_checkout`|  &lt;ul&gt;&lt;li&gt;チェックアウトの開始。&lt;/li&gt;&lt;li&gt;ユーザーがチェックアウトプロセスを開始しました。&lt;/li&gt;&lt;/ul&gt; |
|`checkout_progress`|  &lt;ul&gt;&lt;li&gt;チェックアウトの進行。&lt;/li&gt;&lt;li&gt;ユーザーがチェックアウトの進行でステップを交換しました。&lt;/li&gt;&lt;/ul&gt; |
|`exception`|  &lt;ul&gt;&lt;li&gt;例外。&lt;/li&gt;&lt;li&gt;ユーザーが例外に遭遇しました。&lt;/li&gt;&lt;/ul&gt; |
|`generate_lead`|  &lt;ul&gt;&lt;li&gt;リードの生成。&lt;/li&gt;&lt;li&gt;ユーザーのアクションがリードを生成しました。&lt;/li&gt;&lt;/ul&gt; |
|`login`|  &lt;ul&gt;&lt;li&gt;ログイン。&lt;/li&gt;&lt;li&gt;ユーザーがログインしました。&lt;/li&gt;&lt;/ul&gt; |
|`page_view`|  &lt;ul&gt;&lt;li&gt;ページビュー。&lt;/li&gt;&lt;li&gt;ユーザーがページを閲覧しました。&lt;/li&gt;&lt;/ul&gt; |
|`purchase`|  &lt;ul&gt;&lt;li&gt;購入。&lt;/li&gt;&lt;li&gt;ユーザーが一つ以上の製品の購入を完了しました。&lt;/li&gt;&lt;/ul&gt; |
|`refund`|  &lt;ul&gt;&lt;li&gt;払い戻し。&lt;/li&gt;&lt;li&gt;ユーザーが一つ以上の製品に対して払い戻しを要求しました。&lt;/li&gt;&lt;/ul&gt; |
|`remove_from_cart`|  &lt;ul&gt;&lt;li&gt;カートから削除。&lt;/li&gt;&lt;li&gt;ユーザーがショッピングカートから一つ以上のアイテムを削除しました。&lt;/li&gt;&lt;/ul&gt; |
|`screen_view`|  &lt;ul&gt;&lt;li&gt;スクリーンビュー。&lt;/li&gt;&lt;li&gt;ユーザーがスクリーンを閲覧しました。&lt;/li&gt;&lt;/ul&gt; |
|`search`|  &lt;ul&gt;&lt;li&gt;検索。&lt;/li&gt;&lt;li&gt;ユーザーが検索しました。&lt;/li&gt;&lt;/ul&gt; |
|`select_content`|  &lt;ul&gt;&lt;li&gt;コンテンツの選択。&lt;/li&gt;&lt;li&gt;ユーザーが一つ以上のコンテンツアイテムを選択しました。&lt;/li&gt;&lt;/ul&gt; |
|`set_checkout_option`|  &lt;ul&gt;&lt;li&gt;チェックアウトオプションの構成。&lt;/li&gt;&lt;li&gt;ユーザーが現在のチェックアウトステップのためのチェックアウトオプションを選択しました。&lt;/li&gt;&lt;/ul&gt; |
|`share`|  &lt;ul&gt;&lt;li&gt;共有&lt;/li&gt;&lt;li&gt;ユーザーがコンテンツを共有しました。&lt;/li&gt;&lt;/ul&gt; |
|`sign_up`|  &lt;ul&gt;&lt;li&gt;サインアップ。&lt;/li&gt;&lt;li&gt;ユーザーがサインアップしました。&lt;/li&gt;&lt;/ul&gt; |
|`timing_complete`|  &lt;ul&gt;&lt;li&gt;タイミング完了。&lt;/li&gt;&lt;li&gt;ユーザーのページロードのタイミング情報。&lt;/li&gt;&lt;/ul&gt; |
|`view_item`|  &lt;ul&gt;&lt;li&gt;アイテム表示。&lt;/li&gt;&lt;li&gt;ユーザーが単一のアイテム、通常は詳細ページを閲覧しました。&lt;/li&gt;&lt;/ul&gt; |
|`view_item_list`|  &lt;ul&gt;&lt;li&gt;アイテムリスト表示。&lt;/li&gt;&lt;li&gt;ユーザーが一つ以上のアイテムが含まれるリストページを閲覧しました。&lt;/li&gt;&lt;/ul&gt; |
|`view_promotion`|  &lt;ul&gt;&lt;li&gt;プロモーション表示。&lt;/li&gt;&lt;li&gt;ユーザーがプロモーションをクリックしました。&lt;/li&gt;&lt;/ul&gt; |
|`view_search_results`|  &lt;ul&gt;&lt;li&gt;検索結果表示。&lt;/li&gt;&lt;li&gt;ユーザーが検索の結果を閲覧しました。&lt;/li&gt;&lt;/ul&gt; |
| `update_consent` | &lt;ul&gt;&lt;li&gt;同意の更新。&lt;/li&gt;&lt;/ul&gt;  |
|`custom`|  &lt;ul&gt;&lt;li&gt;カスタムイベント。&lt;/li&gt;&lt;li&gt;ユーザーがカスタムイベントに関連するアクションを開始しました。&lt;/li&gt;&lt;/ul&gt; |
### 製品オーディエンスイベント

特定のイベントをページでトリガーするためにこれらのデスティネーションにマッピングします。

イベントをトリガーするには、以下の手順を使用します：

1. リストからイベントを選択します。  
事前定義されたリストから選択するか、カスタムイベントを作成します。
  * カスタムイベントの場合、それを識別する名前を入力します。

1. **トリガー** フィールドに、マッピングされる変数の値を入力します。
1. より多くのイベントをマッピングするには、プラス記号（**&#43;**）をクリックして、手順1と2を繰り返します。
1. **適用**をクリックします。  
提供された値がデータレイヤーで見つかったときにイベントがトリガーされます。

|変数| 説明|
|---| ---|
|`retail`|  &lt;ul&gt;&lt;li&gt;小売。&lt;/li&gt;&lt;li&gt;小売ベースのマーケティングのためのデータを送信します。&lt;/li&gt;&lt;/ul&gt; |
|`travel`|  &lt;ul&gt;&lt;li&gt;旅行。&lt;/li&gt;&lt;li&gt;旅行ベースのマーケティングのためのデータを送信します。&lt;/li&gt;&lt;/ul&gt; |
|`hotel`|  &lt;ul&gt;&lt;li&gt;ホテル。&lt;/li&gt;&lt;li&gt;ホテルベースのマーケティングのためのデータを送信します。&lt;/li&gt;&lt;/ul&gt; |

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

パラメータは事前定義されたイベントでのみ使用されます。カスタムイベントでパラメータを渡す方法の詳細については、を参照してください。

事前定義されたイベントにパラメータを渡すための以下の手順を使用します：

1. リストからイベントを選択します。
1. リストからパラメータを選択します。  
カスタムパラメータを使用する場合は、それを識別する名前を入力します。
1. **追加**をクリックします。

|変数| 説明|
|---| ---|
|`event_category`|  &lt;ul&gt;&lt;li&gt;イベントカテゴリ。&lt;/li&gt;&lt;li&gt;現在のイベントのカテゴリ。&lt;/li&gt;&lt;li&gt;クリックされたボタンなど、要素やオブジェクトに関する情報を送信します。&lt;/li&gt;&lt;/ul&gt; |
|`event_action`|  &lt;ul&gt;&lt;li&gt;イベントアクション。&lt;/li&gt;&lt;li&gt;現在のイベントのアクション名。&lt;/li&gt;&lt;li&gt;クリックやマウスダウンなどのユーザーアクションを送信します。&lt;/li&gt;&lt;/ul&gt; |
|`event_label`|  &lt;ul&gt;&lt;li&gt;イベントラベル。&lt;/li&gt;&lt;li&gt;現在のイベントのラベル。&lt;/li&gt;&lt;li&gt;製品デモなど、製品目標に関する情報ラベルや詳細を送信します。&lt;/li&gt;&lt;/ul&gt; |
|`event_value`|  &lt;ul&gt;&lt;li&gt;イベント値。&lt;/li&gt;&lt;li&gt;現在のイベントの目標値を数値で送信します。&lt;/li&gt;&lt;/ul&gt; |
|`custom`|  &lt;ul&gt;&lt;li&gt;カスタムプロパティ/パラメータ。&lt;/li&gt;&lt;li&gt;現在のイベントに関連するカスタムプロパティ。&lt;/li&gt;&lt;/ul&gt; |
|`description`|  &lt;ul&gt;&lt;li&gt;エラー説明。&lt;/li&gt;&lt;li&gt;ユーザーが経験したエラーの説明。&lt;/li&gt;&lt;/ul&gt; |
|`fatal`|  &lt;ul&gt;&lt;li&gt;エラー致命的。&lt;/li&gt;&lt;li&gt;ユーザーが経験したエラーが致命的かどうか。&lt;/li&gt;&lt;/ul&gt; |
|`method`|  &lt;ul&gt;&lt;li&gt;方法。&lt;/li&gt;&lt;li&gt;ユーザーのアクションに関連する方法。&lt;/li&gt;&lt;/ul&gt; |
|`screen_name`|  &lt;ul&gt;&lt;li&gt;スクリーン名。&lt;/li&gt;&lt;li&gt;ユーザーが現在閲覧しているスクリーンの名前。&lt;/li&gt;&lt;/ul&gt; |
|`search_term`|  &lt;ul&gt;&lt;li&gt;検索用語。&lt;/li&gt;&lt;li&gt;ユーザーの検索で使用された用語。&lt;/li&gt;&lt;/ul&gt; |
|`content_type`|  &lt;ul&gt;&lt;li&gt;コンテンツタイプ。&lt;/li&gt;&lt;li&gt;ユーザーが選択したコンテンツのタイプ。&lt;/li&gt;&lt;/ul&gt; |
|`content_id`|  &lt;ul&gt;&lt;li&gt;コンテンツID。&lt;/li&gt;&lt;li&gt;ユーザーが選択したコンテンツのID。&lt;/li&gt;&lt;/ul&gt; |
|`checkout_step`|  &lt;ul&gt;&lt;li&gt;チェックアウトステップ。&lt;/li&gt;&lt;li&gt;ユーザーが現在いるチェックアウトプロセスのステップ。&lt;/li&gt;&lt;/ul&gt; |
|`checkout_option`|  &lt;ul&gt;&lt;li&gt;チェックアウトオプション。&lt;/li&gt;&lt;li&gt;ユーザーが選択した現在のチェックアウトオプション。&lt;/li&gt;&lt;/ul&gt; |
|`order_id`|  &lt;ul&gt;&lt;li&gt;注文ID。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_corder` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`order_total`|  &lt;ul&gt;&lt;li&gt;注文合計。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_ctotal` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;小計。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_csubtotal` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`order_shipping`|  &lt;ul&gt;&lt;li&gt;送料。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_cship` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`order_tax`|  &lt;ul&gt;&lt;li&gt;税額。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_ctax` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`order_currency`|  &lt;ul&gt;&lt;li&gt;通貨。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_ccurrency` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`order_coupon_code`|  &lt;ul&gt;&lt;li&gt;プロモーションコード。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_cpromo` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;製品IDのリスト。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_cprod` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;名前のリスト。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_cprodname` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_brand`|  &lt;ul&gt;&lt;li&gt;ブランドのリスト。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_cbrand` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;カテゴリのリスト。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_ccat` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;数量のリスト。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_cquan` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;価格のリスト。&lt;/li&gt;&lt;li&gt;デフォルトのeコマース値 `_cprice` を上書きするために使用します。&lt;/li&gt;&lt;/ul&gt; |
|`product_creative_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品クリエイティブ名のリスト。&lt;/li&gt;&lt;li&gt;製品に使用されるクリエイティブ名の配列。&lt;/li&gt;&lt;/ul&gt; |
|`product_creative_slot`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;製品クリエイティブスロットのリスト。&lt;/li&gt;&lt;li&gt;製品に使用されるクリエイティブスロットの配列。&lt;/li&gt;&lt;/ul&gt; |
|`promotion_creative_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;プロモーションクリエイティブ名のリスト。&lt;/li&gt;&lt;li&gt;プロモーションで使用されるクリエイティブ名の配列。&lt;/li&gt;&lt;/ul&gt; |
|`promotion_creative_slot`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;プロモーションクリエイティブスロットのリスト。&lt;/li&gt;&lt;li&gt;プロモーションで使用されるクリエイティブスロット名の配列。&lt;/li&gt;&lt;/ul&gt; |
|`promotion_id`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;プロモーションIDのリスト。&lt;/li&gt;&lt;li&gt;プロモーションで使用されるプロモーションIDの配列。&lt;/li&gt;&lt;/ul&gt; |
|`promotion_name`|  &lt;ul&gt;&lt;li&gt;配列&lt;/li&gt;&lt;li&gt;プロモーション名。&lt;/li&gt;&lt;li&gt;プロモーションで使用されるプロモーション名の配列。&lt;/li&gt;&lt;/ul&gt; |
### 製品オーディエンスパラメータ

以前にマッピングしたイベントに追加データを渡したい場合は、これらの目的地にマッピングしてください。

パラメータは事前定義されたイベントでのみ使用されます。カスタムイベントでパラメータを渡す方法についての詳細は、を参照してください。

事前定義されたイベントでパラメータを渡すには、以下の手順を使用します：

1. リストからイベントを選択します。
1. リストからパラメータを選択します。
カスタムパラメータを使用する場合は、それを識別する名前を入力します。
1. **追加**をクリックします。

|変数| 説明|
|---| ---|
|`ecomm_prodid`|  &lt;ul&gt;&lt;li&gt;商品ID。&lt;/li&gt;&lt;li&gt;ユーザーが現在見ているか選択した1つ以上のID。&lt;/li&gt;&lt;/ul&gt; |
|`ecomm_pagetype`|  &lt;ul&gt;&lt;li&gt;ページタイプ。&lt;/li&gt;&lt;li&gt;ユーザーが現在見ているページタイプ。&lt;/li&gt;&lt;/ul&gt; |
|`ecomm_totalvalue`|  &lt;ul&gt;&lt;li&gt;総価値。&lt;/li&gt;&lt;li&gt;ユーザーに現在関連付けられている総価値。&lt;/li&gt;&lt;/ul&gt; |
|`ecomm_category`|  &lt;ul&gt;&lt;li&gt;カテゴリ。&lt;/li&gt;&lt;li&gt;ユーザーが現在見ているカテゴリ。&lt;/li&gt;&lt;/ul&gt; |
|`travel_destid`|  &lt;ul&gt;&lt;li&gt;目的地ID。&lt;/li&gt;&lt;li&gt;ユーザーが選択した目的地のID。&lt;/li&gt;&lt;/ul&gt; |
|`travel_originid`|  &lt;ul&gt;&lt;li&gt;出発地ID。&lt;/li&gt;&lt;li&gt;ユーザーの出発地のID。&lt;/li&gt;&lt;/ul&gt; |
|`travel_startdate`|  &lt;ul&gt;&lt;li&gt;開始日。&lt;/li&gt;&lt;li&gt;ユーザーが旅行を開始したい日付。&lt;/li&gt;&lt;/ul&gt; |
|`travel_enddate`|  &lt;ul&gt;&lt;li&gt;終了日。&lt;/li&gt;&lt;li&gt;ユーザーが旅行を終了したい日付。&lt;/li&gt;&lt;/ul&gt; |
|`travel_totalvalue`|  &lt;ul&gt;&lt;li&gt;総価値。&lt;/li&gt;&lt;li&gt;ユーザーが開始したい旅行の総価値。&lt;/li&gt;&lt;/ul&gt; |
|`hct_bpr`|  &lt;ul&gt;&lt;li&gt;ホテル基本価格。&lt;/li&gt;&lt;li&gt;ユーザーが予約したいホテルの基本価格。&lt;/li&gt;&lt;/ul&gt; |
|`hct_tpr`|  &lt;ul&gt;&lt;li&gt;ホテル総価格。&lt;/li&gt;&lt;li&gt;税金や割引を含む、ユーザーが予約したいホテルの総価格。&lt;/li&gt;&lt;/ul&gt; |
|`hct_bid`|  &lt;ul&gt;&lt;li&gt;ホテル予約ID。&lt;/li&gt;&lt;li&gt;ユーザーの予約のID。&lt;/li&gt;&lt;/ul&gt; |
|`hct_cid`|  &lt;ul&gt;&lt;li&gt;ホテルチェックイン日。&lt;/li&gt;&lt;li&gt;ユーザーの滞在のチェックイン日。&lt;/li&gt;&lt;/ul&gt; |
|`hct_cod`|  &lt;ul&gt;&lt;li&gt;ホテルチェックアウト日。&lt;/li&gt;&lt;li&gt;ユーザーの滞在のチェックアウト日。&lt;/li&gt;&lt;/ul&gt; |
|`hct_los`|  &lt;ul&gt;&lt;li&gt;ホテル滞在期間。&lt;/li&gt;&lt;li&gt;ユーザーの滞在の総期間。&lt;/li&gt;&lt;/ul&gt; |
|`hct_pid`|  &lt;ul&gt;&lt;li&gt;ホテルパートナーID。&lt;/li&gt;&lt;li&gt;ユーザーが予約したいホテルのパートナーID。&lt;/li&gt;&lt;/ul&gt; |
|`hct_pagetype`|  &lt;ul&gt;&lt;li&gt;ホテルページタイプ。&lt;/li&gt;&lt;li&gt;ユーザーが現在見ているページタイプ。&lt;/li&gt;&lt;/ul&gt; |

### 製品オーディエンス - 小売

| 変数               | 説明             |
| ------------------ | --------------- |
| `ecomm_prodid`     | &lt;ul&gt;&lt;li&gt;商品ID。&lt;/li&gt;&lt;li&gt;ユーザーが現在見ているか選択した1つ以上のID。&lt;/li&gt;&lt;/ul&gt;      |
| `ecomm_pagetype`   | &lt;ul&gt;&lt;li&gt;ページタイプ。&lt;/li&gt;&lt;li&gt;ユーザーが現在見ているページタイプ。&lt;/li&gt;&lt;li&gt;`home`, `searchresults`, `category`, `product`, `cart`, `purchase`, `other`のいずれか。&lt;/li&gt;&lt;/ul&gt; |
| `ecomm_totalvalue` | &lt;ul&gt;&lt;li&gt;総価値。&lt;/li&gt;&lt;li&gt;ユーザーに現在関連付けられている総価値。&lt;/li&gt;&lt;/ul&gt;            |
| `ecomm_category`   | &lt;ul&gt;&lt;li&gt;カテゴリ。&lt;/li&gt;&lt;li&gt;ユーザーが現在見ているカテゴリ。&lt;/li&gt;&lt;/ul&gt;   |

### 製品オーディエンス - 旅行

|変数| 説明|
|---| ---|
|`travel_destid`|  &lt;ul&gt;&lt;li&gt;目的地ID。&lt;/li&gt;&lt;li&gt;ユーザーが選択した目的地のID。&lt;/li&gt;&lt;/ul&gt; |
|`travel_originid`|  &lt;ul&gt;&lt;li&gt;出発地ID。&lt;/li&gt;&lt;li&gt;ユーザーの出発地のID。&lt;/li&gt;&lt;/ul&gt; |
|`travel_pagetype`|  &lt;ul&gt;&lt;li&gt;ページタイプ。&lt;/li&gt;&lt;li&gt;ユーザーが現在見ているページタイプ。&lt;/li&gt;&lt;li&gt;`home`, `searchresults`, `offerdetail`, `conversionintent`, `conversion`, `cancel`, `other`のいずれか。&lt;/li&gt;&lt;/ul&gt; |
|`travel_startdate`|  &lt;ul&gt;&lt;li&gt;開始日。&lt;/li&gt;&lt;li&gt;ユーザーが旅行を開始したい日付。&lt;/li&gt;&lt;li&gt;日付形式は`YYYY-MM-DD`。&lt;/li&gt;&lt;/ul&gt; |
|`travel_enddate`|  &lt;ul&gt;&lt;li&gt;終了日。&lt;/li&gt;&lt;li&gt;ユーザーが旅行を終了したい日付。&lt;/li&gt;&lt;li&gt;日付形式は`YYYY-MM-DD`。&lt;/li&gt;&lt;/ul&gt; |
|`travel_totalvalue`|  &lt;ul&gt;&lt;li&gt;総価値。&lt;/li&gt;&lt;li&gt;ユーザーが開始したい旅行の総価値。&lt;/li&gt;&lt;/ul&gt; |

### 製品オーディエンス - ホテル

|変数| 説明|
|---| ---|
|`hct_base_price`|  &lt;ul&gt;&lt;li&gt;ホテル基本価格。&lt;/li&gt;&lt;li&gt;ユーザーが予約したいホテルの基本価格。&lt;/li&gt;&lt;/ul&gt; |
|`hct_total_price`|  &lt;ul&gt;&lt;li&gt;ホテル総価格。&lt;/li&gt;&lt;li&gt;税金や割引を含む、ユーザーが予約したいホテルの総価格。&lt;/li&gt;&lt;/ul&gt; |
| `hct_checkin_date` |  &lt;ul&gt;&lt;li&gt;ホテルチェックイン日。&lt;/li&gt;&lt;li&gt;ユーザーの滞在のチェックイン日。&lt;/li&gt;&lt;li&gt;日付形式は`YYYY-MM-DD`。&lt;/li&gt;&lt;/ul&gt; |
| `hct_checkout_date` |  &lt;ul&gt;&lt;li&gt;ホテルチェックアウト日。&lt;/li&gt;&lt;li&gt;ユーザーの滞在のチェックアウト日。&lt;/li&gt;&lt;li&gt;日付形式は`YYYY-MM-DD`。&lt;/li&gt;&lt;/ul&gt; |
|`hct_length_of_stay`|  &lt;ul&gt;&lt;li&gt;ホテル滞在期間。&lt;/li&gt;&lt;li&gt;ユーザーの滞在の総期間。&lt;/li&gt;&lt;/ul&gt; |
|`hct_partner_hotel_id`|  &lt;ul&gt;&lt;li&gt;ホテルパートナーID。&lt;/li&gt;&lt;li&gt;ユーザーが予約したいホテルのパートナーID。&lt;/li&gt;&lt;/ul&gt; |
| `hct_booking_ref` |  &lt;ul&gt;&lt;li&gt;予約参照番号（難読化済み）。&lt;/li&gt;&lt;/ul&gt; |
| `hct_pagetype` |  &lt;ul&gt;&lt;li&gt;ホテルページタイプ。&lt;/li&gt;&lt;li&gt;ユーザーが現在見ているページタイプ。&lt;/li&gt;&lt;li&gt;`home`, `searchresults`, `property`, `cart`, `purchase`, `cancel`, `other`のいずれか。&lt;/li&gt;&lt;/ul&gt; |

## ベンダー文書

* [Microsoft Bing: 販売およびその他のコンバージョンの追跡](http://help.bingads.microsoft.com/#apex/3/en/n5012/2)
* [Microsoft Bing: UETとは何か、どのように役立つか？](https://help.bingads.microsoft.com/#apex/3/en/56681/0)
* [Microsoft Bing: よくある質問](http://help.bingads.microsoft.com/apex/index/3/en-us/53056)