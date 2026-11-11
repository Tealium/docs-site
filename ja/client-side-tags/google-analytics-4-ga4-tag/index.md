---
title: Google Analytics 4（GA4）タグ構成ガイド
description: この記事では、Tag ManagementアカウントでGoogle Analytics 4タグ（GA4）を構成する方法と、実装時に注意すべき事項について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-analytics-4-ga4-tag/
---
## 仕組み

Google Analytics 4（GA4）は、Google Analyticsの新しいバージョンです。GA4とGoogle Universal Analyticsの違いの1つは、GA4では異なるレポート方式が使用されることです。現在サイトでGoogle Universal Analyticsを使用している場合は、GA4へ完全に切り替える前に、Google Universal AnalyticsとGA4を数か月間並行して使用することをお勧めします。この方法により、GA4のレポートに慣れるまでの間も、Google Universal Analyticsで履歴データを継続して収集できます。

Google Universal Analyticsは、2023年7月1日（360アカウントでは2023年10月1日）にデータ処理を停止したことに注意してください。

Google Universal Analyticsには、イベントトラッキング、ページビュー、タイミングイベント、ソーシャルシェアなど、複数のヒットタイプがあります。GA4は完全にイベントベースであり、イベントヒットのみが存在します。GA4には、Google Universal Analyticsで使用されていたイベントカテゴリ、アクション、ラベル、値はありません。代わりに、GA4イベントとともに送信されるデータには、イベント名と、イベントのコンテキストデータを含むカスタマイズ可能なイベントパラメータが含まれます。

