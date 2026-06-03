---
title: アコースティックデジタルアナリティクスタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAcoustic Digital Analyticsタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/acoustic-digital-analytics-tag/
---
## タグのヒント

* E-Commerce Extensionで構成された値を上書きするための値をマッピングできます（推奨されません）
* マッピングツールボックスは、各イベントに対して10のカスタム属性を表示します。Acoustic Digital Analyticsは50の属性をサポートしています。10を超える値にマッピングするには、ツールボックス内の数字を直接編集します
* マニュアルページビュータグを使用するには、マニュアルページビュー宛先URLに値をマップします（他の値は標準のページビューマッピングから取得されます）

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Acoustic Digital Analyticsタグを追加します（[タグの追加方法]()について詳しくはこちらをご覧ください）。

タグを追加したら、以下の構成を行います：

* **タグバージョン**：External（デフォルト）オプションを使用して、eluminate.jsをAcousticがホストするCDNからロードします。これにより、常にAcousticから最新のライブラリコードを取得できます。
* **クライアントID**：cmSetClientID関数への最初のパラメータ（例：`89999999`&amp;#124;`SiteID`）。この値はマッピングを通じて構成することもできます。
* **テストクライアントID**：テストドメインリストで一致が見つかった場合に使用されるクライアントIDです。
* **収集方法**：Trueはクライアント管理のファーストパーティクッキーを示します。FalseはAcoustic管理のファーストパーティまたはサードパーティ（該当する場合）を示します。
* **収集ドメイン**：Acousticデータ収集リクエストのターゲットドメインです。
* **クッキードメイン**：クライアント管理のクッキーのドメイン（例：tealium.com）。
* **テストドメイン**：テストドメインのカンマ区切りリスト。これは完全なドメインです（例：`dev1.tealium.com`,`qa-serv3.tealium.com`）。
* **外部スクリプトURL**：外部タグバージョンでのみ使用されます。

## データタグとマッピング

データレイヤー変数のマッピングを開始する前に、必ず[E-Commerce Extension]()を追加してください。これにより、Product View、ShopAction5、ShopAction9などのイベントに必要なe-commerce変数が自動的にマップされます。

Acoustic Digital Analyticsのデータタグは、受け取ったデータを整理する関数です。各関数呼び出しには、&#34;Attributes&#34;と呼ばれるカスタムメトリクスが利用可能です。属性は、ほとんどの関数で1-100の範囲の番号付き変数に格納され、トラッキングコールでは`pv_a1…pv_a100`（ページビュー属性1-100）のような名前が付けられます。

Tealiumのデータレイヤーから`tealium_event`変数を使用して、どのAcoustic Digital AnalyticsイベントをTealiumのトラッキングイベントに関連付けるかを特定します。

### マッピングツールボックス

マッピングツールボックスは、Acoustic Digital Analyticsデータタグに従って整理されているため、データを送信する先を簡単に選択できます。以下に、各セクションで利用可能な変数の完全なリストを示します。

### イベント

まず、**イベント**タブの構成を開始します。これらのマッピングは、いつ各Acoustic Digital Analyticsデータタグ関数を発火するかを制御します。`tealium_event`変数（または他のイベント変数）を使用して、どのデータタグ関数を発火するかを決定します。

イベントをマップするには：

1. **イベント**カテゴリを選択します。
1. **値**フィールドに、Tealiumのトラッキングイベントの値を入力します。
1. **トリガー**ドロップダウンから、一致するイベントを選択します。
1. **&#43;追加**をクリックします。これらの手順を繰り返して、追加のイベントマッピングを追加します。

![](/images/client-side-tags/ibm-digital-analytics-mapped-events.png)

#### 注文

このデータタグにはマッピングタブがありません。ただし、この関数をページで発火させるためには、E-commerce extensionを構成する必要があります。extensionが構成されている場合、`_corder`変数は自動的にマップされます。

**データタグ:** 注文 

**タグ関数:** `cmCreateOrderTag()`

**説明**: このデータタグは、最終的な注文情報（登録ID、注文ID、注文小計、送料と手数料など）をキャプチャします。この関数呼び出しは、購入確認ページで送信する必要があります。注文ごとに1つの注文関数を呼び出すべきです。E-Commerce extension変数`Order ID`（`_corder`）が入力されている場合、この関数は自動的に実行されます。

