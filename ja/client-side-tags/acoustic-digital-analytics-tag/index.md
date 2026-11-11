---
title: Acoustic Digital Analyticsタグ構成ガイド
description: この記事では、タグ管理アカウントでAcoustic Digital Analyticsタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/acoustic-digital-analytics-tag/
---
## タグに関するヒント

* E-Commerce Extensionで構成された値を上書きするように値をマッピングできます（非推奨）。
* マッピングツールボックスには、イベントごとに10個のカスタム属性が表示されます。Acoustic Digital Analyticsは50個の属性をサポートしています。10を超える番号の値にマッピングするには、ツールボックス内の番号を直接編集します。
* Manual Page Viewタグを使用するには、値をManual Page View Destination URLにマッピングします（その他の値は標準のPage Viewマッピングから取得されます）。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を構成します。

* **タグバージョン**：AcousticがホストするCDNからeluminate.jsを読み込むには、External（デフォルト）オプションを使用します。これにより、常にAcousticの最新ライブラリコードを使用できます。
* **クライアントID**：cmSetClientID関数の最初のパラメータです（例：`89999999`&#124;`SiteID`）。この値はマッピングでも構成できます。
* **テストクライアントID**：Test Domainsリストで一致が見つかった場合に使用されるクライアントIDです。
* **収集方法**：Trueは、クライアント管理のファーストパーティCookieを示します。Falseは、状況に応じてAcoustic管理のファーストパーティCookieまたはサードパーティCookieを示します。
* **収集ドメイン**：Acousticのデータ収集リクエストの送信先ドメインです。
* **Cookieドメイン**：クライアント管理Cookieのドメインです（例：tealium.com）。
* **テストドメイン**：テストドメインのカンマ区切りリストです。完全なドメインを指定します（例：`dev1.tealium.com`,`qa-serv3.tealium.com`）。
* **外部スクリプトURL**：Externalタグバージョンでのみ使用されます。

## データタグとマッピング


<blockquote>
データレイヤー変数のマッピングを開始する前に、必ず[E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/)を追加してください。これにより、Product View、ShopAction5、ShopAction9などのイベントに必要なEコマース変数が自動的にマッピングされます。
</blockquote>


Acoustic Digital Analyticsのデータタグは、受信したデータを整理する関数です。「属性」と呼ばれるカスタム指標を各関数呼び出しで使用できます。ほとんどの関数では、属性は番号付き変数（通常は1～100）に格納され、トラッキング呼び出しでは`pv_a1…pv_a100`（Page View Attributes 1～100）のような命名規則が使用されます。


<blockquote>
データレイヤーの`tealium_event`変数を使用して、Tealiumでトラッキングされるイベントに関連付けるAcoustic Digital Analyticsイベントを特定します。
</blockquote>


### マッピングツールボックス

マッピングツールボックスはAcoustic Digital Analyticsのデータタグに従って整理されているため、データの送信先を簡単に選択できます。以下に、各セクションで使用可能な変数の完全なリストを示します。

### イベント

まず、**Events**タブを構成します。これらのマッピングは、各種Acoustic Digital Analyticsデータタグ関数を実行するタイミングを制御します。`tealium_event`変数（または別のイベント変数）を使用して、実行するデータタグ関数を決定します。

イベントをマッピングするには、次の手順を実行します。

1. **Events**カテゴリを選択します。
1. **Value**フィールドに、Tealiumでトラッキングされるイベントの値を入力します。
1. **Trigger**ドロップダウンから、一致するイベントを選択します。
1. **+Add**をクリックします。イベントマッピングをさらに追加するには、この手順を繰り返します。

