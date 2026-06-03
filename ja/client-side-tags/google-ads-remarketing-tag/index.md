---
title: Google Ads リマーケティングタグ構成ガイド
description: この記事では、Tealium iQ タグ管理で Google Ads リマーケティングタグを構成する方法と、Chrome Google タグアシスタント拡張機能を使用してカスタムパラメータがキャプチャされているかどうかを確認する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/google-ads-remarketing-tag/
---
## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグの追加方法については、[タグ概要]()の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **コンバージョンID**
  * `google_conversion_id` の値を入力します。
  * この値はコードスニペットに記載されており、広告コントロールパネルでも確認できます。
* **ページタイプ**
  * このタグインスタンスでコンバージョンを追跡しているサイトのページタイプを選択します。
  * これはコードスニペットのカスタム `ecomm_pagetype` パラメータの値でもあります。
* **コンバージョン値**
  * コンバージョンアクションに割り当てたい値を入力します。
  * このフィールドは空白のままにするか、注文小計の値を使用するか、データマッピングツールボックスを介して動的に構成することができます。

上記の構成はすべてデータマッピングツールボックスで構成することもできます。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール]()のドキュメントを参照してください。

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

### 標準

タグ構成の下で値を動的に送信（または上書き）するためにこれらの宛先にマップします。

以下の表は、標準変数の宛先名と説明を示しています。

|宛先名| 説明|
|---| ---|
| コンバージョンID `google_conversion_id` |  &lt;ul&gt;&lt;li&gt;`google_conversion_id` パラメータの値。&lt;/li&gt;&lt;/ul&gt; |
|コンバージョンラベル|  &lt;ul&gt;&lt;li&gt;ここにデフォルトラベルを構成し、マッピングを使用してこの値を動的に上書きします。&lt;/li&gt;&lt;li&gt;複数のラベルのデータを送信するためにカンマ区切りリストを使用します。&lt;/li&gt;&lt;li&gt;このリストは、コンバージョンIDの数に合わせて複数のコンバージョンラベルを使用するか、すべてのコンバージョンIDに対して単一のラベルを使用することができます。&lt;/li&gt;&lt;/ul&gt; |
|コンバージョン値 (value)|  &lt;ul&gt;&lt;li&gt;ここにデフォルト値を構成するか、E-Commerce拡張機能からの小計値を使用するためにこのフィールドを空白にします。&lt;/li&gt;&lt;li&gt;マッピングを使用してこの値とE-Commerce拡張機能の値を動的に上書きします。&lt;/li&gt;&lt;li&gt;コンバージョントラッキングを使用する場合、特定のタイプのすべてのコンバージョンアクションに同じ値を割り当てることができます（静的値）または、コンバージョンアクションごとに異なる値を持たせることができます（動的、トランザクション固有の値を表します）。&lt;/li&gt;&lt;li&gt;コンバージョンに値を割り当てると、異なるコンバージョンによってもたらされる広告の総価値を区別し、高価値のコンバージョンを特定して重点を置くことができます。&lt;/li&gt;&lt;li&gt;このフィールドを空白にすると、タグはE-commerceの小計値 (`_csubtotal`) を使用して自動的に入力されます。&lt;/li&gt;&lt;/ul&gt; |
|グローバルオブジェクト|  &lt;ul&gt;&lt;li&gt;イベントキューに使用されるグローバルオブジェクトの名前。&lt;/li&gt;&lt;li&gt;指定されていない場合は「gtag」が使用されます。&lt;/li&gt;&lt;li&gt;ほとんどの実装では必要ありません。&lt;/li&gt;&lt;/ul&gt; |
|データレイヤー名|  &lt;ul&gt;&lt;li&gt;デフォルトでは、グローバルサイトタグによって初期化および参照されるデータレイヤーは **dataLayer** という名前です。&lt;/li&gt;&lt;li&gt;プロジェクトが別の名前を必要とする場合のみ、データレイヤーの名前を変更します。&lt;/li&gt;&lt;/ul&gt; |
|リマーケティングを有効にする|  &lt;ul&gt;&lt;li&gt;値は **On** または **Off** です。&lt;/li&gt;&lt;li&gt;デフォルト値は **Off** です。&lt;/li&gt;&lt;li&gt;リマーケティングが有効になっている場合、このタグは自動的にE-Commerce拡張機能からデータを引き込み、Google Adsの「Retail」パラメータ（接頭辞 `ecomm_`）を入力します。&lt;/li&gt;&lt;li&gt;「Retail」タブに直接マッピングすると、E-Commerce拡張機能を介して引き込まれたデータが上書きされます。&lt;/li&gt;&lt;/ul&gt; |
|ページタイプ `pagetype` |  &lt;ul&gt;&lt;li&gt;コンバージョンを追跡しているページのタイプ。&lt;/li&gt;&lt;li&gt;ここでデフォルトのページタイプを選択し、マッピングを使用してこの値を動的に上書きします。&lt;/li&gt;&lt;/ul&gt; |
|クロストラッキングドメイン|  &lt;ul&gt;&lt;li&gt;クロスドメイントラッキングに使用するドメインのカンマ区切りリスト（setAllowLinkerを構成）。&lt;/li&gt;&lt;li&gt;トップレベルドメイン、例えば「tealiumiq.com」などが該当します。&lt;/li&gt;&lt;/ul&gt; |
|カスタム|  &lt;ul&gt;&lt;li&gt;Google Adsによって事前に定義されていないカスタマイズされたパラメータを定義することができます。&lt;/li&gt;&lt;li&gt;詳細については以下の「Advanced」を参照してください。&lt;/li&gt;&lt;/ul&gt; |