### ページビュー

**Acousticデータタグ:** ページビュー 

**タグ関数:** `cmCreatePageViewTag()`

**説明**: このデータタグは、訪問がサイトをナビゲートする際のページ情報をキャプチャします。この関数は、ページビューを測定したいすべてのページで呼び出すべきです。

**マッピング**: マッピングツールキットを使用して、以下の宛先変数をマップします：

* ページID（`pi`） - ページの英数字識別子
* ページカテゴリ（`cg`） - ページが属するカテゴリ
* 検索文字列（`si`） - 検索結果ページを生成するために使用された検索キーワード
* 検索結果（`sr`） - キーワード検索によって返された結果の数
* 属性変数 `pv_a1` から `pv_a10`まで
* 追加フィールド変数 `pv1` から `pv10`まで

### 商品ビュー

**データタグ:** 商品ビュー

**タグ関数:** `cmCreateProductViewTag()`

**説明**: このデータタグは、商品が受け取ったビューに関する情報をキャプチャします。関連する複数の商品詳細のビューを追跡するために、1つのページから複数の商品ビュー関数呼び出しを送信することができます。

**マッピング**: マッピングツールキットを使用して、Product Virtual Category (cm_vc)とすべての属性変数（`pr_a1`から`pr_a10`まで）をマップします。

E-Commerce Extensionが構成されている場合、以下の項目が自動的にマップされます：

* `_cprod`を商品ID（`pr`）に、商品の一意の識別子
* `_cprodname`を商品名（`pm`）に、表示される商品の名前
* `_ccat`を商品カテゴリ（`cg`）に、商品が属するカテゴリ

### カートビュー（ShopAction5）

**データタグ:** ShopAction5（カートビュー）

**タグ関数:** `cmCreateShopAction5Tag()`

**説明**: このデータタグは、選択された商品とショッピングカートに存在する商品に関するデータをキャプチャします。この関数は、カート内の各商品に対して呼び出すべきです（カート内に3つの商品がある場合、Shop Action 5関数呼び出しは3回行われます）。

**マッピング**: マッピングツールキットを使用して、すべての属性（`s_a1`から`s_a10`まで）とExtra Field（`sx1`から`sx10`まで）変数をマップします。

E-Commerce Extensionが構成されている場合、以下の項目が自動的にマップされます：

* `_cprod`を商品ID（`pr`）に - 商品の一意の識別子
* `_cprodname`を商品名（`pm`）に - カートで表示される商品の名前
* `_cquan`を商品数量（`qt`）に - カートで表示される商品の数量
* `_cprice`を商品価格（`bp`）に - 商品の単価
* `_ccat`を商品カテゴリ（`cg`）に - 商品が属するカテゴリ

### 注文（ShopAction9）

**データタグ:** Shop Action 9（注文商品）

**タグ関数:** `cmCreateShopAction9Tag()`

**説明:** このデータタグは、訪問が購入した商品に関する情報をキャプチャします。この関数呼び出しは、注文の各行項目に対してレシートまたは確認ページで行うべきです。Tealium E-Commerce Extensionの注文ID変数（_corder）が入力されている場合、この関数は自動的に実行されます。

**マッピング**: マッピングツールキットを使用して、すべての属性（`o_a1`から`o_a10`まで）とExtra Field（`or1`から`sx10`まで）変数をマップします。

E-Commerce Extensionが構成されている場合、以下のShopAction 9変数が自動的にマップされます：

* `_ccustid`をShopAction9登録ID（`cd`）に、一意の登録コード。E-Commerce Extensionを通じて、またはマッピングツールボックスを手動でこの宛先に何もマップしない場合、Tealiumは`utag_main`クッキーからのセッションIDを自動的にこの宛先にマップします。
* `_corder`をShopAction9注文番号（`on`）に
* `_csubtotal`をShopAction9注文小計（`tr`）に
* `_cprod`をShopAction9商品ID（`pr`）に
* `_cprodname`をShopAction9商品名（`pm`）に
* `_cquan`をShopAction9数量（`qt`）に
* `_cprice`をShopAction9商品価格（`bp`）に
* `_ccat`をShopAction9商品カテゴリ（`cg`）に
そして、これらの注文変数、

