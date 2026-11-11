---
title: Snowplowタグ構成ガイド
description: この記事では、タグ管理アカウントでSnowplowタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/snowplow-tag/
---
## タグに関するヒント

* Eコマース拡張機能をサポート
* マッピングを使用して、以下を実行できます。
  * 標準構成値を動的に上書きする
  * Eコマース拡張機能の値を動的に上書きする
  * 構造化イベントトラッキングをトリガーする
  * 非構造化イベントトラッキングをトリガーする

* 構造化／非構造化イベントのアクションがマッピングで定義されている場合、構造化／非構造化イベントトラッキングがトリガーされます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を行います。

* **コードバージョン**
  * タグのバージョン（**2.18.2**、**3.1.2**、または**3.23.0**）を選択します。

* **タイトル**
  * 同じベンダーのタグを複数使用する場合は、一意の名前を割り当てます。

* **Snowplowオブジェクト（必須）**
  * グローバルSnowplowオブジェクトの一意の名前。
  * Snowplowオブジェクト名は`window.snowplow.name`として定義されます。

* **SnowplowベースURL（必須）**
  * バージョンを含むSnowplowトラッカーを表すURL。
  * 形式の例：`//d1fc8wv8zag5ca.cloudfront.net/x.xx.x/sp.js`

* **トラッカー名前空間（必須）**
  * Snowplowトラッカーの名前空間。
  * データマッピングを使用して、この値を動的に上書きします。

* **トラッカーエンドポイント（必須）**
  * SnowplowトラッカーのコレクターエンドポイントURI。
  * データマッピングを使用して、この値を動的に上書きします。

* **Cookieドメイン**
  * Cookieを構成するトップレベルドメイン。
  * 例：`.mysite.com`
  * データマッピングを使用して、この値を動的に上書きします。

* **リンクトラッキングを有効化**
  * リンクのクリックにイベントリスナーを追加します。
  * 指定可能な値は`True`または`False`です。
  * データマッピングを使用して、この値を動的に上書きします。

* **アクティビティトラッキングを有効化**
  * ページ上のユーザーアクティビティを追跡するために、「ページping」イベントを有効にします。
  * 指定可能な値は`True`または`False`です。
  * データマッピングを使用して、この値を動的に上書きします。

* **エラートラッキングを有効化**
  * JavaScriptコード内の未処理の例外を追跡します。
  * 指定可能な値は`True`または`False`です。
  * データマッピングを使用して、この値を動的に上書きします。

* **ページビューの保持を有効化**
  * HTMLページ全体が読み込まれたときにのみ、Webページのコンテキストを再生成します。
  * 指定可能な値は`True`または`False`です。
  * データマッピングを使用して、この値を動的に上書きします。

* **公開先**
  * タグは、選択した公開先（`Dev`、`QA`、`Prod`、または`Custom`）にのみ公開されます。

* **詳細構成**
  * このタグと組織内での使用方法に関する説明メモ。

## ロードルール

