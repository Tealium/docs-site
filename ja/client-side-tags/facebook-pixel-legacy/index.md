---
title: Facebook Pixel構成ガイド（レガシー版）
description: Facebook Pixelタグは、Facebookカスタムオーディエンスピクセルとコンバージョントラッキングピクセルの機能を組み合わせたものです。
url: https://docs.tealium.com/ja/client-side-tags/facebook-pixel-legacy/
---
これはタグのレガシーバージョンであり、間もなく非推奨となり、[Facebook Pixelタグ]()に置き換えられます。

## 前提条件

* Facebook広告アカウント
* アップグレードされたFacebook Pixel（またはレガシーのカスタムオーディエンスピクセル）
* コンバージョンピクセル（レガシー）

## タグ構成

まず、Tealiumのタグマーケットプレイスにアクセスし、プロファイルにFacebook Pixelタグを追加します。詳細については、[タグの管理]()を参照してください。

標準のPageViewとイベントトラッキングには、ピクセルIDごとに単一のタグインスタンスを構成することがベストプラクティスです。

タグを追加した後、以下の表に記載されている構成を構成します：

| 構成    | 説明    |
|:------|:-----------------|
| タイトル  | &lt;ul&gt;&lt;li&gt;タグを識別するためのユニークな名前を入力します&lt;/li&gt;&lt;li&gt;このタグの複数のインスタンスを追加する場合に重要です&lt;/li&gt;&lt;/ul&gt;       |
| Facebook Pixel ID  | &lt;ul&gt;&lt;li&gt;あなたのFacebook Pixel IDです&lt;/li&gt;&lt;li&gt;これはコードスニペット内で長い数字のシリーズとして表示されます&lt;/li&gt;&lt;li&gt;カンマ区切りのリストとして複数のピクセルIDを追加することができます&lt;/li&gt;&lt;li&gt;例：`fbq(&#39;init&#39;, &#39;12345678901234&#39;)` &lt;/li&gt;&lt;/ul&gt;   |
| コンバージョンピクセルID    | &lt;ul&gt;&lt;li&gt;レガシーのコンバージョンピクセルのトラッキングのみに必要です（非推奨）&lt;/li&gt;&lt;li&gt;IDはコードスニペットに次のように表示されます：&lt;br&gt; `fb_param.pixel_id = &#39;12345&#39;;`&lt;br&gt; または &lt;br&gt;`fbq(&#39;track&#39;, &#39;12345&#39;)` または `fbq.push([&#39;track&#39;, &#39;12345&#39;, { }]);` &lt;/li&gt;&lt;/ul&gt;     |
| デフォルトのページビューを許可    | &lt;ul&gt;&lt;li&gt;すべてのページでPageViewイベントをトリガーします&lt;ul&gt;&lt;li&gt;`True`  &lt;ul&gt;&lt;li&gt;デフォルト値&lt;/li&gt;&lt;li&gt;コンバージョンイベント以外の自動PageViewトラッキングをオンにします&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;`False`  &lt;ul&gt;&lt;li&gt;コンバージョンイベントのトラッキング時にPageViewのトリガーをオフにします&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; ヒント：このデフォルト動作を望まない場合は、`disablePushState`フラグを使用してオフにすることができます。このフラグを`true`に構成すると、履歴状態の変更時に`PageView`イベントの送信を停止します。|
| デフォルトで送信するイベント  | &lt;ul&gt;&lt;li&gt;デフォルトでトリガーしたいイベントを選択します&lt;/li&gt;&lt;li&gt;これは主にコンバージョンピクセルの使用に関連します&lt;/li&gt;&lt;/ul&gt;      |
| アドバンスドマッチング  | &lt;ul&gt;&lt;li&gt;Facebookのアドバンスドマッチングサービスを有効にします。([詳細を学ぶ](https://developers.facebook.com/docs/facebook-pixel/pixel-with-ads/conversion-tracking#advanced_match))&lt;/li&gt;&lt;li&gt;これはデフォルトで有効ですが、アドバンスドマッチングの利点を享受するためには、顧客はデータマッピングを追加する必要があります。&lt;/li&gt;&lt;/ul&gt;     |
| アイテム数の自動計算 | &lt;ul&gt;&lt;li&gt;チェックアウト時のアイテム数を自動的にカウントするかどうかを選択します&lt;/li&gt;&lt;li&gt;デフォルト値は`True`です&lt;/li&gt;&lt;/ul&gt;       |
| trackSingleを有効にする | &lt;ul&gt;&lt;li&gt;FacebookイベントトラッキングコールのためのtrackSingleおよびtrackSingleCustomの使用を有効にします。&lt;/li&gt;&lt;li&gt;これらは、複数のFacebookピクセルがロードされているシナリオで、このタグで構成されたピクセルIDのみに対してトラッキングコールをトリガーします。&lt;/li&gt;&lt;li&gt;デフォルト値は`True`です&lt;/li&gt;&lt;li&gt;例：`fbq(&#39;trackSingle&#39;, &#39;FB_PIXEL_ID&#39;, &#39;Purchase&#39;, customData )` &lt;br&gt; - または - &lt;br&gt; `fbq(&#39;trackSingleCustom&#39;, &#39;FB_PIXEL&#39;)` &lt;/li&gt;&lt;/ul&gt;    |
| trackCustomを有効にする | &lt;ul&gt;&lt;li&gt;Facebookイベントトラッキングコールのための`trackCustom`の使用を有効にします。&lt;/li&gt;&lt;li&gt;カスタムイベントをトラッキングするために、カスタムイベント名と（オプションで）JSONオブジェクトをパラメータとして`fbq(&#39;trackCustom&#39;)`ピクセル関数を呼び出すことができます。&lt;/li&gt;&lt;li&gt;例：プロモーションを共有して割引を得る訪問をトラッキングする場合、次の例に示すカスタムを使用してトラッキングすることができます：`fbq(&#39;trackCustom&#39;,&#39;ShareDiscount&#39;,{promotion:&#39;share_discount_10%&#39;});` &lt;/li&gt;&lt;/ul&gt; |

## ロードルール

[ロードルール]()は、サイト上のどこでこのタグのインスタンスをロードするかを決定します。

推奨されるロードルール：

* 標準的なPageViewとイベントのトラッキングには、デフォルトの**すべてのページ**ルールを使用します
* レガシーのコンバージョンピクセルのトラッキングには、特定のコンバージョンページにタグをロードするためのカスタムルール条件を適用します。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。Facebook Pixelタグの宛先変数はデータマッピングタブに組み込まれています。変数をタグ宛先にマッピングする方法の説明については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。以下のセクションでは利用可能なカテゴリについて説明します：

### **標準**

これらのマッピングを使用して、タグ構成を動的に上書きすることができます。これは、データレイヤーに基づいて値を動的に構成したい場合に便利です。

| 宛先名    | 宛先変数 | 説明     |
|:----|:--|:-----------|
| Facebook Pixel ID   | `cust_pixel` | Facebook Pixelの数値識別子     |
| コンバージョンピクセルID | `conv_pixel` | レガシーのコンバージョンピクセルの数値識別子   |
| 初期ページビューを許可 [`true`/`false`]   | `page_view`  | &#39;init&#39; トラックコール   |
| 発火するイベントのリスト  | `evt_list`   | 変数内でカンマ区切りの値または配列としてリストされたイベント     |
| trackSingleを有効にする [`true`/false]   | `track_single`   | &lt;ul&gt;&lt;li&gt;`trackSingle`および`trackSingleCustom`のイベントトラッキングの使用を有効にします。&lt;/li&gt;&lt;li&gt;複数のFacebookピクセルがロードされている状況で、Tealium iQ内で追加されたピクセルIDにイベントトラッキングを制限します。&lt;/li&gt;&lt;/ul&gt; |
| trackCustomを有効にする&lt;br&gt; [`true`/`false`] | `track_custom`   | &lt;ul&gt;&lt;li&gt;Facebookイベントトラッキングコールのための`trackCustom`の使用を有効にします。&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;カスタムイベント名は文字列でなければならず、長さは50文字を超えてはいけません。&lt;/li&gt;&lt;/ul&gt;  |

### **アドバンスドマッチング**

この追加データを使用すると、より多くのコンバージョンを報告および最適化し、より大きなリマーケティングオーディエンスを構築することができます。チェックアウト、アカウントサインイン、または登録プロセス中にウェブサイトから収集した顧客識別子をピクセルのパラメータとして渡すことができます。

アドバンスドマッチングでは、一致する項目が既に認識されている場合を除き、入力された用語のケースは正規化されます。

| 宛先名 | 宛先変数 | 説明   |
|:------|:--|:------|
| メール    | `em` | メール |
| 名   | `fn` | 名前    |
| 姓 | `ln` | 姓 |
| 電話番号 | `ph` | 電話番号の数値 |
| 性別   | `ge` | `f` または `m`    |
| 生年月日    | `db` | [ `yyyymmdd`] |
| 市 | `ct` | 市  |
| 州    | `st` | 2文字のコード |
| 郵便番号  | `zp` | 郵便番号   |

### **E-コマース**

Facebook PixelタグはE-コマース対応であり、デフォルトで[E-コマースエクステンション]()のマッピングを自動的に使用します。エクステンションのマッピングを上書きするか、エクステンションで提供されていないE-コマース変数を使用したい場合を除き、このカテゴリでの手動マッピングは必要ありません。

| 宛先名  | 宛先変数 | 説明    | E-コマースエクステンション変数 |
|:---|:--|:---|:------|
| 注文ID  | `order_id`   | 最終注文に割り当てられたユニークな識別子  | `_corder` |
| 小計 | `sub_total`  | 最終注文の小計額    | `_csubtotal`  |
| 通貨  | `order_currency` | 支払いに使用される通貨   | `_ccurrency`  |
| 製品IDリスト   | `product_id` | 製品配列内の各製品のユニークな識別子 | `_cprod`  |
| 製品名リスト | `product_name`   | 製品配列内の各製品の名前  | `_cprodname`  |
| カテゴリリスト    | `product_category`   | 製品配列内の各製品のカテゴリ  | `_ccat`   |
| 価格リスト    | `product_unit_price` | 製品配列内の各製品の単価    | `_cprice` |
### 制限されたデータ使用

| 変数  | 説明  |
|:---|:---------|
| `lmt_data.use_ldu` (LDUを使用)  | &lt;ul&gt;&lt;li&gt;`true`の場合、Facebookの制限されたデータ使用オプションを使用します&lt;/li&gt;&lt;li&gt;`false`の場合、Facebookの制限されたデータ使用オプションを使用しません&lt;/li&gt;&lt;/ul&gt;  |
| `lmt_data.ldu_types.geolocate` (LDUはジオロケートするべき) | &lt;ul&gt;&lt;li&gt;`true`の場合、LDUはユーザーの位置を特定します。&lt;/li&gt;&lt;li&gt;`false`の場合、LDUはユーザーの位置を特定しません。**LDUを使用**が有効な場合、**LDUはジオロケートするべき**もデフォルトで有効になります。&lt;/li&gt;&lt;/ul&gt; |
| `lmt_data.ldu_types.california` (LDUはカリフォルニア州)   | &lt;ul&gt;&lt;li&gt;`true`の場合、テンプレート内で州と国のカリフォルニア特有の値を構成します。ユーザーがカリフォルニアに位置しており、制限されたデータ使用で処理する必要がある場合のみこのオプションを有効にします。&lt;/li&gt;&lt;li&gt;`false`の場合、テンプレート内でユーザーの州と国のカリフォルニア特有の値を構成しません。&lt;/li&gt;&lt;/ul&gt; |

## **イベント**

特定のイベントをページ上でトリガーするためにこれらの目的地にマッピングします。イベントはコンバージョンの追跡とFacebook広告のターゲット可能なオーディエンスの構築に使用されます。

購入イベントは、Eコマース拡張機能を通じて、または直接データマッピングを通じて注文ID値が利用可能な場合に自動的にトリガーされます。

イベントをマッピングするには以下の手順を実行します：

1. **トリガー**フィールドに、選択したイベントに対応する目的地にマッピングする変数の値を入力します。
例えば、UDO内で`event_name=&#34;order&#34;`の場合に**購入**イベントをトリガーしたい場合、`order`を入力します（現在`event_name`変数をマッピングしていると仮定します）。
1. **イベント**リストから、希望するイベント（例えば**購入**）を選択します。
1. **&#43; 追加**をクリックします。

### **カスタムイベント**

カスタムイベントの場合、**カスタム**を選択し、カスタムイベントの名前を入力します。

次の例では、変数`event_name`が`inbound_lead_event`と等しい場合にカスタムイベント&#34;InboundLead&#34;がトリガーされます。

![](/images/client-side-tags/custom-event.png)

カスタムイベントを編集するには、目的地入力フィールドをシングルクリックしてイベント名を直接編集します。値は次の形式で入力されます：`{VARIABLE_VALUE}:{DESTINATION_EVENT}`。

* コロンの左側はイベントをトリガーする変数値です、例えば `inbound_lead_event`
* コロンの右側はカスタムイベント名です、例えば `InboundLead`.

### **カスタムイベントデータ**

[イベントタブ](#events_tab)でマッピングしたカスタムイベントにカスタムパラメータを渡したい場合、これらの目的地にマッピングします。

カスタムイベントデータ変数をマッピングするには、以下の手順を実行します：

1. **イベント名**フィールドに、**イベント**タブで指定されたカスタムイベントの名前を正確に入力します。
1. **パラメータ**フィールドに、送信したいパラメータの名前を入力します。
1. **&#43; 追加**をクリックします。

### 標準イベントの完全なリスト

| 目的地イベント    | イベント説明    |
|:--|:------|
| AddPaymentInfo   | 訪問がチェックアウトプロセス中に支払い詳細を追加する     |
| AddToCart    | 訪問がカートにアイテムを追加する     |
| AddToWishlist    | 訪問がウィッシュリストにアイテムを追加する     |
| CompleteRegistration | &lt;ul&gt;&lt;li&gt;訪問が登録フォームを完了する&lt;/li&gt;&lt;li&gt;例：訪問がニュースレターに成功して登録する&lt;/li&gt;&lt;/ul&gt; |
| Contact  | 人が電話、SMS、メール、チャット、またはその他の方法でビジネスに連絡を取る場合。 |
| Conversion   | レガシー変換ピクセルのみ；変換ピクセルIDの構成が必要です |
| Custom   | &lt;ul&gt;&lt;li&gt;訪問のアクションはカスタムイベントとして扱われる&lt;/li&gt;&lt;li&gt;カスタムオーディエンスとカスタムコンバージョンのレポートに使用できる&lt;/li&gt;&lt;/ul&gt;  |
| CustomizeProduct | 人が製品をカスタマイズする場合。  |
| InitiateCheckout | &lt;ul&gt;&lt;li&gt;訪問がチェックアウトプロセスを開始する最初のステップを踏む&lt;/li&gt;&lt;li&gt;例：訪問が**チェックアウトへ進む**ボタンをクリックする&lt;/li&gt;&lt;/ul&gt;   |
| Lead | &lt;ul&gt;&lt;li&gt;訪問のアクションが彼または彼女の購入意向を示す&lt;/li&gt;&lt;li&gt;例：訪問が試用製品にサインアップする&lt;/li&gt;&lt;/ul&gt;  |
| PageView | 訪問がサイトの任意のページを閲覧する  |
| Purchase | 訪問がチェックアウトプロセスの最後のステップを成功裏に完了する&lt;br&gt; 注意：このイベントはコンバージョンの追跡に必要です。**イベント**タブでマッピングしてください |
| Schedule | 人があなたのロケーションのいずれかを訪問するための予約をする場合。   |
| Search   | 訪問が検索アクションを実行する     |
| StartTrial   | 人があなたが提供する製品またはサービスの無料試用を開始する場合。 |
| SubmitApplication    | 人があなたが提供する製品、サービス、またはプログラムに応募する場合。  |
| Subscribe    | 人があなたが提供する製品またはサービスの有料サブスクリプションを開始するために申し込む場合。   |
| ViewContent  | 訪問が特定のページを閲覧し、その閲覧行動を示す  |

## パラメータ

以前にマッピングしたイベントに追加データを渡したい場合、これらの目的地にマッピングします。

パラメータは事前定義されたイベントでのみ使用されます。カスタムイベントにパラメータを渡す方法については、[カスタムイベントデータ](#custom-event-data)セクションを参照してください。

事前定義されたイベントにパラメータを渡すには、以下の手順を実行します：

1. **イベント**フィールドで、ドロップダウンリストからFacebookイベントを選択します。
1. **パラメータ**フィールドで、Facebookパラメータをドロップダウンリストから選択します。
**カスタム**パラメータの場合、パラメータを識別する名前を入力します。
1. **&#43; 追加**をクリックします。

### 事前定義されたパラメータの完全なリスト

| 目的地パラメータ | 説明   |
|:---|:---|
| Value | イベントに関連する値   |
| Currency  | 値パラメータに関連する通貨  |
| Content Name  | 製品またはページの名前   |
| Content Type  | イベントに関連する製品またはページのタイプ |
| Content IDs   | イベントに関連する識別子   |
| Content Category  | 製品またはページのカテゴリ   |
| Number of Items   | チェックアウト時のアイテム数   |
| Search String | 検索アクションで使用されるキーワード/用語    |
| Order ID  | 最終注文の一意の識別子  |
| Status    | CompleteRegistrationイベントの状態  |
| Custom    | 事前定義されたイベントと一緒に渡されるカスタムパラメータ |

### **ホテルパラメータ**

以前にマッピングしたイベントにホテル関連の検索およびホテル予約の詳細を送信するために、次の表にリストされている目的地にマッピングします。

#### ホテルパラメータの完全なリスト

| パラメータ  | 説明|
|:------|:-----|
| Content Type   | &lt;ul&gt;&lt;li&gt;(必須) ホテルに関連する製品またはページのタイプ。&lt;/li&gt;&lt;/ul&gt; 注意：変数値が`hotel`と等しいことを確認してください。 |
| Content IDs    | &lt;ul&gt;&lt;li&gt;(必須) ホテルに関連する一意の識別子。&lt;/li&gt;&lt;/ul&gt;|
| Destination    | &lt;ul&gt;&lt;li&gt;(必須) ホテルが位置する市、州、または国を説明する文字列値。例：`San Fransisco`。&lt;/li&gt;&lt;/ul&gt;|
| Check-in Date  | &lt;ul&gt;&lt;li&gt;(必須) 訪問がホテルにチェックインする日付&lt;/li&gt;&lt;li&gt;ホテルのタイムゾーンに対応&lt;/li&gt;&lt;li&gt;サポートされる日付形式：&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`YYYYMMDD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mmTZD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mm:ssTZD`&lt;/li&gt;&lt;/ul&gt;&lt;/li&gt;&lt;/ul&gt; |
| Check-out Date | &lt;ul&gt;&lt;li&gt;(必須) 訪問がホテルからチェックアウトする日付&lt;/li&gt;&lt;li&gt;ホテルのタイムゾーンに対応&lt;/li&gt;&lt;li&gt;サポートされる日付形式：&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`YYYYMMDD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mmTZD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mm:ssTZD`&lt;/li&gt;&lt;/ul&gt;  &lt;/li&gt;&lt;/ul&gt;    |
| Value  | &lt;ul&gt;&lt;li&gt;(必須) 広告主にとってのイベントの相対的な価値&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;購入イベントに必須です&lt;/li&gt;&lt;/ul&gt;|
| Currency   | &lt;ul&gt;&lt;li&gt;(必須) 値パラメータに関連する通貨&lt;/li&gt;&lt;li&gt;購入イベントに必須です&lt;/li&gt;&lt;/ul&gt;|
#### オプショナルホテルパラメータ

| パラメータ  | 説明   |
|:--|:-------|
| 市区町村   | &lt;ul&gt;&lt;li&gt;(オプショナル) ホテルが位置する市区町村&lt;/li&gt;&lt;/ul&gt;    |
| 地域 | &lt;ul&gt;&lt;li&gt;(オプショナル) ホテルが位置する州・地区&lt;/li&gt;&lt;/ul&gt;  |
| 国    | &lt;ul&gt;&lt;li&gt;(オプショナル) ホテルが位置する国&lt;/li&gt;&lt;/ul&gt; |
| 大人の数   | &lt;ul&gt;&lt;li&gt;(オプショナル) 予約/検索で指定された大人の数&lt;/li&gt;&lt;/ul&gt;   |
| 子供の数 | &lt;ul&gt;&lt;li&gt;(オプショナル) 予約/検索で指定された子供の数&lt;/li&gt;&lt;/ul&gt; |
| おすすめホテル   | &lt;ul&gt;&lt;li&gt;(オプショナル) 訪問に推奨される他のホテルの識別子&lt;/li&gt;&lt;/ul&gt;    |
| ユーザースコア | &lt;ul&gt;&lt;li&gt;(オプショナル) 広告主に対する訪問の相対的な価値&lt;/li&gt;&lt;li&gt;数値を含む必要があります&lt;/li&gt;&lt;/ul&gt; |
| ホテルスコア    | &lt;ul&gt;&lt;li&gt;(オプショナル) 広告主に対するホテルの相対的な価値&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;数値を含む必要があります&lt;/li&gt;&lt;/ul&gt; |
| 購入通貨  | &lt;ul&gt;&lt;li&gt;(オプショナル) ホテル予約取引に関連する通貨&lt;/li&gt;&lt;/ul&gt; |

#### 検索イベント専用のオプショナルホテルパラメータ

| パラメータ   | 説明    |
|:----|:-----|
| 優先星評価  | &lt;ul&gt;&lt;li&gt;(オプショナル) ホテルの星評価によってフィルタされる検索基準&lt;/li&gt;&lt;/ul&gt; |
| 優先価格帯   | &lt;ul&gt;&lt;li&gt;(オプショナル) 客室料金によってフィルタされる検索基準&lt;/li&gt;&lt;/ul&gt;   |
| 優先エリア | &lt;ul&gt;&lt;li&gt;(オプショナル) 位置エリアによってフィルタされる検索基準&lt;/li&gt;&lt;/ul&gt;    |

### **旅行パラメータ**

以下の表に記載されている目的地にマップして、以前にマップしたイベントとともに訪問の旅行詳細（フライトまたはルート旅行）を送信します。

#### 旅行パラメータの完全なリスト

| パラメータ    | 説明|
|:----|:-----------|
| コンテンツタイプ | &lt;ul&gt;&lt;li&gt;(必須) 旅行のタイプがフライトか非フライトかを示します&lt;/li&gt;&lt;/ul&gt; 注意: 変数の値はフライトの場合は `flight`、非フライトの場合は `route` と等しくなければなりません。|
| 出発地   | &lt;ul&gt;&lt;li&gt;(必須) 旅行が始まる市、州、または国を説明する文字列値です。&lt;/li&gt;&lt;li&gt;例: `San Fransisco, California, USA`。&lt;/li&gt;&lt;/ul&gt;|
| 目的地  | &lt;ul&gt;&lt;li&gt;(必須) 目的地の市、州、または国を説明する文字列値です。&lt;/li&gt;&lt;li&gt;例: `Toronto, Ontario, Canada`。&lt;/li&gt;&lt;/ul&gt;|
| 出発日 | &lt;ul&gt;&lt;li&gt;(必須) 往路の旅行が始まる日時&lt;/li&gt;&lt;li&gt;サポートされる日付形式は以下の通りです：&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`YYYYMMDD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mmTZD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mm:ssTZD`&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
| 帰路出発日 | &lt;ul&gt;&lt;li&gt;(必須) 復路の旅行が始まる日時&lt;/li&gt;&lt;li&gt;サポートされる日付形式は以下の通りです：&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`YYYYMMDD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mmTZD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mm:ssTZD`&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt;   |
| 価値    | &lt;ul&gt;&lt;li&gt;(必須) イベントに対する広告主の相対的な価値&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;購入イベントに必須です&lt;/li&gt;&lt;/ul&gt;|
| 通貨 | &lt;ul&gt;&lt;li&gt;(必須) 価値パラメータに関連する通貨&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;購入イベントに必須です&lt;/li&gt;&lt;/ul&gt;|

#### 必須のフライトパラメータ

`content type` の値が `flight` に等しい場合、以下のパラメータが**必須**です：

| パラメータ   | 説明|
|:--|:--------|
| 出発空港  | &lt;ul&gt;&lt;li&gt;(必須) 出発空港の [IATA](https://en.wikipedia.org/wiki/International_Air_Transport_Association_airport_code) コード（3文字の空港識別子）です。&lt;/li&gt;&lt;/ul&gt;  |
| 目的地空港 | &lt;ul&gt;&lt;li&gt;(必須) 目的地空港の [IATA](https://en.wikipedia.org/wiki/International_Air_Transport_Association_airport_code) コード（3文字の空港識別子）です。&lt;/li&gt;&lt;/ul&gt; |

#### オプショナルな旅行パラメータ

| パラメータ  | 説明|
|:----|:------------|
| 出発地市    | &lt;ul&gt;&lt;li&gt;(オプショナル) 旅行が始まる市の名前です&lt;/li&gt;&lt;/ul&gt;|
| 出発地地域  | &lt;ul&gt;&lt;li&gt;(オプショナル) 旅行が始まる州/地域の名前です&lt;/li&gt;&lt;/ul&gt;|
| 出発地国 | &lt;ul&gt;&lt;li&gt;(オプショナル) 旅行が始まる国の名前です&lt;/li&gt;&lt;/ul&gt;|
| 目的地市   | &lt;ul&gt;&lt;li&gt;(オプショナル) 目的地の市の名前です&lt;/li&gt;&lt;/ul&gt;|
| 目的地地域 | &lt;ul&gt;&lt;li&gt;(オプショナル) 目的地の州/地域の名前です&lt;/li&gt;&lt;/ul&gt;|
| 目的地国    | &lt;ul&gt;&lt;li&gt;(オプショナル) 目的地の国の名前です&lt;/li&gt;&lt;/ul&gt;|
| 到着日 | &lt;ul&gt;&lt;li&gt;(オプショナル) 訪問が目的地に到着する日時です&lt;/li&gt;&lt;li&gt;サポートされる日付形式は以下の通りです：&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`YYYYMMDD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mmTZD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mm:ssTZD`&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt;|
| 帰路到着日 | &lt;ul&gt;&lt;li&gt;(オプショナル) 訪問が出発地に戻る日時です&lt;/li&gt;&lt;li&gt;サポートされる日付形式は以下の通りです：&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`YYYYMMDD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mmTZD`&lt;/li&gt;&lt;li&gt;`YYYY-MM-DDThh:mm:ssTZD`&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt;|
| 大人の数   | &lt;ul&gt;&lt;li&gt;(オプショナル) 旅行に参加する大人の数です&lt;/li&gt;&lt;/ul&gt;|
| 子供の数 | &lt;ul&gt;&lt;li&gt;(オプショナル) 旅行に参加する子供の数です&lt;/li&gt;&lt;/ul&gt;|
| 幼児の数  | &lt;ul&gt;&lt;li&gt;(オプショナル) 旅行に参加する幼児の数です&lt;/li&gt;&lt;/ul&gt;|
| 旅行クラス   | &lt;ul&gt;&lt;li&gt;(オプショナル) 訪問が旅行するクラスのタイプを示します。&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;`flight` の場合、変数は `economy`, `premium`, `business`, `first` などの列挙値を含む必要があります。&lt;/li&gt;&lt;li&gt;`route` の場合、変数はカスタム文字列値を含む必要があります。&lt;/li&gt;&lt;li&gt;例: `Economy`&lt;/li&gt;&lt;/ul&gt; |
| ユーザースコア | &lt;ul&gt;&lt;li&gt;(オプショナル) 広告主に対する訪問の相対的な価値です&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;数値を含む必要があります&lt;/li&gt;&lt;/ul&gt;|
| 購入価格 | &lt;ul&gt;&lt;li&gt;(オプショナル) 旅行予約の価格です&lt;/li&gt;&lt;li&gt;購入およびチェックアウト開始イベントに推奨されます。&lt;/li&gt;&lt;/ul&gt;|
| 購入通貨  | &lt;ul&gt;&lt;li&gt;(オプショナル) 予約取引に使用される通貨です&lt;/li&gt;&lt;/ul&gt;|

#### 検索イベント専用のオプショナルな旅行パラメータ

| パラメータ | 説明|
|:----|:-------|
| 優先停留回数 | &lt;ul&gt;&lt;li&gt;(オプショナル) 検索基準は停留回数によってフィルタされます&lt;/li&gt;&lt;li&gt;直行便の場合は変数値を `0` に構成し、訪問が停留回数を指定した場合は `1` に構成します。&lt;/li&gt;&lt;/ul&gt; |

## ユースケース

このセクションでは、実際のシナリオを表すユースケースを提供します。

### ユースケース: PageView と標準/カスタムイベントの追跡

すべてのページで自動的に PageView イベントを発火させ、データマッピングを介して非変換イベントをトリガーします。

このユースケースを環境に構成するための手順は次のとおりです：

1. 次の構成を構成します：
    * **Pixel ID**: `FB_PIXEL_ID`
    * **デフォルトページビューを許可**: `True`
    * **デフォルトイベントの送信**: `None`

1. すべてのページにタグをロードします（デフォルトルール）。
1. 非変換イベントの選択に `event_name` 変数をマップします。

### ユースケース: PageView と変換イベントの追跡（非推奨）

変換イベントをトリガーするには、変換ピクセル ID が必要です。これは、PageView と非変換イベントを追跡するために使用している同じタグインスタンスで行うことができます。

このユースケースを環境に構成するための手順は次のとおりです：

1. 次の構成を構成します：
    * **Pixel ID**: `FB_PIXEL_ID`
    * **変換ピクセル ID**: `CONVERSION_PIXEL_ID`
    * **デフォルトページビューを許可**: `True`
    * **デフォルトイベントの送信**: `None`
1. すべてのページにタグをロードします（デフォルトルール）。
1. 変換イベントの選択に `event_name` 変数をマップします。

### ユースケース: 旧式の変換ピクセルのみの追跡（非推奨）

変換ピクセルは別のタグインスタンスで追跡する必要があります。このタグインスタンスでは、Pixel ID を空白にし、自動ページビュー追跡を無効にします。特定のイベントを追跡していないため、データマッピングは必要ありません。

このユースケースを環境に構成するための手順は次のとおりです：

1. 次の構成を構成します：
    * **変換ピクセル ID**: `CONVERSION_PIXEL_ID`
    * **デフォルトページビューを許可**: `False`
    * **デフォルトイベントの送信**: `Conversion`

1. 特定の変換ページにこのタグをロードするためのカスタムロードルールを適用します。
### 使用例：1ページに複数のピクセル

以下の使用例は、1ページに複数のピクセルを使用するシナリオを示しています：

* **共有イベントトラッキング**
  * 複数のFacebookピクセルでページビューやイベントトラッキングを共有したい場合、タグ構成のFacebookピクセルIDフィールドにピクセルIDのカンマ区切りリストを追加できます。
  * 複数のFacebookピクセルがそれぞれのピクセルIDを持っている場合、`trackSingle`構成が`false`であれば他のFacebookピクセルとイベントトラッキングを共有することができますが、これはトラッキングの一貫性が損なわれる可能性があり、推奨されません。

* **個別イベントトラッキング**
  * 1ページに複数のFacebookピクセルをロードして、そのページの全てのピクセルに対してトラッキングイベントが記録されるのを防ぎたい場合は、**Enable trackSingle** 構成を `true` にしてください。
  * この構成により、そのタグに追加されたピクセルIDのみでイベントトラッキングが行われます。
  * 2018年3月以前にTealium iQでFacebookピクセルを追加した場合、trackSingle機能を利用できない可能性があります。
    * この場合、[Facebookタグテンプレートを最新バージョンに更新してください]()。trackSingle構成はデフォルトで`true`に構成されています。
    * `track_single`にマッピングし、この機能を無効にするために値を`false`に構成する必要があります。

* **2018年3月以前のバージョン**
  * 2018年3月以降にタグを追加した場合は、複数のFacebookピクセルを構成する際に上記の使用例を参照してください。
  * 古いバージョンのFacebookピクセルは、[1ページに複数回ロードされるように設計されていませんでした](https://www.facebook.com/business/help/community/question/?id=10100525729830570)。
  * Facebook JavaScriptライブラリは`fbq`オブジェクトの単一インスタンスを初期化し、ページ上で発生するすべてのトラッキングに使用されます（同じピクセルIDを再利用します）。
  * 1ページに異なるピクセルIDを持つ複数のFacebookピクセルを発火させる必要があり、タグテンプレートを更新できない場合は、[Tealium Genericタグ]()を使用して`&lt;noscript&gt;`バージョンのピクセルを実装することをお勧めします。

#### 例示シナリオ

Facebookピクセルの`&lt;noscript&gt;`コードの例：

```
`&lt;noscript&gt;&lt;br&gt;
&lt;img height=&#34;1&#34; width=&#34;1&#34; style=&#34;display:none&#34;&lt;br&gt;
 src=&#34;https://www.facebook.com/tr?id={{FACEBOOK_PIXEL_ID}}&amp;ev=PageView&amp;noscript=1&#34;&lt;br&gt;
/&gt;&lt;br&gt;
&lt;/noscript&gt;`
```

このシナリオでは、隠された画像ピクセルのURLは次のように構成できます：

1. Tealium Genericタグを追加します。
1. **Title** を `Facebook Pixel (custom)` に構成します。
1. **Base URL** を `https://www.facebook.com/tr` に構成します。
1. **Query String** を `id={{FACEBOOK_PIXEL_ID}}&amp;ev=PageView&amp;noscript=1&#34;` に構成します。  
![](/images/client-side-tags/facebook-tag-generic-tag-pixel.png)

1. 必要なロードルールとデータマッピングを構成します。
1. **Apply** をクリックします。

## Tealium iQのFacebookダイナミック広告

Tealium iQでFacebookダイナミック広告を構成する方法についての詳細は、TLC記事 [How to Set up Facebook Dynamic Ads in Tealium iQ](/ja/client-side-tags/facebook-dynamic-ads-tag/) を参照してください。

## ベンダー文書

詳細については、以下のベンダー文書を参照してください：

* [廃止されたピクセルからの移行](https://developers.facebook.com/docs/facebook-pixel/pixel-migration)
* [参照：標準およびカスタムイベント](https://developers.facebook.com/docs/facebook-pixel/api-reference#events)
* [FacebookピクセルFAQ](https://www.facebook.com/business/help/651294705016616)
* [広告主ヘルプセンター：TealiumでのFacebookピクセルの使用](https://www.facebook.com/business/help/978910435507261)
* [ピクセルを使用したコンバージョントラッキング](https://developers.facebook.com/docs/facebook-pixel/pixel-with-ads/conversion-tracking#advanced_match)