* `_cship` を注文配送金額（`sg`）に
* `_ccity` を注文都市（`ct`）に
* `_cstate` を注文州（`sa`）に
* `_czip` を注文の郵便番号/郵便番号（`zp`）に

### 登録

**データタグ:** 登録

**タグ付け機能:** `cmCreateRegistrationTag()`

**説明**: このデータタグは、サイト上の登録イベントを追跡し、登録の一部として提供された訪問の人口統計情報（郵便番号、都市、州など）とメールアドレスを収集します。E-Commerce Extensionを使用していない場合、TealiumはShopAction9登録IDにマッピングされた値か、`utag_main`クッキーからのセッションIDを使用します。

**マッピング**: マッピングツールキットを使用して、登録メール（`em`）とすべてのExtra Field（`rg1`から`rg10`まで）変数をマッピングします。

E-Commerce Extensionが構成されている場合、自動的にマッピングします：

* `_ccustid` を登録ID（`cd`）に。E-Commerce Extensionを使用していない場合、TealiumはShopAction9登録IDにマッピングされた値か、`utag_main`クッキーからのセッションIDを使用します。
* `_ccity` を登録都市（`ct`）に
* `_cstate` を登録州（`sa`）に
* `_czip` を登録の郵便番号/郵便番号（`zp`）に
* `_ccountry` を登録国（`cy`）に

### コンバージョンイベント

**データタグ:** コンバージョンイベント

**タグ付け機能:** `cmCreateConversionEventTag()`

**説明**: このデータタグは、コンバージョンイベントの非金銭的詳細を収集します。高ボリュームのページのロード時にコンバージョンイベントタグを追加すると、サーバーコール料金が増加する可能性があることに注意してください。

**マッピング**: これらの変数をマッピングするためのマッピングツールキットを使用します：

* コンバージョンイベントID（`cid`） - コンバージョンの種類の一意の識別子
* コンバージョンイベントアクションタイプ（`cat`） - コンバージョンイベントの開始または成功した完了
* コンバージョンイベントカテゴリID（`ccid`） - イベントIDのカテゴリ
* コンバージョンイベントポイント（`cpt`） - コンバージョンの価値を測定するために割り当てられたポイント
* 属性変数 `c_a1` から `c_a10` まで
* Extra Field変数 `cx1` から `cx5` まで

### 要素

**データタグ:** 要素 

**タグ付け機能**: `cmCreateElementTag`

**説明**: このデータタグは、訪問のサイト上の動的要素との相互作用を追跡します。動的要素の例には、ビデオ、ホバーオーバー、エラーメッセージ、機能セレクターなどがあります。

**マッピング**: これらの変数をマッピングするためのマッピングツールキットを使用します：

* 要素ID（`eid`） - 追跡される要素の一意の識別子
* 要素カテゴリ（`ecat`） - 要素が属するカテゴリ

コンバージョンイベントID（`cid`）にマッピングするデータソースとは異なるデータソースを要素ID（`eid`）にマッピングすることを確認してください。

### マニュアル

このセクションは、3つの異なるデータタグ機能に適用されます：Manual Link Click、Manual Page View、およびManual Impression。

**データタグ:** Manual Link Click

**タグ付け機能**: `cmCreateManualLinkClickTag()`

**説明**: このデータタグは、自動的に追跡されないリンククリックをキャプチャします。例えば：

* `HREF=&#34;&#34;`属性がないリンク、またはクリック時にJavaScriptを使用してナビゲーションを作成するリンク。
* HTMLアンカーがないFlash、Silverlight、または他の対話型アプリケーション要素。

**マッピング**: マッピングツールキットを使用して、Manual Link Click/Page View/Impressionの目的地変数をマッピングします：

* Manual Link HREF（`hr`） - クリックされたリンクのhref値
* Manual Link Name（`nm`） - クリックされたリンクの名前
* Manual Link Page ID（`pi`） - ページを識別する一意の英数字値

**データタグ:** Manual Page View 

**タグ付け機能**: `cmCreateManualPageviewTag()`

**説明**: このデータタグは、ページロードイベントを持たないページビューイベントをキャプチャします（例えば、モーダルポップアップなど）。