[ロードルール](https://docs.tealium.com/about-load-rules/)では、サイト上でこのタグのインスタンスをいつ、どこに読み込むかを決定します。

推奨ロードルール：**すべてのページ**

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

Snowplowタグの宛先変数は、**データマッピング**タブに組み込まれています。利用可能なカテゴリーは以下のとおりです。

### 標準

|**宛先名**| **説明**|
|---| ---|
| `customURL` |  <ul><li>カスタムURL</li><li>ページのカスタムURLを構成します。</li></ul> |
| `referrerURL` |  <ul><li>カスタム参照元URL。</li><li>参照元のカスタムURLを構成します。</li></ul> |
| `pageTitle` |  <ul><li>ページタイトル</li><li>ページのタイトルを構成します。</li></ul> |
| `cookieTimeOut` |  <ul><li>Cookieタイムアウト</li><li>セッションCookieをアクティブに保つ時間を秒単位で構成します。</li><li>デフォルトは30分（1800秒）です。</li></ul> |
| `enableAT` |  <ul><li>アクティビティトラッキングを有効化</li><li>ページ上のユーザーアクティビティを追跡するために、`page ping`イベントを有効にします。</li><li>値のオプション：`true`または`false`</li></ul> |
| `minimumVisitLength` |  <ul><li>最小訪問時間</li><li>ページの読み込みから最初のページpingまでの時間を秒単位で構成します。</li></ul> |
| `heartBeat` |  <ul><li>ハートビート</li><li>ページping間の時間を秒単位で構成します。</li></ul> |
| `enableET` |  <ul><li>エラートラッキングを有効化</li><li>JavaScriptコード内の未処理の例外を追跡します。</li><li>値のオプション：`true`または`false`</li></ul> |
| `preservePageView` |  <ul><li>ページビューを保持</li><li>HTMLページ全体が読み込まれたときにのみ、Webページのコンテキストを再生成します。</li><li>値のオプション：`true`または`false`</li></ul> |
### トラッカー

|**宛先名**| **説明**|
|---| ---|
| `trk_namespace` |  <ul><li>トラッカーの名前空間</li><li>Snowplow トラッカーの名前空間。</li><li>構成を上書きするために使用します。</li><li>構成値を動的に上書きするために使用します。</li></ul> |
| `trk_endpoint` |  <ul><li>トラッカーのエンドポイント</li><li>Snowplow トラッカーのコレクターエンドポイント URI。</li><li>構成値を動的に上書きするために使用します。</li></ul> |
| `trk_cookieDomain` |  <ul><li>Cookie ドメイン</li><li>Cookie を構成するトップレベルドメイン。</li><li>構成値を動的に上書きするために使用します。</li></ul> |
| `trk_cookieName` |  <ul><li>Cookie 名</li><li>Snowplow Cookie のベース名を構成します。</li><li>デフォルト値は **sp** です。</li></ul> |
| `trk_appId` |  <ul><li>アプリ ID</li><li>トラッカーイベントのアプリケーション ID を構成します。</li><li>ページごとに異なる ID を送信してイベントを区別できます。</li></ul> |
| `trk_platform` |  <ul><li>プラットフォーム</li><li>トラッカーのプラットフォームタイプを構成します。</li><li>デフォルト値は **web** です。</li><li>指定可能な値については、[使用可能なプラットフォーム値](https://github.com/snowplow/snowplow/wiki/SnowPlow-Tracker-Protocol#appid)を参照してください。</li></ul> |
| `trk_send` |  <ul><li>送信トラッカー</li><li>文字列／配列</li><li>同じソースからの複数の項目（広告など）を識別するための名前空間値。</li><li>値を構成すると、ページビュー、広告インプレッション、広告コンバージョン、広告クリック、およびリンククリックにエンリッチメントされます。</li></ul> |
| `trk_encodeBase64` |  <ul><li>Base64 エンコードの使用</li><li>自己記述型イベントとカスタムコンテキストを Base64 でエンコードするかどうかを構成します。</li><li>デフォルトは true です。</li><li>指定可能な値は `true` または `false` です。</li></ul> |
| `trk_respectDoNotTrack` |  <ul><li>Do Not Track の尊重</li><li>ブラウザーの Do Not Track オプションを尊重するかどうかを構成します。</li><li>デフォルト値は `false` です。</li><li>指定可能な値は `true` または `false` です。</li></ul> |
| `trk_userFingerprint` |  <ul><li>ユーザーフィンガープリント</li><li>Snowplow がブラウザーの機能に基づいてユーザーフィンガープリントを生成するかどうかを構成します。</li><li>デフォルト値は `true` です。</li><li>指定可能な値は `true` または `false` です。</li></ul> |
| `trk_userFingerprintSeed` |  <ul><li>ユーザーフィンガープリントのシード</li><li>ユーザーフィンガープリントの生成に使用するハッシュシードを構成します。</li><li>デフォルトは `123412414` です。</li></ul> |
| `trk_pageUnloadTimer` |  <ul><li>ページアンロードタイマー</li><li>イベントの発火後、ページをアンロードするまでの待機時間（ミリ秒）を構成します。</li><li>デフォルトは 500 ミリ秒です。</li></ul> |
| `trk_forceSecure` |  <ul><li>トラッカーの HTTPS 強制</li><li>現在のページが http であっても、トラッカーで **https** を強制するよう構成します。</li><li>デフォルト値は `false` です。</li><li>指定可能な値は `true` または `false` です。</li></ul> |
| `trk_sendAsPost` |  <ul><li>POST として送信</li><li>GET リクエストではなく POST リクエストを使用してイベントを送信するよう構成します。</li><li>デフォルト値は `false` です。</li><li>指定可能な値は `true` または `false` です。</li></ul> |
| `trk_bufferSize` |  <ul><li>バッファーサイズ</li><li>POST の使用時にイベントをバッチ処理するためのバッファーサイズを構成します。</li><li>デフォルト値は **1** です。</li></ul> |
| `trk_maxPostBytes` |  <ul><li>POST の最大バイト数</li><li>コレクターに送信する POST リクエストの最大サイズ（バイト単位）を構成します。</li><li>デフォルト値は 40,000 バイトです。</li></ul> |
| `trk_storageStrategy` |  <ul><li>状態の保存方法</li><li>トラッカーの状態を保存する方法を構成します。</li><li>デフォルトは Cookie です。</li><li>指定可能な値：`cookie`、`localStorage`、または `none`</li></ul> |
|`trk_cookieLifetime`|  <ul><li>Cookie の有効期間</li><li>ドメイン固有の訪問 Cookie の保持期間（秒単位）を構成します。</li><li>デフォルト値は 2 年です。1 日は 86,400 秒です。</li></ul> |
|`trk_contextVendor`|  <ul><li>コンテキストエディター</li><li>配列</li><li>すべてのイベントとともに自動送信する、事前定義されたコンテキストの配列を構成します。</li><li>[ベンダーオプション](https://github.com/snowplow/snowplow/wiki/1-General-parameters-for-the-Javascript-tracker#predefined-contexts)</li></ul> |

### E コマース

Snowplow タグでは E コマースが有効になっているため、デフォルトの E コマース拡張機能マッピングが自動的に使用されます。拡張機能のマッピングを上書きする場合や、必要な E コマース変数が拡張機能で提供されていない場合を除き、通常、このカテゴリーで手動マッピングを行う必要はありません。

|**宛先名**| **説明**|
|---| ---|
| `order_id` |  <ul><li>注文 ID</li><li>デフォルトの E コマース値 `_corder` を上書きするために使用します。</li></ul> |
| `order_total` |  <ul><li>注文合計</li><li>デフォルトの E コマース値 `_ctotal` を上書きするために使用します。</li></ul> |
|`order_shipping`|  <ul><li>注文の送料</li><li>デフォルトの E コマース値 `_cship` を上書きするために使用します。</li></ul> |
| `order_tax` |  <ul><li>注文の税額</li><li>デフォルトの E コマース値 `_ctax` を上書きするために使用します。</li></ul> |
|`order_store`|  <ul><li>注文店舗</li><li>デフォルトの E コマース値 `_cstore` を上書きするために使用します。</li></ul> |
| `order_currency` |  <ul><li>注文通貨</li><li>デフォルトの E コマース値 `_ccurrency` を上書きするために使用します。</li></ul> |
|`customer_id`|  <ul><li>顧客 ID</li><li>デフォルトの E コマース値 `_ccustid` を上書きするために使用します。</li></ul> |
| `customer_city` |  <ul><li>顧客の市区町村</li><li>デフォルトの E コマース値 `_ccity` を上書きするために使用します。</li></ul> |
|`customer_state`|  <ul><li>顧客の州</li><li>デフォルトの E コマース値 `_cstate` を上書きするために使用します。</li></ul> |
| `customer_country` |  <ul><li>顧客の国</li><li>デフォルトの E コマース値 `_ccountry` を上書きするために使用します。</li></ul> |
|`product_name`|  <ul><li>商品名のリスト</li><li>配列</li><li>デフォルトの E コマース値 `_cprodname` を上書きするために使用します。</li></ul> |
| `product_sku` |  <ul><li>商品 SKU のリスト</li><li>配列</li><li>デフォルトの E コマース値 `_csku` を上書きするために使用します。</li></ul> |
| `product_category` |  <ul><li>商品カテゴリーのリスト</li><li>配列</li><li>デフォルトの E コマース値 `_ccat` を上書きするために使用します。</li></ul> |
|`product_quantity`|  <ul><li>商品数量のリスト</li><li>配列</li><li>デフォルトの E コマース値 `_cquan` を上書きするために使用します。</li></ul> |
| `product_unit_price` |  <ul><li>商品単価のリスト</li><li>配列</li><li>デフォルトの E コマース値 `_cprice` を上書きするために使用します。</li></ul> |
| `ecm_schema` |  <ul><li>トランザクションコンテキストのスキーマ</li><li>コンテキストを記述する JSON スキーマ。</li><li>Iglu ライブラリ内に存在している必要があります。</li></ul> |
| `ecm_context.data` |  <ul><li>トランザクションコンテキストデータ</li><li>コンテキストによって追跡されるデータ値。</li><li>マッピング時に、`ecm_context.data` の `data` を値に関連付けられた名前に置き換えます。</li></ul> |
| `ecm_contextObj` |  <ul><li>トランザクションのユーザー定義コンテンツ</li><li>スキーマおよびデータプロパティを持つカスタムコンテキストオブジェクト。</li></ul> |
### リンクトラッキング

|**送信先名**| **説明**|
|---| ---|
| `enableLCT` |  <ul><li>リンククリックトラッキングを有効にします。</li><li>リンクのクリックにイベントリスナーを追加します。</li><li>指定可能な値は `true` または `false` です。</li></ul> |
| `ltr_blacklist` |  <ul><li>ブラックリスト</li><li>文字列／配列</li><li>リンククリックトラッカーで無視するCSSクラスのリストです。</li><li>その他のすべてのリンクはトラッキングされます。</li></ul> |
| `ltr_whitelist` |  <ul><li>ホワイトリスト</li><li>文字列／配列</li><li>リンククリックトラッカーでトラッキングするCSSクラスのリストです。</li><li>その他のすべてのリンクは無視されます。</li></ul> |
| `ltr_filter` |  <ul><li>フィルター</li><li>`true` または `false` のいずれかを返す関数（または関数への参照）です。</li><li>`true` を返すすべての項目がトラッキングされます。</li></ul> |
| `ltr_pseudoClicks` |  <ul><li>疑似クリック</li><li>中央クリックをクリックイベントとして認識するかどうかを構成します。</li><li>デフォルト値は `false` です。</li><li>指定可能な値は `true` または `false` です。</li></ul> |
| `ltr_clickContent` |  <ul><li>クリックコンテンツ</li><li>クリックイベントでリンクのinnerHTMLを取得するかどうかを構成します。</li><li>指定可能な値は `true` または `false` です。</li></ul> |
|`ltr_url`|  <ul><li>URL</li><li>手動でトラッキングするイベント用です。</li><li>ターゲットURLを構成します。</li></ul> |
| `ltr_elementId` |  <ul><li>要素ID</li><li>手動でトラッキングするイベント用です。</li><li>要素のリンクIDを構成します。</li></ul> |
| `ltr_elementClasses` |  <ul><li>要素のクラス</li><li>配列</li><li>手動でトラッキングするイベント用です。</li><li>要素のリンククラスを構成します。</li></ul> |
| `ltr_elementTarget` |  <ul><li>要素のターゲット</li><li>手動でトラッキングするイベント用です。</li><li>要素のリンクターゲットを構成します。</li></ul> |
|`ltr_elementClickContent`|  <ul><li>要素のクリックコンテンツ</li><li>配列</li><li>手動でトラッキングするイベント用です。</li><li>要素のリンクコンテンツを構成します。</li></ul> |
| `ltr_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマです。</li><li>Igluライブラリに存在している必要があります。</li></ul> |
| `ltr_context.data` |  <ul><li>コンテキストデータ</li><li>コンテキストでトラッキングするデータ値です。</li><li>マッピング時に、`ltr_context.data` の `data` を値に関連付けられた名前に置き換えます。</li></ul> |
| `ltr_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマおよびデータプロパティを持つカスタムコンテキストオブジェクトです。</li></ul> |

### 広告トラッキング

|**送信先名**| **説明**|
|---| ---|
|`adtracking`|  <ul><li>広告トラッキング</li><li>トラッキングする広告の種類を構成します。</li><li>この項目に値が入力されている場合にのみ、広告イベントが発生します。</li><li>指定可能な値は `impression`、`click`、または `conversion` です。</li></ul> |
| `ad_impressionId` |  <ul><li>インプレッションID</li><li>現在のインプレッションインスタンスの識別子を構成します。</li></ul> |
| `ad_costModel` |  <ul><li>コストモデル</li><li>キャンペーンのコストモデルを構成します。</li><li>指定可能な値：`cpc`、`cpm`、または `cpa`</li></ul> |
| `ad_cost` |  <ul><li>コスト</li><li>広告のコストを構成します。</li></ul> |
|`ad_targetUrl`|  <ul><li>ターゲットURL</li><li>広告の遷移先URLを構成します。</li></ul> |
|`ad_bannerId`|  <ul><li>バナーID</li><li>広告の `adserver` 識別子を構成します。</li></ul> |
| `ad_zoneId` |  <ul><li>ゾーンID</li><li>広告が配置されているゾーンの `adserver` 識別子を構成します。</li></ul> |
| `ad_advertiserId` |  <ul><li>広告主ID</li><li>配列</li><li>キャンペーンの属する広告主の `adserver` 識別子を構成します。</li></ul> |
| `ad_campaignId` |  <ul><li>キャンペーンID</li><li>バナーの属するキャンペーンの `adserver` 識別子を構成します。</li></ul> |
| `ad_clickId` |  <ul><li>クリックID</li><li>現在のクリックインスタンスの識別子を構成します。</li></ul> |
| `ad_conversionId` |  <ul><li>コンバージョンID</li><li>現在のコンバージョンインスタンスの識別子を構成します。</li></ul> |
| `ad_category` |  <ul><li>カテゴリー</li><li>コンバージョンのカテゴリーを構成します。</li></ul> |
| `ad_action` |  <ul><li>アクション</li><li>コンバージョンにおけるユーザー操作の種類を構成します。</li></ul> |
| `ad_property` |  <ul><li>プロパティ</li><li>コンバージョンのオブジェクトに関する説明を構成します。</li></ul> |
| `ad_initialValue` |  <ul><li>初期値</li><li>コンバージョンの初期価値を構成します。</li></ul> |
| `ad_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマです。</li><li>Igluライブラリに存在している必要があります。</li></ul> |
| `ad_context.data` |  <ul><li>コンテキストデータ</li><li>コンテキストでトラッキングするデータ値です。</li><li>マッピング時に、`ad_context.data` の `data` を値に関連付けられた名前に置き換えます。</li></ul> |
| `ad_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマおよびデータプロパティを持つカスタムコンテキストオブジェクトです。</li></ul> |

### ページビューのカスタムコンテキスト

|**送信先名**| **説明**|
|---| ---|
| `cc_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマです。</li><li>Igluライブラリに存在している必要があります。</li></ul> |
|`cc_context.data`|  <ul><li>コンテキストデータ</li><li>コンテキストでトラッキングするデータ値です。</li><li>マッピング時に、`cc_context.data` の `data` を値に関連付けられた名前に置き換えます。</li></ul> |
| `cc_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマおよびデータプロパティを持つカスタムコンテキストオブジェクトです。</li></ul> |

### ソーシャルトラッキング

|**送信先名**| **説明**|
|---| ---|
| `sot_action` |  <ul><li>アクション</li><li>ユーザーが実行したアクションです。</li></ul> |
| `sot_network` |  <ul><li>ソーシャルネットワーク</li><li>ユーザーが操作したネットワークです。</li></ul> |
| `sot_target` |  <ul><li>ターゲット</li><li>実行されたアクションの対象となるオブジェクトです。</li></ul> |
| `sot_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマです。</li><li>Igluライブラリに存在している必要があります。</li></ul> |
| `sot_context.data` |  <ul><li>コンテキストデータ</li><li>コンテキストでトラッキングするデータ値です。</li><li>マッピング時に、`sot_context.data` の `data` を値に関連付けられた名前に置き換えます。</li></ul> |
| `sot_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマおよびデータプロパティを持つカスタムコンテキストオブジェクトです。</li></ul> |

### フォームトラッキング

|**送信先名**| **説明**|
|---| ---|
| `enableFormTracking` |  <ul><li>フォームトラッキングを有効にします。</li><li>フォームの変更および送信をトラッキングするかどうかを構成します。</li><li>指定可能な値は `true` または `false` です。</li></ul> |
| `ftr_formBlacklist` |  <ul><li>フォームのカスタムブラックリスト</li><li>配列</li><li>フォームトラッカーで無視するフォームのCSSクラスのリストです。</li><li>その他のすべてのリンクはトラッキングされます。</li><li>例：ログインフォーム、リクエストフォーム</li></ul> |
| `ftr_formWhitelist` |  <ul><li>フォームのカスタムホワイトリスト</li><li>配列</li><li>フォームトラッカーでトラッキングするフォームのCSSクラスのリストです。</li><li>その他のすべてのリンクは無視されます。</li><li>例：ログインフォーム、リクエストフォーム</li></ul> |
| `ftr_fieldBlacklist` |  <ul><li>フィールドのカスタムブラックリスト</li><li>配列</li><li>フォームトラッカーで無視するフィールドのCSSクラスのリストです。</li><li>その他のすべてのリンクはトラッキングされます。</li><li>例：パスワードフィールド、メールアドレスフィールド</li></ul> |
| `ftr_fieldWhitelist` |  <ul><li>フィールドのカスタムホワイトリスト</li><li>配列</li><li>フォームトラッカーでトラッキングするフィールドのCSSクラスのリストです。</li><li>その他のすべてのリンクは無視されます。</li><li>例：パスワードフィールド、メールアドレスフィールド</li></ul> |
| `ftr_filterForm` |  <ul><li>カスタムフォームフィルター関数</li><li>`true` または `false` のいずれかを返す関数（または関数への参照）です。</li><li>`true` を返すすべての項目がトラッキングされます。</li></ul> |
| `ftr_filterField` |  <ul><li>カスタムフィールドフィルター関数</li><li>`true` または `false` のいずれかを返す関数（または関数への参照）です。</li><li>`true` を返すすべての項目がトラッキングされます。</li></ul> |
| `ftr_ctmConfig` |  <ul><li>ユーザー定義構成</li><li>上記のプロパティを持つカスタム構成オブジェクトです。</li><li>個別のプロパティの代わりに使用します。</li></ul> |
### カートトラッキング

|**送信先名**| **説明**|
|---| ---|
| `cartTracking` |  <ul><li>カートトラッキング</li><li>トラッキングするカートイベントの種類を構成します。</li><li>この値が構成されている場合にのみ、カートイベントが発生します。</li><li>指定可能な値は `cart_add` または `cart_remove` です。</li></ul> |
| `cart_sku` |  <ul><li>カート内商品のSKU</li><li>カート内で移動される商品のSKU。</li></ul> |
| `cart_name` |  <ul><li>カート内商品名</li><li>カート内で移動される商品の名前。</li></ul> |
| `cart_category` |  <ul><li>カート内商品のカテゴリー</li><li>カート内で移動される商品のカテゴリー。</li></ul> |
| `cart_price` |  <ul><li>カート内商品の単価</li><li>カート内で移動される商品の価格。</li></ul> |
| `cart_quantity` |  <ul><li>カート内商品の数量</li><li>カート内で移動される商品の数量。</li></ul> |
| `cart_currency` |  <ul><li>カート内商品の通貨</li><li>カート内で移動される商品の通貨。</li></ul> |
| `cart_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマ。</li><li>Igluライブラリ内に存在する必要があります。</li></ul> |
| `cart_context.data` |  <ul><li>コンテキストデータ</li><li>コンテキストによってトラッキングされるデータ値。</li><li>マッピング時に、`cart_context.data` 内の `data` を値に関連付けられた名前に置き換えます。</li></ul> |
| `cart_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマおよびデータプロパティを持つカスタムコンテキストオブジェクト。</li></ul> |

### サイト内検索トラッキング

|**送信先名**| **説明**|
|---| ---|
| `sst_terms` |  <ul><li>検索語句</li><li>配列</li><li>サイト内検索で使用された語句のリスト。</li><li>この値が構成されている場合にのみ、検索イベントが発生します。</li></ul> |
|`sst_filters`|  <ul><li>検索フィルター</li><li>フィルターの種類と語句を定義するJSONオブジェクト。</li></ul> |
| `sst_totalResults` |  <ul><li>検索結果の総数</li><li>検索で見つかった結果の総数。</li></ul> |
| `sst_pageResults` |  <ul><li>最初のページの検索結果数</li><li>最初のページに表示される結果の数。</li></ul> |
| `sst_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマ。</li><li>Igluライブラリ内に存在する必要があります。</li></ul> |
| `sst_context.data` |  <ul><li>コンテキストデータ</li><li>コンテキストによってトラッキングされるデータ値。</li><li>マッピング時に、`sst_context.data` 内の `data` を値に関連付けられた名前に置き換えます。</li></ul> |
| `sst_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマおよびデータプロパティを持つカスタムコンテキストオブジェクト。</li></ul> |

### 構造化イベント

|**送信先名**| **説明**|
|---| ---|
| `stctCat` |  <ul><li>カテゴリー</li><li>トラッキングするオブジェクトのグループ名。</li></ul> |
| `stctActn` |  <ul><li>アクション名</li><li>トラッキングするオブジェクトに対するユーザー操作の名前。</li></ul> |
| `stctLabel` |  <ul><li>ラベル</li><li>トラッキングする特定のオブジェクトを識別する追加の名前。</li></ul> |
| `stctProp` |  <ul><li>プロパティ</li><li>オブジェクトまたはそのオブジェクトに対して実行されたアクションを記述する追加項目。</li></ul> |
| `stctVal` |  <ul><li>値</li><li>ユーザー操作を記述する追加の10進数値。</li></ul> |
| `stc_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマ。</li><li>Igluライブラリ内に存在する必要があります。</li></ul> |
|`stc_context.data`|  <ul><li>コンテキストデータ</li><li>コンテキストによってトラッキングされるデータ値。</li><li>マッピング時に、`stc_context.data` 内の `data` を値に関連付けられた名前に置き換えます。</li></ul> |
| `stc_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマおよびデータプロパティを持つカスタムコンテキストオブジェクト。</li></ul> |

### 非構造化イベント

|**送信先名**| **説明**|
|---| ---|
| `unstctDataSchema` |  <ul><li>スキーマ</li><li>イベントを記述するJSONスキーマ。Igluライブラリ内に存在する必要があります。</li></ul> |
| `unstctData.data` |  <ul><li>ユーザー定義データ</li><li>イベントによってトラッキングされるデータ値。</li><li>マッピング時に、`unstctData.data` 内の `data` を値に関連付けられた名前に置き換えます。</li></ul> |
| `unstctDataObj` |  <ul><li>ユーザー定義データオブジェクト</li><li>上記のプロパティを持つカスタム構成オブジェクト。</li><li>個別のプロパティの代わりに使用します。</li></ul> |
| `stc_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマ。</li><li>Igluライブラリ内に存在する必要があります。</li></ul> |
| `nstc_context.data` |  <ul><li>コンテキストデータ</li><li>コンテキストによってトラッキングされるデータ値。</li><li>マッピング時に、`unstc_context.data` 内の `data` を値に関連付けられた名前に置き換えます。</li></ul> |
| `unstc_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマおよびデータプロパティを持つカスタムコンテキストオブジェクト。</li></ul> |

### 同意トラッキング

|**送信先名**| **説明**|
|---| ---|
| `consentGranted` |  <ul><li>ユーザーによる同意</li><li>ユーザーがデータ収集にオプトインしたことをトラッキングするために使用します。</li><li>少なくとも `id` および `version` 引数が指定されている場合、同意文書コンテキストがイベントに添付されます。</li></ul> |
| `consentWithdrawn` |  <ul><li>ユーザーによる一部の同意の撤回</li><li>ユーザーがデータ収集への同意を撤回したことをトラッキングするために使用します。</li><li>少なくとも `id` および `version` 引数が指定されている場合、同意文書コンテキストがイベントに添付されます。</li></ul> |
| `allConsentWithdrawn` |  <ul><li>ユーザーによるすべての同意の撤回</li><li>すべての同意を撤回するかどうかを指定します。</li></ul> |
| `con_documentId` |  <ul><li>同意文書ID</li><li>同意文書は、メソッドに渡された引数を格納するカスタムコンテキストです（同意および撤回イベントのいずれでも、引数は `id`、`version`、`name`、`description` です）。</li><li>いずれの同意メソッドでも、コンテキスト引数に同意文書の自己記述型JSONの配列を渡すことで、イベントに文書を追加できます。</li></ul> |
| `con_documentVer` |  <ul><li>同意文書のバージョン</li><li>必須</li><li>同意を付与する文書のバージョン。</li></ul> |
| `con_documentName` |  <ul><li>同意文書名</li><li>同意文書の名前。</li></ul> |
| `con_documentDesc` |  <ul><li>同意文書の説明</li><li>同意文書の説明。</li></ul> |
| `con_documentExpiry` |  <ul><li>同意文書の有効期限</li><li>指定された日時まで、ユーザーが添付文書に同意することを示します。その日時を過ぎると、同意は無効になります。</li></ul> |
| `unstc_schema` |  <ul><li>コンテキストスキーマ</li><li>文字列</li><li>コンテキストを記述するJSONスキーマ。</li><li>Igluライブラリ内に存在する必要があります。</li></ul> |
| `nstc_context.data` |  <ul><li>コンテキストデータ</li><li>コンテキストによってトラッキングされるデータ値。</li><li>マッピング時に、`unstc_context.data` 内の `data` を値に関連付けられた名前に置き換えます。</li></ul> |
| `con_contextObj` |  <ul><li>ユーザー定義コンテキスト</li><li>スキーマおよびデータプロパティを持つカスタムコンテキストオブジェクト。</li></ul> |

## ベンダーのドキュメント

* [SnowPlow JavaScript Trackerのドキュメント](https://docs.snowplowanalytics.com/docs/collecting-data/collecting-from-own-applications/javascript-trackers/)