### 小売

このタグには、[E-Commerce拡張機能]()の構成をお勧めします。これにより、必要な製品および注文の詳細が適切な広告パラメータに自動的に送信されます。また、マッピングを使用して拡張機能の変数を上書きすることもできます。

以下の表は、小売変数の宛先名と説明を示しています。

|宛先名| 説明|
|---| ---|
|`ecomm.prodid`|  &lt;ul&gt;&lt;li&gt;（必須）これは現在のページに表示されている製品の製品IDまたは製品IDです。ここで使用されるIDはフィード内のIDと一致する必要があります。&lt;/li&gt;&lt;li&gt;E-commerce拡張機能を使用する場合、このパラメータのマッピングは `_cprod` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`ecomm.totalvalue`|  &lt;ul&gt;&lt;li&gt;このパラメータは製品ページ、カートページ、購入ページのタイプで使用され、単一の製品の値を製品ページで、またはカートおよび購入ページで1つ以上の製品の値の合計を含む必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`ecomm.category`|  &lt;ul&gt;&lt;li&gt;このパラメータは、現在表示されている製品またはカテゴリページのカテゴリを含みます。&lt;/li&gt;&lt;li&gt;E-commerce拡張機能を使用する場合、このパラメータは `_ccat` を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`ecomm.pagetype`|  &lt;ul&gt;&lt;li&gt;推奨。&lt;/li&gt;&lt;li&gt;タグが配置されているページのタイプを示します。&lt;/li&gt;&lt;li&gt;次の値のいずれかを使用します：&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`category`&lt;/li&gt;&lt;li&gt;`product`&lt;/li&gt;&lt;li&gt;`cart`&lt;/li&gt;&lt;li&gt;`purchase`&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;`other` ページタイプに当てはまらない場合に使用します。例えば、「Contact Us」や「About Us」ページなどです。&lt;/li&gt;&lt;/ul&gt; &lt;li&gt;このパラメータを含める場合は、データソースを `ecomm.pagetype` にマップします。&lt;/li&gt;&lt;/ul&gt; |
|`ecomm.value`|  &lt;ul&gt;&lt;li&gt;非推奨。&lt;/li&gt;&lt;li&gt;このパラメータはGoogle Adsによってこのリマーケティングタグではもはや使用されていません。&lt;/li&gt;&lt;/ul&gt; |
|`ecomm.quantity`|  &lt;ul&gt;&lt;li&gt;非推奨。&lt;/li&gt;&lt;li&gt;このパラメータはGoogle Adsによってこのリマーケティングタグではもはや使用されていません。&lt;/li&gt;&lt;/ul&gt; |
|`Custom`|  &lt;ul&gt;&lt;li&gt;Google Adsによって事前に定義されていないカスタマイズされたパラメータを定義することができます。&lt;/li&gt;&lt;li&gt;詳細については以下の「Advanced」を参照してください。&lt;/li&gt;&lt;/ul&gt; |