* Manual Page View Destination URL（`ul`） - 目的地のURL
* Manual Page View Referring URL（`rf`） - 参照URL

**データタグ:** Manual Impression

**タグ付け機能**: `cmCreateManualImpressionTag ()`

**説明**: このデータタグは、ディスプレイ広告タグのような特定の機能からの広告インプレッションをキャプチャします。

* Manual Impression Page ID（`pi`） - インプレッションのPage IDはLink Page ID（`pi`）と一致します
* Manual Impression Track Real Estate（`cm_re`） - 有効な`cm_re=`値を持つReal Estate Impression：`version-_-area-_-link`
* Manual Impression Track Site Promotion（`cm_sp`） - 有効な`cm_sp=`値を持つSite Promotion Impression：`group-_-promotion-_-link`

### Config

このタブは、任意のData Tag機能に対応していません。代わりに、テストサイト/環境に接続されたAcoustic Digital Analytics Tagの構成構成を動的に構成するために使用できます。

* Client ID（`ClientID`） - Acoustic Digital Analyticsによって割り当てられたID
* Test Client ID（`TestClientID`） - テストサイトのClient ID
* Test Data Collection Method（`TestDataCollectionMethod`） - テストサイトのData Collection Method
* Test Data Collection Domain（`TestDataCollectionDomain`） - テストサイトのデータ収集ドメイン

## データマッピング参照

マッピングは、[データレイヤー変数]()からベンダータグの対応する目的地変数にデータを送信するプロセスです。タグの目的地に変数をマッピングする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### ページビュー

| 変数           | 説明 |
|:---------------|:------------|
| Page ID        | (`pi`)      |
| Page Category  | (`cg`)      |
| Search String  | (`se`)      |
| Search Results | (`sr`)      |
| Attribute 1    | (`pv_a1`)   |
| Attribute 2    | (`pv_a2`)   |
| Attribute 3    | (`pv_a3`)   |
| Attribute 4    | (`pv_a4`)   |
| Attribute 5    | (`pv_a5`)   |
| Attribute 6    | (`pv_a6`)   |
| Attribute 7    | (`pv_a7`)   |
| Attribute 8    | (`pv_a8`)   |
| Attribute 9    | (`pv_a9`)   |
| Attribute 10   | (`pv_a10`)  |
| Extra Field 1  | (`pv1`)     |
| Extra Field 2  | (`pv2`)     |
| Extra Field 3  | (`pv3`)     |
| Extra Field 4  | (`pv4`)     |
| Extra Field 5  | (`pv5`)     |
| Extra Field 6  | (`pv6`)     |
| Extra Field 7  | (`pv7`)     |
| Extra Field 8  | (`pv8`)     |
| Extra Field 9  | (`pv9`)     |
| Extra Field 10 | (`pv10`)    |

### 商品ビュー

| 変数                 | 説明 |
|:-------------------------|:------------|
| Product ID               | (`pr`)      |
| Product Name             | (`pm`)      |
| Product Category         | (`cg`)      |
| Product Virtual Category | (`cm_vc`)   |
| Attribute 1              | (`pr_a1`)   |
| Attribute 2              | (`pr_a2`)   |
| Attribute 3              | (`pr_a3`)   |
| Attribute 4              | (`pr_a4`)   |
| Attribute 5              | (`pr_a5`)   |
| Attribute 6              | (`pr_a6`)   |
| Attribute 7              | (`pr_a7`)   |
| Attribute 8              | (`pr_a8`)   |
| Attribute 9              | (`pr_a9`)   |
| Attribute 10             | (`pr_a10`)  |

### カートビュー (ShopAction5)