Google Universal AnalyticsからGA4への移行について詳しくは、[Universal AnalyticsからGoogle Analytics 4への移行](https://support.tealiumiq.com/en/support/solutions/articles/36000363506-migrating-from-universal-analytics-gtag-jsanalytics-js-to-google-analytics-4-ga4-)を参照してください。

## タグに関するヒント

* マッピングを使用して、以下を行います。
  * Eコマース拡張機能の値を動的に上書きする
  * イベントトリガーを構成する
* 以下のEコマース拡張機能の値をサポートします。
  * 注文ID
  * 注文合計
  * 配送料
  * 税額
  * ストア
  * プロモーションコード
  * 顧客ID
  * 商品IDのリスト
  * 商品名のリスト
  * ブランドのリスト
  * カテゴリのリスト
  * 価格のリスト
  * 数量のリスト
  * 割引のリスト
  * カスタムの商品スコープディメンション

## Google Analytics 4タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳しくは、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を構成します。

* **測定ID**
  * データの送信先となるGoogle Analyticsプロパティの測定IDです。測定IDは「G-」で始まります。例：`G-12345678M`
  * 複数のGA4プロパティにデータを送信するには、測定IDをカンマ区切りのリストで指定します。
* **グローバルオブジェクト**
  * イベントキューに使用するグローバルオブジェクトの名前です。
  * 指定しない場合は、`gtag`が使用されます。
  * ほとんどの実装では、デフォルト値を使用します。
* **データレイヤー名**
  * デフォルトでは、グローバルサイトタグによって初期化および参照されるデータレイヤーの名前は`dataLayer`です。
  * ほとんどの実装では、デフォルト値を使用します。
* **ページビューを送信**
  * デフォルトでは、サイトの各ページについてページビューイベントが自動的に記録されます。
  * ページビューイベントをGoogle Analyticsに送信しない場合は、このオプションをfalseに構成します。
* **変数をクリア**
  * 各トラッキングリクエストの後に、通常はトラッカーの存続期間中にわたって構成される項目をクリアします。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳しくは、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## GA4のイベントタイプ

GA4はイベントベースで、以下のタイプのイベントを提供します。

* 自動収集イベント
* 拡張計測機能イベント
* 推奨イベント
* カスタムイベント

次の図は、ユースケースに必要なイベントタイプを判断する方法を示しています。

![](https://docs.tealium.com/images/client-side-tags/ga4-flowchart-event-type-v3.png)

### 自動イベント

GA4では、構成を必要とせず、一部のイベントが自動的に生成されます。自動生成されるイベントとそのパラメータについて詳しくは、[Google Analytics 4の自動収集イベント](https://support.google.com/analytics/answer/9234069/ga4-automatically-collected-events)を参照してください。

### 拡張計測機能イベント

Google Analyticsのインターフェイスで拡張計測機能のオプション（イベント）を有効にすると、コンテンツに対するインタラクションを測定できます。Tag Managementでの構成は必要ありません。拡張計測機能のオプションを有効にすると、ファイルのダウンロードや検索などのユーザーアクティビティに関する情報を提供する追加イベントが送信されます。詳しくは、GA4ドキュメントの[拡張計測機能イベント](https://support.google.com/analytics/answer/9216061?hl=en&ref_topic=9756175)を参照してください。

### 推奨イベント

GA4では、すべてのサイトに推奨されるイベントに加え、オンライン販売やゲームに固有のイベントなど、推奨イベントが提供されています。各推奨イベントには、イベントの追加コンテキストを提供する1つ以上のパラメータがあります。これらのイベントとそのパラメータについて詳しくは、Googleの[推奨イベント](https://support.google.com/analytics/answer/9267735?hl=en&ref_topic=9756175)ドキュメントを参照してください。

### 動的イベントトリガー

データレイヤー属性を**動的イベントトリガー**にマッピングすると、マッピングされた属性の値に基づいてGA4イベントをトリガーできます。

例：

1. `event_name`を動的イベントトリガーにマッピングします。
1. `variable1`を`variable2`にマッピングします。
1. データレイヤーが`{event_name:'value',variable1:'abc'}`の場合、タグは`gtag('event','value',{variable2:'abc'})`をトリガーします。

| 変数 | 説明 |
|:---------|:------------|
| `dynamic_event` | 動的イベントトリガー |

#### タグテンプレートのバージョンを確認する

動的イベントトリガーを使用するには、テンプレートを2023年5月26日版（`20230526`）以降に更新する必要があります。テンプレートのバージョンを確認して更新するには、以下の手順を実行します。

1. **タグ構成**タブに移動し、**詳細構成**をクリックします。
1. **テンプレートを編集**をクリックします。テンプレートウィンドウが表示されます。
1. テンプレートの上部には、テンプレートIDと`YYYYMMDD`形式の日付で始まる日付（タイムスタンプ）があります。
1. タグテンプレートをカスタマイズしている場合は、そのカスタマイズ内容を含めるようにテンプレートを編集します。
1. **更新**をクリックしてテンプレートを更新します。

詳しくは、[テンプレートの管理](https://docs.tealium.com/manage-templates/)を参照してください。

### カスタムイベント

イベントが上記のいずれのイベントタイプにも該当しない場合は、カスタムイベントを送信します。詳しくは、[GA4のカスタムイベント](https://support.google.com/analytics/answer/12229021?hl=en&ref_topic=9756175)を参照してください。

## イベントマッピングの例

このセクションでは、GA4に送信される以下の2つのイベントについて、イベントマッピングの例を示します。

* 訪問がログインする
* 訪問が「お問い合わせ」リンクをクリックする

Tag Managementでイベントをマッピングするには、イベントを発生させるタイミングを指定するデータレイヤー変数の値をマッピングします。以下の例では、送信するイベントを識別するために`tealium_event`変数を使用します。

### ログインイベントの例

ログインイベントでは、`utag.link`呼び出しによって以下のデータがTag Managementに送信されます。

```
utag.link({
   "tealium_event" : "sign in",
   "signin_method" : "email"
 });
```

ログインはGA4の推奨イベントの1つで、ユーザーがどのようにログインしたかを示す`method`というパラメータがあります。GA4タグを構成する際は、マッピングツールボックスを使用して、`tealium_event`変数と`signin_method`変数を以下のようにマッピングします。

* `tealium_event` – **カテゴリ**で**イベントトリガー**を選択し、**トリガー**フィールドに`sign in`を入力して、**イベント**で`login`を選択します。   
![](https://docs.tealium.com/images/client-side-tags/map-tealium-event.png)
* `signin_method` – **カテゴリ**で**イベント固有のパラメータ**を選択し、**イベントパラメータ**フィールドに`method`を入力して、**対象イベント**で`login`を選択します。  
![](https://docs.tealium.com/images/client-side-tags/map-signin-method.png)

変数のマッピングについて詳しくは、[データマッピング](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を参照してください。
### お問い合わせリンクイベントの例

お問い合わせリンクイベントでは、次のデータが `utag.link` 呼び出しでタグ管理に送信されます。

```
utag.link({
   "tealium_event" : "contact us"
 });
```

このイベントは GA4 の推奨イベントではないため、次のようにカスタムイベントとしてマッピングします。

* `tealium_event` – **Category** で **Event Triggers** を選択し、**Trigger** フィールドに `contact us` と入力します。**Event** で `Custom Event` を選択し、**Custom Name** フィールドに `contact_us_click` と入力します。  
![](https://docs.tealium.com/images/client-side-tags/map-contactus-example.png)

変数のマッピングについて詳しくは、[データマッピング](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を参照してください。

## Eコマースイベントのトラッキング

GA4 には、Google Universal Analytics の拡張 Eコマースイベントに相当する Eコマースイベントがあります。GA4 の Eコマースイベントには、次のような違いがあります。

* `checkout_step` イベントと `checkout_options` イベントは、GA4 では `view_cart`、`begin_checkout`、`add_shipping_info`、`add_payment_info` イベントに置き換えられています。
* `product_click` イベントと `select_content` イベント（`items` 配列パラメータを使用）は、GA4 では `select_item` イベントに置き換えられています。
* `promotion_click` イベントと `select_content` イベント（`promotions` 配列パラメータを使用）は、GA4 では `select_promotion` イベントに置き換えられています。

### 推奨イベントの items パラメータ

一部の Eコマースイベントには `items` パラメータがあります。これらのイベントでは、`items` 配列に商品名、カテゴリ、価格などの Eコマース拡張機能の値が自動的に入力されます。

詳しくは、[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)を参照してください。

### カスタム items

商品関連データをアイテムスコープのカスタムディメンションにマッピングするには、`utag` データを `item.myDimension` 配列のメンバーにマッピングします。

たとえば、商品の色を取得してマッピングするには、`utag_data.product_color` を `item.product_color` にマッピングします。

## カスタムディメンション

現在、GA4 のカスタムディメンションには、次の2つのスコープがあります。

* ユーザースコープ
* イベントスコープ

Google Universal Analytics には、次の4つのスコープがあります。

* ヒット（GA4 のイベントに類似）
* セッション
* ユーザー（GA4 のユーザーに類似）
* 商品

Google Universal Analytics の要件を GA4 に移行する際は、妥当な場合にはセッションスコープの変数をユーザースコープの変数として渡すことを検討してください。商品スコープの変数は、Eコマースパラメータとして渡すことができます。詳しくは、[Universal Analytics と Google Analytics 4 のデータの比較 > カスタムディメンションとカスタム指標](https://support.google.com/analytics/answer/9964640?hl=en#custom-dim)を参照してください。

### ユーザープロパティ

GA4 は、言語構成や地域など、訪問のセグメントを示すユーザースコープのプロパティを収集します。

ユーザープロパティを構成するには、マッピングするデータレイヤー変数を選択し、**User Properties** カテゴリを選択して、GA4 のプロパティ名を入力します。マッピングは `set.user_properties.USER_PROPERTY` 形式で追加されます。ここで、`USER_PROPERTY` は GA4 のプロパティ名を表します。

![](https://docs.tealium.com/images/client-side-tags/ga4-user-property.png)

### ユーザー提供データ

GA4 は、ユーザー提供データも収集します。ユーザー提供データを使用すると、顧客は `User-ID` とともに追加のユーザー提供データを指定し、同意を得たうえでハッシュ化したファーストパーティデータを GA4 に送信できます。このデータはプライバシーに配慮した方法で Google のデータと照合され、拡張コンバージョンおよびユーザー属性とインタレストカテゴリに関するレポートに活用されます。

次のユーザー提供データの送信先を使用できます。

* メールアドレス（`email`）
* ハッシュ化されたメールアドレス（`user_data.sha256_email_address`）
* 電話番号（`user_data.phone_number`）
* ハッシュ化された電話番号（`user_data.sha256_phone_number`）
* 名（`user_data.address.first_name`）
* ハッシュ化された名（`user_data.address.sha256_first_name`）
* 姓（`user_data.address.last_name`）
* ハッシュ化された姓（`user_data.address.sha256_last_name`）
* 住所（`user_data.address.street`）
* 市区町村（`user_data.address.city`）
* 地域（`user_data.address.region`）
* 郵便番号（`user_data.address.postal_code`）
* 国（`user_data.address.country`）

## GA4 実装の検証

### イベントのバッチ処理

Google Universal Analytics では、トリガーされたヒットごとに1回のネットワーク呼び出しが行われます。一方、GA4 では、数秒以内に発生したイベントが1回の呼び出しにまとめられます。実装を検証するためにネットワーク呼び出しを調査する際は、1回のネットワークリクエストで複数のイベントが送信される可能性があることに注意してください。

### レポートの遅延

Google のドキュメントによると、呼び出しが行われてから GA4 レポートが生成されるまでに24～48時間かかる場合があります。GA4 のリアルタイムレポートと DebugView を使用して、GA4 プロパティにデータが送信されていることを確認できます。