### 教育

以下の表は、教育変数の宛先名と説明を示しています。

|宛先名| 説明|
|---| ---|
|`edu.pid`|  &lt;ul&gt;&lt;li&gt;（必須）このパラメータは、訪問が現在プログラムページまたはリードページタイプで表示しているプログラムのIDです。&lt;/li&gt;&lt;li&gt;このIDはフィード内の「教育プログラム」の値と一致する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`edu.plocid`|  &lt;ul&gt;&lt;li&gt;このパラメータは、ユーザーが現在プログラムページまたはリードページタイプで表示しているプログラムの場所のIDです。&lt;/li&gt;&lt;li&gt;このIDはフィード内の「ロケーションID」の値と一致する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`edu.pagetype`|  &lt;ul&gt;&lt;li&gt;推奨。&lt;/li&gt;&lt;li&gt;タグが配置されているページのタイプを示します。&lt;/li&gt;&lt;li&gt;次の値のいずれかを使用します：&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`program`&lt;/li&gt;&lt;li&gt;`lead`&lt;/li&gt;&lt;li&gt;`complete` または&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;`other` ページタイプに当てはまらない場合に使用します。例えば、「Contact Us」や「About Us」ページなどです。&lt;/li&gt;&lt;/ul&gt; &lt;li&gt;このパラメータを含める場合は、データソースを `edu.pagetype` にマップします。&lt;/li&gt;&lt;/ul&gt; |


### フライト

以下の表は、フライト変数の目的地名と説明を示しています。

|目的地名| 説明|
|---| ---|
|`flight.originid`|  &lt;ul&gt;&lt;li&gt;このパラメーターは、検索結果、カート、購入ページタイプで表示されるフライト行程の出発地です。&lt;/li&gt;&lt;li&gt;このIDはフィード内の値と一致する必要がありますが、Googleは3文字の空港コードの使用を推奨しています。&lt;/li&gt;&lt;/ul&gt; |
|`flight.destid`|  &lt;ul&gt;&lt;li&gt;（必須）このパラメーターは、検索結果、カート、購入ページタイプで表示されるフライト行程の目的地です。&lt;/li&gt;&lt;li&gt;このIDはフィード内の値と一致する必要がありますが、Googleは3文字の空港コードの使用を推奨しています。&lt;/li&gt;&lt;/ul&gt; |
|`flight.totalvalue`|  &lt;ul&gt;&lt;li&gt;このパラメーターはカートおよび購入ページタイプで使用され、フライト行程の総価値を含むべきです。&lt;/li&gt;&lt;li&gt;通貨記号は含めないでください。&lt;/li&gt;&lt;/ul&gt; |
|`flight.startdate`|  &lt;ul&gt;&lt;li&gt;フライト行程が始まる日付です。&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`形式であるべきです。&lt;/li&gt;&lt;/ul&gt; |
|`flight.enddate`|  &lt;ul&gt;&lt;li&gt;フライト行程が終わる日付です。&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`形式であるべきです。&lt;/li&gt;&lt;/ul&gt; |
|`flight.pagetype`|  &lt;ul&gt;&lt;li&gt;推奨されます。&lt;/li&gt;&lt;li&gt;タグが存在するページのタイプを示します。&lt;/li&gt;&lt;li&gt;以下の値のいずれかを使用してください：&lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`offerdetail`&lt;/li&gt;&lt;li&gt;`cart`&lt;/li&gt;&lt;li&gt;`purchase`&lt;/li&gt;&lt;li&gt;`cancel` または&lt;/li&gt;&lt;li&gt;`other` 上記にリストされていないページタイプに当てはまらない場合に使用します。例えば、「お問い合わせ」や「会社概要」ページなどです。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;このパラメーターを含める場合は、データソースを `flight.pagetype` にマッピングしてください。&lt;/li&gt;&lt;/ul&gt; |