| 変数                   | 説明 |
|:---------------------------|:------------|
| Product ID                 | (`pr`)      |
| Product Name               | (`pm`)      |
| Product Quantity           | (`qt`)      |
| Product Price              | (`bp`)      |
| Product Category           | (`cg`)      |
| ShopAction5 Attribute 1    | (`s_a1`)    |
| ShopAction5 Attribute 2    | (`s_a2`)    |
| ShopAction5 Attribute 3    | (`s_a3`)    |
| ShopAction5 Attribute 4    | (`s_a4`)    |
| ShopAction5 Attribute 5    | (`s_a5`)    |
| ShopAction5 Attribute 6    | (`s_a6`)    |
| ShopAction5 Attribute 7    | (`s_a7`)    |
| ShopAction5 Attribute 8    | (`s_a8`)    |
| ShopAction5 Attribute 9    | (`s_a9`)    |
| ShopAction5 Attribute 10   | (`s_a10`)   |
| ShopAction5 Extra Field 1  | (`sx1`)     |
| ShopAction5 Extra Field 2  | (`sx2`)     |
| ShopAction5 Extra Field 3  | (`sx3`)     |
| ShopAction5 Extra Field 4  | (`sx4`)     |
| ShopAction5 Extra Field 5  | (`sx5`)     |
| ShopAction5 Extra Field 6  | (`sx6`)     |
| ShopAction5 Extra Field 7  | (`sx7`)     |
| ShopAction5 Extra Field 8  | (`sx8`)     |
| ShopAction5 Extra Field 9  | (`sx9`)     |
| ShopAction5 Extra Field 10 | (`sx10`)    |

### 注文 (ShopAction9)

| 変数                          | 説明 |
|:----------------------------------|:------------|
| ShopAction9登録ID       | (`cd`)      |
| ShopAction9注文番号     | (`on`)      |
| ShopAction9注文小計     | (`tr`)      |
| ShopAction9製品ID (pr)  | [配列]     |
| ShopAction9製品名 (pm)  | [配列]     |
| ShopAction9製品数量 (qt)| [配列]     |
| ShopAction9製品価格 (bp)| [配列]     |
| ShopAction9製品カテゴリ (cg)| [配列] |
| ShopAction9属性1        | (`s_a1`)    |
| ShopAction9属性2        | (`s_a2`)    |
| ShopAction9属性3        | (`s_a3`)    |
| ShopAction9属性4        | (`s_a4`)    |
| ShopAction9属性5        | (`s_a5`)    |
| ShopAction9属性6        | (`s_a6`)    |
| ShopAction9属性7        | (`s_a7`)    |
| ShopAction9属性8        | (`s_a8`)    |
| ShopAction9属性9        | (`s_a9`)    |
| ShopAction9属性10       | (`s_a10`)   |
| ShopAction9追加フィールド1 | (`sx1`) |
| ShopAction9追加フィールド2 | (`sx2`) |
| ShopAction9追加フィールド3 | (`sx3`) |
| ShopAction9追加フィールド4 | (`sx4`) |
| ShopAction9追加フィールド5 | (`sx5`) |
| ShopAction9追加フィールド6 | (`sx6`) |
| ShopAction9追加フィールド7 | (`sx7`) |
| ShopAction9追加フィールド8 | (`sx8`) |
| ShopAction9追加フィールド9 | (`sx9`) |
| ShopAction9追加フィールド10| (`sx10`)|
| 注文番号                 | (`on`)      |
| 注文小計                 | (`tr`)      |
| 注文送料                 | (`sg`)      |
| 注文登録ID              | (`cd`)      |
| 注文都市                 | (`ct`)      |
| 注文州                   | (`sa`)      |
| 注文郵便/郵便番号        | (`zp`)      |
| 注文属性1                | (`o_a1`)    |
| 注文属性2                | (`o_a2`)    |
| 注文属性3                | (`o_a3`)    |
| 注文属性4                | (`o_a4`)    |
| 注文属性5                | (`o_a5`)    |
| 注文属性6                | (`o_a6`)    |
| 注文属性7                | (`o_a7`)    |
| 注文属性8                | (`o_a8`)    |
| 注文属性9                | (`o_a9`)    |
| 注文属性10               | (`o_a10`)   |
| 注文追加フィールド1      | (`or1`)     |
| 注文追加フィールド2      | (`or2`)     |
| 注文追加フィールド3      | (`or3`)     |
| 注文追加フィールド4      | (`or4`)     |
| 注文追加フィールド5      | (`or5`)     |
| 注文追加フィールド6      | (`or6`)     |
| 注文追加フィールド7      | (`or7`)     |
| 注文追加フィールド8      | (`or8`)     |
| 注文追加フィールド9      | (`or9`)     |
| 注文追加フィールド10     | (`or10`)    |

### 登録

