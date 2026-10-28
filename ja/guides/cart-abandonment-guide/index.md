---
title: カート放棄ガイド
description: このガイドでは、商品をショッピングカートに追加したものの、購入を完了しなかった訪問をターゲティングする方法を説明します。
url: https://docs.tealium.com/ja/guides/cart-abandonment-guide/
---
このガイドでは、Tealium iQ Tag Management（任意）、Tealium AudienceStream CDP、およびメールマーケティングコネクタを組み合わせて、基本的なカート放棄を追跡する方法を説明します。

![](https://docs.tealium.com/images/guides/cart-abandonment-flow-diagram.png)

このガイドのソリューションでは、以下の手順を説明します。

* [ステップ1：イベントを追跡する](#step-1-track-events)
* [ステップ2：訪問属性を定義する](#step-2-define-visitor-attributes)
* [ステップ3：オーディエンスを定義する](#step-3-define-an-audience)
* [ステップ4：コネクタを構成する](#step-4-configure-a-connector)

## 必須のイベントと属性

以下のイベントを追跡する必要があります。
* `cart_add`
* `purchase`

一般に、以下のイベント属性はカート放棄アクティビティの追跡に役立ちます。実際の属性名は異なる場合があります。

| 属性名                  | 値の例 |
|----------------------- |---------------|
|`cart_product_id`       | `["PROD123", "PROD456"]`|
|`cart_product_price`    | `["12.00", "25.99"]`|
|`cart_product_quantity` | `["2", "2"]`|
|`cart_product_sku`      | `["PR-RED-123", "PR-BLK-456"]` |
|`product_category`      | `["Shirts"]`|
|`product_id`            | `["PROD678"]`|
|`product_image_url`     | `["//example.com/path/image.gif"]`|
|`product_name`          | `["Product Three"]`|
|`product_price`         | `["18.00"]`|
|`product_quantity`      | `["2"]`|
|`product_sku`           | `["PR-BLU-678"]`|
|`product_subcategory`   | `["T-Shirts"]`|
|`tealium_event`         | `"cart_add"`|

eコマースイベントの追跡について詳しくは、[retail](https://docs.tealium.com/retail/)を参照してください。


## 必須の訪問属性

| 属性名 | タイプ   | スコープ   | 説明        |
|----------------|--------|---------|--------------------|
| カートに追加 | ブール値 | 訪問 | 前回の訪問で商品がショッピングカートに追加されたことを示します。|
| 購入済み | ブール値 | 訪問 | 前回の訪問中に購入が行われたことを示します。 |
| カート放棄者 | バッジ | 訪問 | カート放棄の条件を満たしたことを示します。 |

## ステップ1：イベントを追跡する

このステップでは、Tealium iQイベントを使用し、訪問が商品をカートに追加したときにイベント情報と商品情報を送信します。

すでに`cart_add`イベントを収集している場合は、このステップをスキップしてください。

### 「カートに追加」イベントを追跡する

まず、訪問がカートに商品を追加したタイミングを把握する必要があります。ユーザーがカートに商品を追加したときに追跡するイベントリスナーを作成します。

このユースケースでは、`tealium_event`を`cart_add`に構成します。

1. **Tag Management > Events**に移動し、**+New Event**をクリックします。
1. **Event Types**画面で、イベントタイプとして**Click**を選択し、**Next**をクリックします。
1. **Configuration**画面で、クリックイベントに以下の値を構成します。
   * **Name**：カートに追加
   * **Scope**：DOM Ready
   * **Tracking Event**：Link
   * **Event Triggers**：Mousedown
   * **Element Selector**：Webサイトに最も適した、ハッシュ`#`で始まるセレクター。たとえば、Webサイトの**カートに追加**ボタンに`#add-to-cart`というセレクターが構成されている場合があります。
   * イベントトリガー変数：Tealium EventをTextに構成し、`cart_add`と入力します。
1. **Next**をクリックします。

![](https://docs.tealium.com/images/guides/event_add_cart_to_pages.png)


<blockquote>
本番環境にパブリッシュする前に、イベント構成をテストしてください。
</blockquote>


## ステップ2：訪問属性を定義する

次に、以下の2つのブール属性を作成する必要があります。

* **カートに追加（ブール値）**：訪問がカートに商品を追加したかどうかを判定します。
* **購入済み（ブール値）**：訪問が前回の訪問中に購入を完了したかどうかを判定します。

### 「カートに追加」ブール値

`cart_add`イベントが発生したタイミングを追跡するために、訪問ブール属性を作成します。

1. **Transform > Visitor / Visit Attributes**に移動し、**+Add Attribute**をクリックします。
1. **Add Attribute**画面で、**Visitor**、**Continue**の順にクリックします。
1. **Boolean**を選択し、**Continue**をクリックします。
1. **Properties**セクションで、タイトルとして`Added to Cart `を入力します。
1. **Add Enrichment**をクリックし、**Added to Cart**ブール値を`false`、スコープを**NEW VISIT**に構成します。
1. **Add Enrichment**をクリックし、**Added to Cart**ブール値を`true`、スコープを**ANY EVENT**に構成します。
1. ルールがまだ存在しない場合は、以下のルールを作成します。
    * **Title**：Event cart_add
    * **+Attribute Condition**をクリックします。
    * `tealium_event`が`cart_add`と**equal (ignore case)**になるように選択します。
1. **Save**をクリックします。

![](https://docs.tealium.com/images/guides/boolean_added_to_cart.png)

### 「購入済み」ブール値

`purchase`イベントが発生したタイミングを追跡するために、訪問ブール属性を作成します。

1. **Transform > Visitor / Visit Attributes**に移動し、**+Add Attribute**をクリックします。
1. **Add Attribute**画面で、**Visitor**、**Continue**の順にクリックします。
1. **Boolean**を選択し、**Continue**をクリックします。
1. **Properties**セクションで、タイトルとして`Did Purchase`を入力します。
1. **Add Enrichment**をクリックし、**Purchase**ブール値を`false`、スコープを**NEW VISIT**に構成します。
1. **Add Enrichment**をクリックし、**Purchase**ブール値を`true`、スコープを**Any Event**に構成します。
1. ルールがまだ存在しない場合は、以下のルールを作成します。
    * **Title**：Purchase event
    * **+Attribute Condition**をクリックします。
    * `tealium_event`が`purchase`を**contains (ignore case)**するように選択します。
    ![](https://docs.tealium.com/images/guides/boolean_purchase.png)
1. **Save**をクリックします。
1. **Finish**をクリックします。

### カート放棄者バッジとルール

オーディエンスを作成する前に、作成したブール属性を使用して、カートを放棄した訪問に割り当てるバッジを作成する必要があります。

1. **Transform > Visitor / Visit Attributes**に移動し、**+Add Attribute**をクリックします。
1. **Visitor**を選択し、次に**Badge**を選択します。
1. **Properties**セクションで、タイトルとして`Cart Abandoner `を入力します。
1. **Add Enrichment**、**Assign a badge**の順にクリックします。
1. **Assign this badge to visitor**で、ドロップダウンリストから**VISIT ENDED**を選択します。
1. **Create Rule**をクリックし、以下の属性条件を構成します。
    * **Added to Cart**ブール値：`true`である
    * **Purchase**ブール値：`false`である
1. **Add Enrichment**、**Remove badge**の順にクリックします。
1. **Remove this badge from Visitor**で**ANY EVENT**を選択します。
1. **Create Rule**をクリックし、まだ存在しない場合は以下のルールを作成します。
    * `tealium_event`を**contains (ignore case)**、`purchase`に構成します。
1. **Finish**をクリックします。

![](https://docs.tealium.com/images/guides/badge_cart_abandoner.png)

## ステップ3：オーディエンスを定義する

作成したバッジを使用して、オーディエンスを簡単に作成できるようになりました。

1. **Activate > Audiences**に移動し、**+New Audience**をクリックします。
1. 以下のオーディエンスを追加します。
    * **Name**：カート放棄者
    * 最初のドロップダウンリストから**Cart Abandoner**バッジを選択し、2番目のドロップダウンリストから**is assigned**を選択します。
1. **Done**をクリックします。
1. プロファイルを保存してパブリッシュします。

![](https://docs.tealium.com/images/guides/audience_cart_abandoners.png)

## ステップ4：コネクタを構成する

属性、バッジ、オーディエンスの構成が完了したら、この新しいオーディエンスをメールマーケティングツールに接続し、訪問をリターゲティングしてコンバージョンにつなげることができます。

カート放棄に使用される一般的なコネクタとアクションには、以下があります。

* [Adobe Campaign Classic](https://docs.tealium.com/adobe-campaign-classic-connector/)
* [Iterable](https://docs.tealium.com/iterable-connector/)：**Subscribe User to a List**、**Upsert User**アクション
* [Marketo](https://docs.tealium.com/marketo-connector/)：**Add Lead to List**アクション
* [SendGrid](https://docs.tealium.com/sendgrid-connector/)：**Upsert Contact**アクション
### 遅延アクション

多くの場合、ユーザーがカートを放棄した直後にメールを送信できますが、メールの送信を遅らせることで、コンバージョンの可能性が高まる場合があります。遅延アクションを使用して、リターゲティングキャンペーンのコネクタを実行するタイミングを制御します。

詳細については、[about-delayed-actions](https://docs.tealium.com/about-delayed-actions/)を参照してください。

## 追加のトラッキング

### カート金額

カート放棄ユーザーをより具体的にセグメント化できるように、放棄されたカートの金額をトラッキングすることを検討してください。これらのセグメントでは、`cart_total_value`属性を使用して、カート内の全商品の合計金額を判定します。

* **カート放棄ユーザー - 高額**  
商品をカートに追加しており、カートの合計金額がカスタムの高額しきい値を超えていて、購入していないユーザー。
* **カート放棄ユーザー - 中額**  
商品をカートに追加しており、カートの合計金額がカスタムの高額しきい値と低額しきい値の間で、購入していないユーザー。
* **カート放棄ユーザー - 低額**  
商品をカートに追加しており、カートの合計金額がカスタムの低額しきい値未満で、購入していないユーザー。

### 補足属性

追加の顧客アクティビティをトラッキングすることで、顧客行動への理解を深めます。

次の表は、カート放棄キャンペーンでトラッキングする追加属性の一覧です。

| 属性名 | 属性タイプ | スコープ | カテゴリ | 注記 |
|---|---|---|---|---|
| カート放棄ユーザー | ブール値／バッジ | 訪問 | 購入行動 | このセッション中に商品がカートに追加され、購入されなかった場合に、セッション終了時に適用されます。 |
| 到達したファネルの最終段階 | バッジ | 訪問 | 購入行動 | 次のユーザーフローで使用できます：獲得 > 閲覧 > 商品詳細ページ（PDP）の表示 > カートへの追加 > カートの表示 > 購入。 |
| このセッションでのカート表示 | ブール値 | 訪問 | 購入行動 | ユーザーがカートを表示したか、商品をカートに追加しただけかを示します。 |
| カート合計金額 | 数値 | 訪問 | 購入行動 | 分析、機会規模の評価、および将来的な有料メディアへの展開に役立ちます。 |
| 前回のカート放棄からの日数 | 数値 | 訪問 | 購入行動 | カート放棄ユーザーとしての適格性を判断するための単純な日数カウントです。分析にも使用できます。 |
| カート放棄回数 | 数値 | 訪問 | ライフタイム行動 | カート放棄イベントごとに1ずつ増加する数値です。 |
| 平均注文金額 | 数値 | 訪問 | ライフタイム行動 | 全般的な行動の把握と、将来的なユースケースの拡張に使用できます。 |
| 平均商品金額 | 数値 | 訪問 | ライフタイム行動 | 全般的な行動の把握と、将来的なユースケースの拡張に使用できます。 |
| お気に入りのカテゴリ | 集計 | 訪問 | ライフタイム行動 | 全般的な行動の把握と、将来的なユースケースの拡張に使用できます。 |

より堅牢なリターゲティングを行うには、この基本的なカート放棄構成をモバイルおよびオフラインの販売時点情報管理（POS）システムと組み合わせて、商品を閲覧および購入する可能性のあるすべての行動を監視します。オフラインPOSシステムのデータを含めることで、店舗で購入したユーザーをオンラインキャンペーンから自動的に除外できるため、リターゲティングキャンペーンの効率が向上します。

## 次のステップ

カート放棄ユーザーの属性を定義したため、Context APIなどのソリューションを使用したパーソナライゼーションにも利用できます。

詳細については、[about-context-api](https://docs.tealium.com/about-context-api/)を参照してください。