### ホテルとレンタル

以下の表は、ホテルおよびレンタル変数の目的地名と説明を示しています。

|目的地名| 説明|
|---| ---|
|`hrental.id`|  &lt;ul&gt;&lt;li&gt;（必須）このパラメーターは、訪問が現在プロパティページタイプで閲覧しているホテルまたはレンタル物件のIDです。&lt;/li&gt;&lt;li&gt;このIDはフィード内の値と一致する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`hrental.startdate`|  &lt;ul&gt;&lt;li&gt;予約が開始される日付です。&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`形式であるべきです。&lt;/li&gt;&lt;/ul&gt; |
|`hrental.enddate`|  &lt;ul&gt;&lt;li&gt;予約が終了する日付です。&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`形式であるべきです。&lt;/li&gt;&lt;/ul&gt; |
|`hrental.totalvalue`|  &lt;ul&gt;&lt;li&gt;このパラメーターは、転換意図および転換ページタイプで使用され、訪問のカート内のすべての物件の総合計値を含むべきです。&lt;/li&gt;&lt;li&gt;通貨記号は含めないでください。&lt;/li&gt;&lt;/ul&gt; |
|`hrental.pagetype`|  &lt;ul&gt;&lt;li&gt;推奨されます。&lt;/li&gt;&lt;li&gt;タグが存在するページのタイプを示します。&lt;/li&gt;&lt;li&gt;以下の値のいずれかを使用してください：&lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`offerdetail`&lt;/li&gt;&lt;li&gt;`conversionintent`&lt;/li&gt;&lt;li&gt;`conversion` または&lt;/li&gt;&lt;li&gt;`other` 上記にリストされていないページタイプに当てはまらない場合に使用します。例えば、「お問い合わせ」や「会社概要」ページなどです。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;このパラメーターを含める場合は、データソースを `hrental.pagetype.` にマッピングしてください。&lt;/li&gt;&lt;/ul&gt; |

### ジョブ

以下の表は、ジョブ変数の目的地名と説明を示しています。

|目的地名| 説明|
|---| ---|
|`job.id`|  &lt;ul&gt;&lt;li&gt;（必須）このパラメーターは、`searchresults`, `offerdetail`, `conversionintent` および `conversion` ページタイプで表示される求人のIDです。&lt;/li&gt;&lt;li&gt;このIDはフィード内の値と一致する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`job.locid`|  &lt;ul&gt;&lt;li&gt;このパラメーターは、場所のIDまたは名前を表し、フィードで複数の job\_ids を同じ値で使用するが、異なる場所IDを使用して二次的なマッチングキーとして機能し、検索結果、オファー詳細、転換意図および転換ページタイプで存在すべきです。&lt;/li&gt;&lt;/ul&gt; |
|`job.totalvalue`|  &lt;ul&gt;&lt;li&gt;このパラメーターは、転換意図および転換ページタイプで使用され、ユーザーが選択した求人リストの総価値を含むべきです。&lt;/li&gt;&lt;li&gt;通貨記号は含めないでください。&lt;/li&gt;&lt;/ul&gt; |
|`job.pagetype`|  &lt;ul&gt;&lt;li&gt;推奨されます。&lt;/li&gt;&lt;li&gt;タグが存在するページのタイプを示します。&lt;/li&gt;&lt;li&gt;以下の値のいずれかを使用してください：&lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`offerdetail`&lt;/li&gt;&lt;li&gt;`conversionintent` または&lt;/li&gt;&lt;li&gt;`other` 上記にリストされていないページタイプに当てはまらない場合に使用します。例えば、「お問い合わせ」や「会社概要」ページなどです。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;このパラメーターを含める場合は、データソースを `job.pagetype.` にマッピングしてください。&lt;/li&gt;&lt;/ul&gt; |

### ローカル

以下の表は、ローカル変数の目的地名と説明を示しています。