![](https://docs.tealium.com/images/client-side-tags/ibm-digital-analytics-mapped-events.png)

#### 注文

このデータタグにはマッピングタブがありません。ただし、ページ上でこの関数を実行するには、E-Commerce Extensionを構成する必要があります。構成されている場合、Extensionによって`_corder`変数が自動的にマッピングされます。

**データタグ：** Order

**タグ付け関数：** `cmCreateOrderTag()`

**説明**：このデータタグは、登録ID、注文ID、注文小計、配送料、手数料など、最終的な注文情報を取得します。関数呼び出しは購入確認ページで送信する必要があります。1件の注文につき、Order関数は1回だけ呼び出してください。E-Commerce Extension変数の`Order ID`（`_corder`）に値が構成されると、この関数が自動的に実行されます。

### ページビュー

**Acousticデータタグ：** Page View

**タグ付け関数：** `cmCreatePageViewTag()`

**説明**：このデータタグは、訪問がサイト内を移動する際のページ情報を取得します。ページビューを測定するすべてのページで、この関数を呼び出す必要があります。

**マッピング**：マッピングツールキットを使用して、以下の宛先変数をマッピングします。

* Page ID（`pi`）- ページの英数字識別子
* Page Category（`cg`）- ページが属するカテゴリ
* Search String（`si`）- 検索結果ページの生成に使用された検索キーワード
* Search Results（`sr`）- キーワード検索で返された結果数
* `pv_a1`から`pv_a10`までのAttribute変数
* `pv1`から`pv10`までのExtra Field変数

### 商品ビュー

**データタグ：** Product View

**タグ付け関数：** `cmCreateProductViewTag()`

**説明**：このデータタグは、商品が閲覧された際の情報を取得します。関連する複数の商品の詳細表示をトラッキングするために、1つのページから複数のProduct View関数呼び出しを送信できます。

**マッピング**：マッピングツールキットを使用して、Product Virtual Category（cm_vc）とすべてのAttribute変数（`pr_a1`から`pr_a10`）をマッピングします。

E-Commerce Extensionが構成されている場合、以下が自動的にマッピングされます。

* `_cprod`からProduct ID（`pr`）- 商品の一意の識別子
* `_cprodname`からProduct Name（`pm`）- 閲覧されている商品の名前
* `_ccat`からProduct Category（`cg`）- 商品が属するカテゴリ

### カートビュー（ShopAction5）

**データタグ：** ShopAction5（Cart View）

**タグ付け関数：** `cmCreateShopAction5Tag()`

**説明**：このデータタグは、選択された商品とショッピングカート内に存在する商品に関するデータを取得します。カート内の商品ごとに関数を呼び出す必要があります（カート内に3商品ある場合は、Shop Action 5関数を3回呼び出します）。

**マッピング**：マッピングツールキットを使用して、すべてのAttribute変数（`s_a1`から`s_a10`）とExtra Field変数（`sx1`から`sx10`）をマッピングします。

E-Commerce Extensionが構成されている場合、以下が自動的にマッピングされます。

* `_cprod`からProduct ID（`pr`）- 商品の一意の識別子
* `_cprodname`からProduct Name（`pm`）- カート内で表示された商品の名前
* `_cquan`からProduct Quantity（`qt`）- カート内で表示された商品の数量
* `_cprice`からProduct Price（`bp`）- 商品の単価
* `_ccat`からProduct Category（`cg`）- 商品が属するカテゴリ

### 注文（ShopAction9）

**データタグ：** Shop Action 9（Products Ordered）

**タグ付け関数：** `cmCreateShopAction9Tag()`

**説明：** このデータタグは、訪問が購入した商品に関する情報を取得します。注文の各明細項目について、領収書ページまたは確認ページで関数を呼び出す必要があります。Tealium E-Commerce ExtensionのOrder ID変数（_corder）に値が構成されると、この関数が自動的に実行されます。

**マッピング**：マッピングツールキットを使用して、すべてのAttribute変数（`o_a1`から`o_a10`）とExtra Field変数（`or1`から`sx10`）をマッピングします。

E-Commerce Extensionが構成されている場合、以下のShopAction 9変数が自動的にマッピングされます。

* `_ccustid`からShopAction9 Registration ID（`cd`）- 一意の登録コード。この宛先に対して、E-Commerce Extensionまたはマッピングツールボックスを使用した手動構成で何もマッピングしない場合、Tealiumは`utag_main`CookieのセッションIDをこの宛先に自動的にマッピングします。
* `_corder`からShopAction9 Order Number（`on`）
* `_csubtotal`からShopAction9 Order Subtotal（`tr`）
* `_cprod`からShopAction9 Product ID（`pr`）
* `_cprodname`からShopAction9 Product Name（`pm`）
* `_cquan`からShopAction9 Quantity（`qt`）
* `_cprice`からShopAction9 Product Price（`bp`）
* `_ccat`からShopAction9 Product Category（`cg`）

また、以下のOrder変数もマッピングされます。

* `_cship`からOrder Shipping Amount（`sg`）
* `_ccity`からOrder City（`ct`）
* `_cstate`からOrder State（`sa`）
* `_czip`からOrder Zip/Postcode（`zp`）
### 登録

**データタグ:** 登録

**タグ付け関数:** `cmCreateRegistrationTag()`

**説明**: このデータタグはサイト上の登録イベントを追跡し、登録時に提供された訪問の属性情報（郵便番号、市区町村、都道府県など）とメールアドレスを収集します。E-Commerce Extensionを使用しない場合、TealiumはShopAction9 Registration IDにマッピングされた値、または`utag_main` CookieのセッションIDを使用します。

**マッピング**: マッピングツールキットを使用して、Registration Email（`em`）とすべてのExtra Field（`rg1`～`rg10`）変数をマッピングします。

E-Commerce Extensionが構成されている場合、以下が自動的にマッピングされます。

* `_ccustid`をRegistration ID（`cd`）にマッピングします。E-Commerce Extensionを使用しない場合、TealiumはShopAction9 Registration IDにマッピングされた値、または`utag_main` CookieのセッションIDを使用します。
* `_ccity`をRegistration City（`ct`）にマッピングします。
* `_cstate`をRegistration State（`sa`）にマッピングします。
* `_czip`をRegistration Zip/Postcode（`zp`）にマッピングします。
* `_ccountry`をRegistration Country（`cy`）にマッピングします。

### コンバージョンイベント

**データタグ:** コンバージョンイベント

**タグ付け関数:** `cmCreateConversionEventTag()`

**説明**: このデータタグは、コンバージョンイベントの金銭以外の詳細を収集します。トラフィック量の多いページの読み込み時にConversion Eventタグを追加すると、Server Callの料金が増加する可能性がある点に注意してください。

**マッピング**: マッピングツールキットを使用して、以下の変数をマッピングします。

* Conversion Event ID（`cid`）- コンバージョンタイプの一意の識別子
* Conversion Event Action Type（`cat`）- コンバージョンイベントの開始または正常完了
* Conversion Event Category ID（`ccid`）- Event IDのカテゴリー
* Conversion Event Points（`cpt`）- コンバージョンの価値を測定するために割り当てられたポイント
* Attribute変数`c_a1`～`c_a10`
* Extra Field変数`cx1`～`cx5`

### エレメント

**データタグ:** エレメント

**タグ付け関数**: `cmCreateElementTag`

**説明**: このデータタグは、サイト上の動的エレメントに対する訪問の操作を追跡します。動的エレメントの例には、動画、ホバー表示、エラーメッセージ、機能セレクターなどがあります。

**マッピング**: マッピングツールキットを使用して、以下の変数をマッピングします。

* Element ID（`eid`）- 追跡対象エレメントの一意の識別子
* Element Category（`ecat`）- エレメントが属するカテゴリー

Conversion Event ID（`cid`）とElement ID（`eid`）には、必ず異なるデータソースをマッピングしてください。

### 手動

このセクションは、Manual Link Click、Manual Page View、Manual Impressionという3つの異なるデータタグ関数に適用されます。

**データタグ:** Manual Link Click

**タグ付け関数**: `cmCreateManualLinkClickTag()`

**説明**: このデータタグは、自動的に追跡されないリンククリックを取得します。たとえば、以下のようなリンクが該当します。

* `HREF=""`属性がないリンク、またはクリック時にJavaScriptを使用してナビゲーションを生成するリンク。
* HTMLアンカーのないFlash、Silverlight、またはその他の対話型アプリケーションエレメント。

**マッピング**: マッピングツールキットを使用して、Manual Link Click/Page View/Impressionの宛先変数をマッピングします。

* Manual Link HREF（`hr`）- クリックされたリンクのhref値
* Manual Link Name（`nm`）- クリックされたリンクの名前
* Manual Link Page ID（`pi`）- ページを識別する一意の英数字値

**データタグ:** Manual Page View

**タグ付け関数**: `cmCreateManualPageviewTag()`

**説明**: このデータタグは、ページ読み込みイベントが発生しないページビューイベント（モーダルポップアップなど）を取得します。

* Manual Page View Destination URL（`ul`）- 遷移先URL
* Manual Page View Referring URL（`rf`）- 参照元URL

**データタグ:** Manual Impression

**タグ付け関数**: `cmCreateManualImpressionTag ()`

**説明**: このデータタグは、ディスプレイ広告タグなど、特定の機能による広告インプレッションを取得します。

* Manual Impression Page ID（`pi`）- Link Page ID（`pi`）と一致するインプレッションのPage ID
* Manual Impression Track Real Estate（`cm_re`）- 有効な`cm_re=`値を持つReal Estate Impression：`version-_-area-_-link`
* Manual Impression Track Site Promotion（`cm_sp`）- 有効な`cm_sp=`値を持つSite Promotion Impression：`group-_-promotion-_-link`

### 構成

このタブは、どのデータタグ関数にも対応していません。代わりに、テストサイト／環境に関連付けられたAcoustic Digital Analyticsタグの構成構成を動的に指定するために使用できます。

* Client ID（`ClientID`）- Acoustic Digital Analyticsによって割り当てられたID
* Test Client ID（`TestClientID`）- テストサイトのClient ID
* Test Data Collection Method（`TestDataCollectionMethod`）- テストサイトのデータ収集方式
* Test Data Collection Domain（`TestDataCollectionDomain`）- テストサイトのデータ収集ドメイン

## データマッピングリファレンス

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### ページビュー

| 変数           | 説明 |
|:---------------|:-----|
| ページID       | (`pi`)      |
| ページカテゴリー | (`cg`)      |
| 検索文字列     | (`se`)      |
| 検索結果       | (`sr`)      |
| 属性1          | (`pv_a1`)   |
| 属性2          | (`pv_a2`)   |
| 属性3          | (`pv_a3`)   |
| 属性4          | (`pv_a4`)   |
| 属性5          | (`pv_a5`)   |
| 属性6          | (`pv_a6`)   |
| 属性7          | (`pv_a7`)   |
| 属性8          | (`pv_a8`)   |
| 属性9          | (`pv_a9`)   |
| 属性10         | (`pv_a10`)  |
| 追加フィールド1  | (`pv1`)     |
| 追加フィールド2  | (`pv2`)     |
| 追加フィールド3  | (`pv3`)     |
| 追加フィールド4  | (`pv4`)     |
| 追加フィールド5  | (`pv5`)     |
| 追加フィールド6  | (`pv6`)     |
| 追加フィールド7  | (`pv7`)     |
| 追加フィールド8  | (`pv8`)     |
| 追加フィールド9  | (`pv9`)     |
| 追加フィールド10 | (`pv10`)    |

### 製品ビュー

| 変数                       | 説明 |
|:---------------------------|:-----|
| 製品ID                     | (`pr`)      |
| 製品名                     | (`pm`)      |
| 製品カテゴリー             | (`cg`)      |
| 製品仮想カテゴリー         | (`cm_vc`)   |
| 属性1                      | (`pr_a1`)   |
| 属性2                      | (`pr_a2`)   |
| 属性3                      | (`pr_a3`)   |
| 属性4                      | (`pr_a4`)   |
| 属性5                      | (`pr_a5`)   |
| 属性6                      | (`pr_a6`)   |
| 属性7                      | (`pr_a7`)   |
| 属性8                      | (`pr_a8`)   |
| 属性9                      | (`pr_a9`)   |
| 属性10                     | (`pr_a10`)  |

### カートビュー（ShopAction5）

| 変数                         | 説明 |
|:-----------------------------|:-----|
| 製品ID                       | (`pr`)      |
| 製品名                       | (`pm`)      |
| 製品数量                     | (`qt`)      |
| 製品価格                     | (`bp`)      |
| 製品カテゴリー               | (`cg`)      |
| ShopAction5属性1             | (`s_a1`)    |
| ShopAction5属性2             | (`s_a2`)    |
| ShopAction5属性3             | (`s_a3`)    |
| ShopAction5属性4             | (`s_a4`)    |
| ShopAction5属性5             | (`s_a5`)    |
| ShopAction5属性6             | (`s_a6`)    |
| ShopAction5属性7             | (`s_a7`)    |
| ShopAction5属性8             | (`s_a8`)    |
| ShopAction5属性9             | (`s_a9`)    |
| ShopAction5属性10            | (`s_a10`)   |
| ShopAction5追加フィールド1   | (`sx1`)     |
| ShopAction5追加フィールド2   | (`sx2`)     |
| ShopAction5追加フィールド3   | (`sx3`)     |
| ShopAction5追加フィールド4   | (`sx4`)     |
| ShopAction5追加フィールド5   | (`sx5`)     |
| ShopAction5追加フィールド6   | (`sx6`)     |
| ShopAction5追加フィールド7   | (`sx7`)     |
| ShopAction5追加フィールド8   | (`sx8`)     |
| ShopAction5追加フィールド9   | (`sx9`)     |
| ShopAction5追加フィールド10  | (`sx10`)    |
### 注文（ShopAction9）

| 変数                                  | 説明      |
|:--------------------------------------|:----------|
| ShopAction9 登録 ID                   | (`cd`)    |
| ShopAction9 注文番号                  | (`on`)    |
| ShopAction9 注文小計                  | (`tr`)    |
| ShopAction9 商品 ID（pr）             | [配列]    |
| ShopAction9 商品名（pm）              | [配列]    |
| ShopAction9 商品数量（qt）            | [配列]    |
| ShopAction9 商品価格（bp）            | [配列]    |
| ShopAction9 商品カテゴリ（cg）        | [配列]    |
| ShopAction9 属性 1                    | (`s_a1`)  |
| ShopAction9 属性 2                    | (`s_a2`)  |
| ShopAction9 属性 3                    | (`s_a3`)  |
| ShopAction9 属性 4                    | (`s_a4`)  |
| ShopAction9 属性 5                    | (`s_a5`)  |
| ShopAction9 属性 6                    | (`s_a6`)  |
| ShopAction9 属性 7                    | (`s_a7`)  |
| ShopAction9 属性 8                    | (`s_a8`)  |
| ShopAction9 属性 9                    | (`s_a9`)  |
| ShopAction9 属性 10                   | (`s_a10`) |
| ShopAction9 追加フィールド 1          | (`sx1`)   |
| ShopAction9 追加フィールド 2          | (`sx2`)   |
| ShopAction9 追加フィールド 3          | (`sx3`)   |
| ShopAction9 追加フィールド 4          | (`sx4`)   |
| ShopAction9 追加フィールド 5          | (`sx5`)   |
| ShopAction9 追加フィールド 6          | (`sx6`)   |
| ShopAction9 追加フィールド 7          | (`sx7`)   |
| ShopAction9 追加フィールド 8          | (`sx8`)   |
| ShopAction9 追加フィールド 9          | (`sx9`)   |
| ShopAction9 追加フィールド 10         | (`sx10`)  |
| 注文番号                              | (`on`)    |
| 注文小計                              | (`tr`)    |
| 注文配送料                            | (`sg`)    |
| 注文登録 ID                           | (`cd`)    |
| 注文の市区町村                        | (`ct`)    |
| 注文の州                              | (`sa`)    |
| 注文の郵便番号                        | (`zp`)    |
| 注文属性 1                            | (`o_a1`)  |
| 注文属性 2                            | (`o_a2`)  |
| 注文属性 3                            | (`o_a3`)  |
| 注文属性 4                            | (`o_a4`)  |
| 注文属性 5                            | (`o_a5`)  |
| 注文属性 6                            | (`o_a6`)  |
| 注文属性 7                            | (`o_a7`)  |
| 注文属性 8                            | (`o_a8`)  |
| 注文属性 9                            | (`o_a9`)  |
| 注文属性 10                           | (`o_a10`) |
| 注文追加フィールド 1                  | (`or1`)   |
| 注文追加フィールド 2                  | (`or2`)   |
| 注文追加フィールド 3                  | (`or3`)   |
| 注文追加フィールド 4                  | (`or4`)   |
| 注文追加フィールド 5                  | (`or5`)   |
| 注文追加フィールド 6                  | (`or6`)   |
| 注文追加フィールド 7                  | (`or7`)   |
| 注文追加フィールド 8                  | (`or8`)   |
| 注文追加フィールド 9                  | (`or9`)   |
| 注文追加フィールド 10                 | (`or10`)  |

### 登録

| 変数                  | 説明     |
|:----------------------|:---------|
| 登録 ID               | (`cd`)   |
| 登録メールアドレス    | (`em`)   |
| 登録の市区町村        | (`ct`)   |
| 登録の州              | (`sa`)   |
| 登録の郵便番号        | (`zp`)   |
| 登録の国              | (`cy`)   |
| 登録属性 1            | (`rg1`)  |
| 登録属性 2            | (`rg2`)  |
| 登録属性 3            | (`rg3`)  |
| 登録属性 4            | (`rg4`)  |
| 登録属性 5            | (`rg5`)  |
| 登録属性 6            | (`rg6`)  |
| 登録属性 7            | (`rg7`)  |
| 登録属性 8            | (`rg8`)  |
| 登録属性 9            | (`rg9`)  |
| 登録属性 10           | (`rg10`) |

### コンバージョンイベント

| 変数                                  | 説明      |
|:--------------------------------------|:----------|
| コンバージョンイベント ID            | (`cid`)   |
| コンバージョンイベントのアクション種別 | (`cat`)   |
| コンバージョンイベントのカテゴリ ID  | (`ccid`)  |
| コンバージョンイベントのポイント     | (`cpt`)   |
| コンバージョンイベント属性 1         | (`c_a1`)  |
| コンバージョンイベント属性 2         | (`c_a2`)  |
| コンバージョンイベント属性 3         | (`c_a3`)  |
| コンバージョンイベント属性 4         | (`c_a4`)  |
| コンバージョンイベント属性 5         | (`c_a5`)  |
| コンバージョンイベント属性 6         | (`c_a6`)  |
| コンバージョンイベント属性 7         | (`c_a7`)  |
| コンバージョンイベント属性 8         | (`c_a8`)  |
| コンバージョンイベント属性 9         | (`c_a9`)  |
| コンバージョンイベント属性 10        | (`c_a10`) |
| コンバージョンイベント追加フィールド 1 | (`cx1`)  |
| コンバージョンイベント追加フィールド 2 | (`cx2`)  |
| コンバージョンイベント追加フィールド 3 | (`cx3`)  |
| コンバージョンイベント追加フィールド 4 | (`cx4`)  |
| コンバージョンイベント追加フィールド 5 | (`cx5`)  |

#### 要素

| 変数        | 説明      |
|:------------|:----------|
| 要素 ID     | (`eid`)   |
| 要素カテゴリ | (`ecat`) |
| 要素属性 1  | (`e_a1`)  |
| 要素属性 2  | (`e_a2`)  |
| 要素属性 3  | (`e_a3`)  |
| 要素属性 4  | (`e_a4`)  |
| 要素属性 5  | (`e_a5`)  |
| 要素属性 6  | (`e_a6`)  |
| 要素属性 7  | (`e_a7`)  |
| 要素属性 8  | (`e_a8`)  |
| 要素属性 9  | (`e_a9`)  |
| 要素属性 10 | (`e_a10`) |

### 手動

| 変数                                   | 説明      |
|:---------------------------------------|:----------|
| 手動リンク HREF                       | (`hr`)    |
| 手動リンク名                          | (`nm`)    |
| 手動リンクのページ ID                 | (`pi`)    |
| 手動ページビューの遷移先 URL          | (`ul`)    |
| 手動ページビューの参照元 URL          | (`rf`)    |
| 手動インプレッションのページ ID       | (`pi`)    |
| 手動インプレッションの不動産トラッキング | (`cm_re`) |
| 手動インプレッションのサイトプロモーショントラッキング | (`cm_sp`) |

### エラー

| 変数           | 説明   |
|:---------------|:-------|
| ページ ID      | (`pi`) |
| エラーカテゴリ | (`cg`) |

### イベント

| 変数                     | 説明                 |
|:-------------------------|:---------------------|
| 登録                     | 登録                 |
| 注文                     | 注文                 |
| カート／ShopAction5      | ShopAction5          |
| 商品ビュー               | 商品ビュー           |
| コンバージョンイベント   | コンバージョン       |
| 要素                     | 要素                 |
| エラー                   | エラー               |

### 構成

| 変数                                      | 説明                         |
|:------------------------------------------|:-----------------------------|
| クライアント ID                           | (`ClientID`)                 |
| テスト用クライアント ID                   | (`TestClientID`)             |
| テスト用データ収集方法                    | (`TestDataCollectionMethod`) |
| テスト用データ収集ドメイン                | (`TestDataCollectionDomain`) |
| 詳細構成オブジェクト（`cmSetupOther`）    | [オブジェクト]               |