| 変数                     | 説明 |
|:--------------------------|:------------|
| 登録ID                   | (`cd`)      |
| 登録メール               | (`em`)      |
| 登録都市                 | (`ct`)      |
| 登録州                   | (`sa`)      |
| 登録郵便/郵便番号        | (`zp`)      |
| 登録国                   | (`cy`)      |
| 登録属性1                | (`rg1`)     |
| 登録属性2                | (`rg2`)     |
| 登録属性3                | (`rg3`)     |
| 登録属性4                | (`rg4`)     |
| 登録属性5                | (`rg5`)     |
| 登録属性6                | (`rg6`)     |
| 登録属性7                | (`rg7`)     |
| 登録属性8                | (`rg8`)     |
| 登録属性9                | (`rg9`)     |
| 登録属性10               | (`rg10`)    |

### 変換イベント

| 変数                            | 説明 |
|:-------------------------------|:------------|
| 変換イベントID                 | (`cid`)     |
| 変換イベントアクションタイプ   | (`cat`)     |
| 変換イベントカテゴリID         | (`ccid`)    |
| 変換イベントポイント           | (`cpt`)     |
| 変換イベント属性1              | (`c_a1`)    |
| 変換イベント属性2              | (`c_a2`)    |
| 変換イベント属性3              | (`c_a3`)    |
| 変換イベント属性4              | (`c_a4`)    |
| 変換イベント属性5              | (`c_a5`)    |
| 変換イベント属性6              | (`c_a6`)    |
| 変換イベント属性7              | (`c_a7`)    |
| 変換イベント属性8              | (`c_a8`)    |
| 変換イベント属性9              | (`c_a9`)    |
| 変換イベント属性10             | (`c_a10`)   |
| 変換イベント追加フィールド1    | (`cx1`)     |
| 変換イベント追加フィールド2    | (`cx2`)     |
| 変換イベント追加フィールド3    | (`cx3`)     |
| 変換イベント追加フィールド4    | (`cx4`)     |
| 変換イベント追加フィールド5    | (`cx5`)     |

#### 要素

| 変数                     | 説明 |
|:---------------------|:------------|
| 要素ID               | (`eid`)     |
| 要素カテゴリ         | (`ecat`)    |
| 要素属性1            | (`e_a1`)    |
| 要素属性2            | (`e_a2`)    |
| 要素属性3            | (`e_a3`)    |
| 要素属性4            | (`e_a4`)    |
| 要素属性5            | (`e_a5`)    |
| 要素属性6            | (`e_a6`)    |
| 要素属性7            | (`e_a7`)    |
| 要素属性8            | (`e_a8`)    |
| 要素属性9            | (`e_a9`)    |
| 要素属性10           | (`e_a10`)   |

### マニュアル

| 変数                               | 説明 |
|:---------------------------------------|:------------|
| マニュアルリンクHREF                  | (`hr`)      |
| マニュアルリンク名                    | (`nm`)      |
| マニュアルリンクページID              | (`pi`)      |
| マニュアルページビュー宛先URL         | (`ul`)      |
| マニュアルページビュー参照URL         | (`rf`)      |
| マニュアルインプレッションページID     | (`pi`)      |
| マニュアルインプレッショントラック不動産 | (`cm_re`)   |
| マニュアルインプレッショントラックサイトプロモーション | (`cm_sp`)   |

### エラー

| 変数               | 説明 |
|:---------------|:------------|
| ページID        | (`pi`)      |
| エラーカテゴリ  | (`cg`)      |

### イベント

| 変数             | 説明  |
|:-----------------|:-------------|
| 登録             | 登録 |
| 注文             | 注文        |
| カート/ShopAction5 | ShopAction5  |
| 製品ビュー       | Productview  |
| 変換イベント     | 変換   |
| 要素             | 要素      |
| エラー           | エラー        |

### 構成

| 変数                               | 説明                  |
|:---------------------------------------|:-----------------------------|
| クライアントID                       | (`ClientID`)                 |
| テストクライアントID                 | (`TestClientID`)             |
| テストデータ収集方法                 | (`TestDataCollectionMethod`) |
| テストデータ収集ドメイン             | (`TestDataCollectionDomain`) |
| 高度な構成オブジェクト (`cmSetupOther`) | [オブジェクト]                     |