|目的地名| 説明|
|---| ---|
|`local.id`|  &lt;ul&gt;&lt;li&gt;（必須）このパラメーターは、検索結果、オファー詳細、転換意図および転換ページタイプで表示されるオファーまたはディールのIDです。&lt;/li&gt;&lt;li&gt;このIDはフィード内の値と一致する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`local.totalvalue`|  &lt;ul&gt;&lt;li&gt;このパラメーターは、転換意図および転換ページタイプで使用され、ユーザーが購入したオファーまたはオファーの総価値を含むべきです。&lt;/li&gt;&lt;li&gt;通貨記号は含めないでください。&lt;/li&gt;&lt;/ul&gt; |
|`local.pagetype`|  &lt;ul&gt;&lt;li&gt;推奨されます。&lt;/li&gt;&lt;li&gt;タグが存在するページのタイプを示します。&lt;/li&gt;&lt;li&gt;以下の値のいずれかを使用してください：&lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`offerdetail`&lt;/li&gt;&lt;li&gt;`conversionintent`&lt;/li&gt;&lt;li&gt;`conversion` または&lt;/li&gt;&lt;li&gt;`other` 上記にリストされていないページタイプに当てはまらない場合に使用します。例えば、「お問い合わせ」や「会社概要」ページなどです。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;このパラメーターを含める場合は、データソースを `local.pagetype` にマッピングしてください。&lt;/li&gt;&lt;/ul&gt; |

### 不動産

以下の表は、不動産変数の目的地名と説明を示しています。

|目的地名| 説明|
|---| ---|
|`listing.id`|  &lt;ul&gt;&lt;li&gt;（必須）このパラメーターは、検索結果、オファー詳細、転換意図および転換ページタイプで表示される物件のIDです。&lt;/li&gt;&lt;li&gt;このIDはフィード内の値と一致する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`listing.totalvalue`|  &lt;ul&gt;&lt;li&gt;このパラメーターは、転換意図および転換ページタイプで使用され、物件の総価値を含むべきです。&lt;/li&gt;&lt;li&gt;通貨記号は含めないでください。&lt;/li&gt;&lt;/ul&gt; |
|`listing.pagetype`|  &lt;ul&gt;&lt;li&gt;推奨されます。&lt;/li&gt;&lt;li&gt;タグが存在するページのタイプを示します。&lt;/li&gt;&lt;li&gt;以下の値のいずれかを使用してください：&lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`offerdetail`&lt;/li&gt;&lt;li&gt;`conversionintent`&lt;/li&gt;&lt;li&gt;`conversion` または&lt;/li&gt;&lt;li&gt;`other` 上記にリストされていないページタイプに当てはまらない場合に使用します。例えば、「お問い合わせ」や「会社概要」ページなどです。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;このパラメーターを含める場合は、データソースを `listing.pagetype` にマッピングしてください。&lt;/li&gt;&lt;/ul&gt; |
### 旅行

以下の表は、旅行変数の目的地名と説明を示しています。

|目的地名| 説明|
|---| ---|
|`travel.destid`|  &lt;ul&gt;&lt;li&gt;(必須) 検索結果、転換意図、転換ページタイプで表示される旅行先のIDです。&lt;/li&gt;&lt;li&gt;このIDはフィード内の値と一致する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`travel.originid`|  &lt;ul&gt;&lt;li&gt;(オプション) 検索結果、転換意図、転換ページタイプで表示される出発地のIDです。&lt;/li&gt;&lt;li&gt;この値はフィードで二次的なマッチングキーとして使用され、何を表す必要はありませんが、Googleは3文字の空港コードまたは2文字の国コードの使用を推奨しています。&lt;/li&gt;&lt;/ul&gt; |
|`travel.startdate`|  &lt;ul&gt;&lt;li&gt;旅行の日程が始まる日付です。&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`形式である必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`travel.enddate`|  &lt;ul&gt;&lt;li&gt;旅行の日程が終わる日付です。&lt;/li&gt;&lt;li&gt;`YYYY-MM-DD`形式である必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`travel.totalvalue`|  &lt;ul&gt;&lt;li&gt;このパラメーターは転換意図と転換ページタイプで使用され、旅行の日程の総価値を含む必要があります。&lt;/li&gt;&lt;li&gt;通貨記号は含めないでください。&lt;/li&gt;&lt;/ul&gt; |
|`travel.pagetype`|  &lt;ul&gt;&lt;li&gt;推奨。&lt;/li&gt;&lt;li&gt;タグが存在するページのタイプを示します。&lt;/li&gt;&lt;li&gt;以下の値のいずれかを使用してください：&lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`offerdetail`&lt;/li&gt;&lt;li&gt;`conversionintent`&lt;/li&gt;&lt;li&gt;`conversion`&lt;/li&gt;&lt;li&gt;`cancel`&lt;/li&gt;&lt;li&gt;`other` 上記にリストされていないページタイプの場合に使用します。例えば、「Contact Us」や「About Us」ページなど。&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;このパラメーターを含める場合は、データソースを`travel.pagetype`にマッピングしてください。&lt;/li&gt;&lt;/ul&gt; |

### 電話転換オプション

ウェブサイトからの電話呼び出しを効果的にリードする広告の効果を見るために、電話呼び出し転換トラッキングを使用します。誰かが広告をクリックした後にあなたのウェブサイトを訪れた場合、ウェブサイトの呼び出し転換トラッキングはあなたのサイトからの呼び出しを識別し、測定するのに役立ちます。この種の転換トラッキングは、構成した最小の長さよりも長く続く呼び出しを転換としてトラックします。

以下の表は、電話転換オプション変数の目的地名と説明を示しています。

|目的地名| 説明|
|---| ---|
|`phone_conversion_number`|  &lt;ul&gt;&lt;li&gt;(必須) 次の例では、「REPLACE WITH VALUE」をあなたのビジネスの電話番号に置き換えてください。&lt;/li&gt;&lt;li&gt;番号はページ上の番号と正確に一致し、関連する国コードを含む必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`phone_conversion_css_class`|  &lt;ul&gt;&lt;li&gt;(必須) CSSクラス名を入力してください。&lt;/li&gt;&lt;li&gt;そのクラスのすべての要素は、整形された電話番号で内容が置き換えられます。&lt;/li&gt;&lt;/ul&gt; |

### その他

以下の表は、「その他」カテゴリに分類される変数の目的地名と説明を示しています。

|目的地名| 説明|
|---| ---|
|`dynx.itemid`|  &lt;ul&gt;&lt;li&gt;(必須) 検索結果、オファー詳細、転換意図、転換ページタイプで表示される製品のIDです。&lt;/li&gt;&lt;li&gt;このIDはフィード内の値と一致する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`dynx.itemid2`|  &lt;ul&gt;&lt;li&gt;(オプション) 検索結果、オファー詳細、転換意図、転換ページタイプで表示される製品の二次IDです。&lt;/li&gt;&lt;li&gt;このIDはフィード内の値と一致する必要があります。&lt;/li&gt;&lt;/ul&gt; |
|`dynx.totalvalue`|  &lt;ul&gt;&lt;li&gt;このパラメーターは転換意図ページタイプで使用され、訪問が購入した製品の総価値を含む必要があります。&lt;/li&gt;&lt;li&gt;通貨記号は含めないでください。&lt;/li&gt;&lt;/ul&gt; |
|`dynx.pagetype`|  &lt;ul&gt;&lt;li&gt;推奨。&lt;/li&gt;&lt;li&gt;タグが存在するページのタイプを示します。以下の値のいずれかを使用してください：&lt;/li&gt; &lt;ul&gt;&lt;li&gt;`home`&lt;/li&gt;&lt;li&gt;`searchresults`&lt;/li&gt;&lt;li&gt;`offerdetail`&lt;/li&gt;&lt;li&gt;`conversionintent`&lt;/li&gt;&lt;li&gt;`conversion`&lt;/li&gt;&lt;li&gt;`cancel`&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;`other` 上記にリストされていないページタイプの場合に使用します。例えば、「Contact Us」や「About Us」ページなど。&lt;/li&gt;&lt;/ul&gt; &lt;li&gt;このパラメーターを含める場合は、データソースを`dynx.pagetype`にマッピングしてください。&lt;/li&gt;&lt;/ul&gt; |

### 高度な構成

以下の表は、高度な変数の目的地名と説明を示しています。

|目的地名| 説明|
|---| ---|
|推奨される製品ID `custom.ecomm_rec_prodid`|  &lt;ul&gt;&lt;li&gt;このパラメーターは、ページ上の推奨製品の製品IDを渡すために使用することができます。&lt;/li&gt;&lt;/ul&gt; |
|訪問の年齢 `custom.a`|  &lt;ul&gt;&lt;li&gt;このパラメーターは、訪問の年齢を渡すために使用することができます。&lt;/li&gt;&lt;/ul&gt; |
|訪問の性別 `custom.g`|  &lt;ul&gt;&lt;li&gt;このパラメーターは、訪問の性別を渡すために使用することができます。&lt;/li&gt;&lt;/ul&gt; |
|訪問がアカウントを持っているか `custom.hasaccount`|  &lt;ul&gt;&lt;li&gt;このパラメーターは、訪問がアカウントを持っているかどうかを示すために使用することができます。&lt;/li&gt;&lt;/ul&gt; |
|顧客品質スコア `custom.cqs`|  &lt;ul&gt;&lt;li&gt;このパラメーターは、訪問の顧客品質スコアを報告するために使用することができます。&lt;/li&gt;&lt;/ul&gt; |
|リピート購入者 `custom.rp`|  &lt;ul&gt;&lt;li&gt;このパラメーターは、訪問がリピート購入者であるかどうかを識別するために使用することができます。&lt;/li&gt;&lt;/ul&gt; |
|訪問のロイヤルティスコア `custom.ly` |  &lt;ul&gt;&lt;li&gt;このパラメーターは、訪問のロイヤルティスコアを識別するために使用されます。&lt;/li&gt;&lt;/ul&gt; |
|訪問のハイスペンダースコア `custom.hs`|  &lt;ul&gt;&lt;li&gt;このパラメーターは、訪問のハイスペンダースコアを識別するために使用されます。&lt;/li&gt;&lt;/ul&gt; |
|カスタム `custom.myvar`|  &lt;ul&gt;&lt;li&gt;このパラメーターは、任意のカスタマイズされたパラメーターを渡すために使用することができます。&lt;/li&gt;&lt;li&gt;`myvar`をあなた自身のパラメーター名に置き換えてください。&lt;/li&gt;&lt;/ul&gt; |

### Eコマース

このタグは自動的にEコマース拡張機能からデータを引き出し、以下の小売パラメーターを埋めます：

* `_cprod`からの`ecomm.prodid`
* `_ccat`からの`ecomm.category`
* `_csubtotal`からの`ecomm.totalvalue`（`_corder`が存在する場合やページタイプに`purchase`、`conversion`、`cart`、または`conversionintent`が含まれる場合）

以下の表は、Eコマース変数の目的地名と説明を示しています。

|目的地名| 説明|
|---| ---|
|注文ID `_corder`|  &lt;ul&gt;&lt;li&gt;最終注文に割り当てられた一意の識別子を表します。&lt;/li&gt;&lt;li&gt;Eコマースパラメーターを使用する利点の一つは、タグが自動的に任意のビジネスタイプに対して`_csubtotal`を総価値として使用することです。&lt;/li&gt;&lt;li&gt;例えば、小売ビジネスタイプの場合、`ecomm.totalvalue`の値は`_csubtotal`を使用します。&lt;/li&gt;&lt;/ul&gt; |
|小計 (`_csubtotal`)|  &lt;ul&gt;&lt;li&gt;最終注文の小計額を表します。&lt;/li&gt;&lt;li&gt;`_csubtotal`内の値は、報告されるビジネスタイプに関係なく自動的に総価値として`_csubtotal`を使用します。&lt;/li&gt;&lt;li&gt;例えば、小売ビジネスタイプの場合、`ecomm.totalvalue`の値は`_csubtotal`を使用します。&lt;/li&gt;&lt;/ul&gt; |
|製品IDリスト `_cprod`|  &lt;ul&gt;&lt;li&gt;製品配列内の各製品の一意の識別子を表します。&lt;/li&gt;&lt;li&gt;存在する場合、カスタムパラメーターecomm.prodidは`_cprod`の内容を含みます。&lt;/li&gt;&lt;/ul&gt; |
|カテゴリリスト `_ccat`|  &lt;ul&gt;&lt;li&gt;製品配列内の各製品のカテゴリを表します。&lt;/li&gt;&lt;li&gt;存在する場合、カスタムパラメーターecomm.categoryは`_ccat`の内容を含みます。&lt;/li&gt;&lt;/ul&gt; |
|数量リスト `_cquan`|  &lt;ul&gt;&lt;li&gt;製品配列内の各製品の数量を表します。&lt;/li&gt;&lt;li&gt;存在する場合、カスタムパラメーターecomm.quantityは`_cquan`の内容を含みます。&lt;/li&gt;&lt;/ul&gt; |
|価格リスト `_cprice`|  &lt;ul&gt;&lt;li&gt;製品配列内の各製品の単位価格を表します。&lt;/li&gt;&lt;li&gt;存在する場合、カスタムパラメーターecomm.pvalueは`_cprice`の内容を含みます。&lt;/li&gt;&lt;/ul&gt; |
|通貨 `_ccurrency`|  &lt;ul&gt;&lt;li&gt;製品配列の価格の通貨を表します。&lt;/li&gt;&lt;li&gt;存在する場合、カスタムパラメーターecomm.currencyは`_ccurrency`の内容を含みます。&lt;/li&gt;&lt;/ul&gt; |
|割引リスト `product_discount`|  &lt;ul&gt;&lt;li&gt;製品配列内の各製品の単位割引を表します。&lt;/li&gt;&lt;li&gt;存在する場合、カスタムパラメーターecomm.discountは`_cdisc`の内容を含みます。&lt;/li&gt;&lt;/ul&gt; |
## タグの確認

[Google Tag Assistant](https://support.google.com/tagassistant/answer/2947093?hl=en&amp;ref_topic=6000196)を使用するには、Chrome Webブラウザが必要です。ブラウザがすでにコンピュータにインストールされている場合は、[Google Chrome Store](https://chrome.google.com/webstore/detail/tag-assistant-by-google/kejbdjndbnbjgmefkgdddjlbokphdefk)からGoogle Tag Assistantをインストールしてください。正常にインストールされたら、以下の手順に従ってください：

1. サイトにアクセスし、対象ページを開きます。
1. ブラウザの右上隅にあるアシスタントアイコンをクリックします。
1. **このページを今すぐチェック**をクリックします。  
![](/images/client-side-tags/test-page.png)
アイコンの色指標が緑ではなく赤に表示される場合がありますが、これはTealiumを通じてタグを実装しているためです。
Tag Assistantが実行されると、値が表示されるようになります。以下のサンプルユースケースでは、ホームページのテストを示しています。例では、リクエストが「動作中」であり、データソースが取得されていることに注意してください。また、`ecomm_pagetype`は`home`の値で入力されていますが、`ecomm_value`と`ecomm_prodid`はホームページにそれらの値が含まれていないため、入力されていません。  
![](/images/client-side-tags/home-page.png)次の例は、製品詳細ページでのTag Assistantの様子を示しています。  
![](/images/client-side-tags/product-detail.png)

## ベンダー文書

追加情報については、以下のベンダー文書を参照してください：

* [Google広告ヘルプ](https://support.google.com/adwords#topic=3119071)
* [ダイナミックリターゲティングのためのサイトタグ付け](https://support.google.com/adwords/answer/3103357)
* [コンバージョン値について](https://support.google.com/adwords/answer/3419241?hl=en)
* [ダイナミックリマーケティングパラメータ](https://developers.google.com/adwords-remarketing-tag/parameters)

