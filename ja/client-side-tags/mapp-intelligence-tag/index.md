---
title: Mapp Intelligence（レガシーピクセル）タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでMapp Intelligence（レガシーピクセル）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/mapp-intelligence-tag/
---
Mapp Intelligenceは、ウェブサイトの使用状況と顧客の深い理解を分析者とマーケターに提供し、適切なメッセージを適切なタイミングで適切なチャネルでターゲットオーディエンスに提供するための必要な情報を提供します。

## タグのヒント

* データマッピングに追加された値は、Webtrekk（`wt`）オブジェクトに挿入されます。例えば、`wt_config.contentId`や`internalSearch`を構成するためにデータマッピングを使用します。
* Mapp Intelligenceタグは、**Form HTML ID**（`formTrackInstall`）に値を構成することで`formTrackInstall()`を自動的にトリガーします。
* イベントトラッキングは、`utag.link()`を使用した関数呼び出しで行うことができます。
* 注文値を自動的に構成するには、E-Commerce拡張が必要です。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[Tag Overview]()の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **ライブラリバージョン**：使用しているライブラリのバージョン。
* **トラックID**：リクエストをアカウントに割り当てるために使用されるID。Mapp **システム構成**の**データ収集**に移動してトラックIDを探します。同じ情報を複数のアカウントに記録する必要がある場合は、対応するトラックIDをカンマで区切ったリストとして入力します。
* **トラックドメイン**：アカウントマネージャーから提供されたMapp Intelligenceのトラックドメイン。
* **Param First**：最初に送信されるパラメータのセミコロンで区切られたリスト。
* **ドメイン**：トラッキングされるウェブサイトのドメイン。セミコロンで区切って複数のドメインを入力することができます。
* **リンクトラッキング**：Mapp IntelligenceタグはHTMLリンクをトラッキングする2つの方法を提供します：
  * **リンク**：すべてのHTMLリンクは、クリックされたときに自動的にトラッキングされます
  * **スタンダード**：ページのすべてのラベル付きHTMLリンクは、クリックされたときにトラッキングされます。
* **Link Track Attribute**：リンク名に使用されるHTML属性の名前。
* **Link Track Params**：リンクURLのクエリ文字列パラメータの名前。これはリンク名として使用されます。
* **Link Track Downloads**：トラックするダウンロードファイルの拡張子。例えば、`.zip`、`.rar`、`.doc`
* **Pixel Sampling**：ページ上でn番目のユーザーだけがトラッキングされるかどうかを定義します。
* **Force HTTPS**：**on**または**off**を選択します。
* **Cookie Handling**：使用するクッキーを選択します：ファーストパーティクッキーまたはサードパーティクッキー。
* **Cookie Domain**
* **mediaCode**：標準キャンペーントラッキングに使用するパラメータを識別するために**mediaCode**を構成します。
* **mediaCodeCookie**：**mediaCode**クエリパラメータがアドレスバーにある場合（例えば、AJAX駆動のウェブサイトで）、**mediaCodeCookie**を`sid`に構成します。
* **WT Object Name**：WTオブジェクトの名前。単一のWebtrekkインスタンスを使用している場合は、デフォルトの`wt`をそのまま使用します。
* **Form Tracking**：グローバルフォームトラッキングを有効にします。単一のページでフォームトラッキングを有効にするには、データマッピングで**Form HTML ID**を使用します。
* **Request Queue**：**on**または**off**を選択します。
* **Server to Server Tracking**：**on**または**off**を選択します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[Load Rules]()のドキュメンテーションを参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。タグ宛先に変数をマップする方法については、[data mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

| 変数                                                              | 説明     |
|:----------------------------------------------------------------------|:----------------|
| WT Object Name (`wt_object_name`)                                     | [文字列]        |
| Request of Obfusacation (`requestObfuscation`)                        | [ブーリアン]       |
| Secure Configuration (`secureConfig`)                                 | [文字列]        |
| Send via SDK ( `sendViaSDK` )                                         | [ブーリアン]       |
| Parameters to Include First (`wt_config.paramFirst`)                  |                 |
| Ignore Pre-rendering (`wt_config.ignorePrerendering`)                 | [ブーリアン]       |
| Form Path Analysis (`wt_config.formPathAnalysis`)                     | [ブーリアン]       |
| tabBrowsing (`wt_config.tabBrowsing`)                                 | [ブーリアン]       |
| globalVisitorIds (`wt_config.globalVisitorIds`)                       | [ブーリアン]       |
| execCDB (`wt_config.execCDB`)                                         | [ブーリアン]       |
| useCDBCache (`wt_config.useCDBCache`)                                 | [ブーリアン]       |
| useCDBScript (`wt_config.useCDBScript`)                               | [ブーリアン]       |
| requestLimitAmount (`wt_config.requestLimitAmount`)                   |                 |
| requestLimitTime (`wt_config.requestLimitTime`)                       |                 |
| Track ID (`wt_config.trackId`)                                        |                 |
| Track Domain (`wt_config.trackDomain`)                                |                 |
| Domain (`wt_config.domain`)                                           |                 |
| Link Track ( `wt_config.linkTrack` )                                  |                 |
| Link Track Attribute (`wt_config.linkTrackAttribute`)                 |                 |
| Link Track Params (`wt_config.linkTrackParams`)                       |                 |
| Link Track Downloads (`wt_config.linkTrackDownloads`)                 | [RegExp Object] |
| Link Track Pattern (`wt_config.linkTrackPattern`)                     |                 |
| Llink Track Replace (`wt_config.linkTrackReplace`)                    |                 |
| Link Track Ignore Pattern (`wt_config.linkTrackIgnorePattern`)        |                 |
| No Delay Link Track Attribute (`wt_config.noDelayLinkTrackAttribute`) |                 |
| Pixel Sampling (`wt_config.pixelSampling`)                            |                 |
| Force HTTPS (`wt_config.forceHTTPS`)                                  |                 |
| Cookie Handling (`wt_config.cookie`)                                  |                 |
| Cookie Domain (`wt_config.cookieDomain`)                              |                 |
| contentId (`wt_config.contentId`)                                     |                 |
| Form (`wt_config.form`)                                               |                 |
| executePluginFunction (`wt_config.executePluginFunction`)             |                 |
| Media Code Cookie (`wt_config.mediaCodeCookie`)                       |                 |
| Media Code (`wt_config.mediaCode`)                                    |                 |
| Custom wt config item (`wt_config.###`)                               |                 |

### 一般

| 変数                           | 説明  |
|:-----------------------------------|:-------------|
| Custom Visitor ID                  |              |
| Login Status (`loginStatus`)       |              |
| URM Categories (`urmCategory.###`) |              |
| Email RID (`emailRID`)             |              |
| Email Opt-In (`emailOptin`)        |              |
| Gender (`gender`)                  |              |
| Birthday (`birthday`)              | [`YYYYMMDD`] |
| Birthday Year (`birthdayJ`)        | [`YYYY`]     |
| Birthday Month (`birthdayM`)       | [`MM`]       |
| Birthday Day (`birthdayD`)         |              |
| CRM Category 1                     |              |
| CRM Category 2                     |              |
| CRMカテゴリー3                     |              |
| CRMカテゴリー4                     |              |
| CRMカテゴリー5                     |              |
| CRMカテゴリー6                     |              |
| CRMカテゴリー7                     |              |
| CRMカテゴリー8                     |              |
| CRMカテゴリー9                     |              |
| CRMカテゴリー10                    |              |
| カスタムセッションパラメーター1         |              |
| カスタムセッションパラメーター2         |              |
| カスタムセッションパラメーター3         |              |
| カスタムセッションパラメーター4         |              |
| カスタムセッションパラメーター5         |              |
| カスタムセッションパラメーター6         |              |
| カスタムセッションパラメーター7         |              |
| カスタムセッションパラメーター8         |              |
| カスタムセッションパラメーター9         |              |
| カスタムセッションパラメーター10        |              |

### ページデータ

| 変数                                        | 説明 |
|:------------------------------------------------|:------------|
| ページタイトル (`pageTitle`)                        | [文字列]    |
| コンテンツID (`contentId`)                        |             |
| URLパターン (`pageURLPattern`)                  |             |
| URL置換 (`pageURLReplace`)                  |             |
| タブブラウジング (`tabBrowsing`)                    | [ブール値]   |
| 内部検索 (`internalSearch`)              | [文字列]    |
| 検索結果の数 (`numberSearchResults`) | [数値]    |
| エラーメッセージ (`errorMessages`)                | [文字列]    |
| ページタイプ (`pageType`)                          | [文字列]    |
| ページ長 (`pageLength`)                          | [文字列]    |
| 記事タイトル (`articleTitle`)                  | [文字列]    |
| 公開からの日数 (`daysSincePublication`) | [数値]    |
| ペイウェルコール (`paywell`)                       | [文字列]    |
| コンテンツタグ (`contentTags`)                    | [文字列]    |
| コンテンツグループ1                                 |             |
| コンテンツグループ2                                 |             |
| コンテンツグループ3                                 |             |
| コンテンツグループ4                                 |             |
| コンテンツグループ5                                 |             |
| コンテンツグループ6                                 |             |
| コンテンツグループ7                                 |             |
| コンテンツグループ8                                 |             |
| コンテンツグループ9                                 |             |
| コンテンツグループ10                                |             |
| コンテンツグループ11                                |             |
| コンテンツグループ12                                |             |
| コンテンツグループ13                                |             |
| コンテンツグループ14                                |             |
| コンテンツグループ15                                |             |
| コンテンツグループ16                                |             |
| コンテンツグループ17                                |             |
| コンテンツグループ18                                |             |
| コンテンツグループ19                                |             |
| コンテンツグループ20                                |             |
| コンテンツグループ21                                |             |
| コンテンツグループ22                                |             |
| コンテンツグループ23                                |             |
| コンテンツグループ24                                |             |
| コンテンツグループ25                                |             |
| カスタムパラメーター1                              |             |
| カスタムパラメーター2                              |             |
| カスタムパラメーター3                              |             |
| カスタムパラメーター4                              |             |
| カスタムパラメーター5                              |             |
| カスタムパラメーター6                              |             |
| カスタムパラメーター7                              |             |
| カスタムパラメーター8                              |             |
| カスタムパラメーター9                              |             |
| カスタムパラメーター10                             |             |
| カスタムパラメーター11                             |             |
| カスタムパラメーター12                             |             |
| カスタムパラメーター13                             |             |
| カスタムパラメーター14                             |             |
| カスタムパラメーター15                             |             |
| カスタムパラメーター16                             |             |
| カスタムパラメーター17                             |             |
| カスタムパラメーター18                             |             |
| カスタムパラメーター19                             |             |
| カスタムパラメーター20                             |             |
| カスタムパラメーター21                             |             |
| カスタムパラメーター22                             |             |
| カスタムパラメーター23                             |             |
| カスタムパラメーター24                             |             |
| カスタムパラメーター25                             |             |
| カスタムパラメーター26                             |             |
| カスタムパラメーター27                             |             |
| カスタムパラメーター28                             |             |
| カスタムパラメーター29                             |             |
| カスタムパラメーター30                             |             |
| カスタムパラメーター31                             |             |
| カスタムパラメーター32                             |             |
| カスタムパラメーター33                             |             |
| カスタムパラメーター34                             |             |
| カスタムパラメーター35                             |             |
| カスタムパラメーター36                             |             |
| カスタムパラメーター37                             |             |
| カスタムパラメーター38                             |             |
| カスタムパラメーター39                             |             |
| カスタムパラメーター40                             |             |
| カスタムパラメーター41                             |             |
| カスタムパラメーター42                             |             |
| カスタムパラメーター43                             |             |
| カスタムパラメーター44                             |             |
| カスタムパラメーター45                             |             |
| カスタムパラメーター46                             |             |
| カスタムパラメーター47                             |             |
| カスタムパラメーター48                             |             |
| カスタムパラメーター49                             |             |
| カスタムパラメーター50                             |             |

### 検索＆フォームトラッキング

| 変数                                           | 説明      |
|:---------------------------------------------------|:-----------------|
| フォーム (`form`)                                      | [`0`/`1`]        |
| フォーム属性 (`formAttribute`)                   | [文字列]         |
| フォーム値属性 (`formValueAttribute`)        | [文字列]         |
| フォームフィールド属性 (`formFieldAttribute`)        | [文字列]         |
| フルコンテンツフォームトラッキング (`formFullContent`)     | [配列]          |
| フォームパス分析 (`formPathAnalysis`)            | [`true`/`false`] |
| 匿名フォームトラッキング (`formAnonymous`)          | [`0`/`1`]        |
| フォームフィールドデフォルト値 (`formFieldDefaultValue`) | [文字列]         |
| フォームHTML ID (`formTrackInstall`)                  |                  |

### クリックトラッキング

| 変数                                                    | 説明     |
|:------------------------------------------------------------|:----------------|
| リンクトラック (`linkTrack`)                                    | [link/standard] |
| リンクトラック属性 (`linkTrackAttribute`)                 | [文字列]        |
| リンクトラックパターン (`linkTrackPattern`)                     | [RegExp Object] |
| リンクトラック無視パターン (`linkTrackIgnorePattern`)        | [String]        |
| リンクトラック置換 (`linkTrackReplace`)                     | [String]        |
| リンクトラックダウンロード (`linkTrackDownloads`)                 | [Array]         |
| リンクトラック遅延 (`delayLinkTrack`)                         | [true/false]    |
| リンクトラック遅延時間 (`delayLinkTrackTime`)                | [Number]        |
| リンクトラック遅延なし属性 (`noDelayLinkTrackAttribute`) | [String]        |
| リンクトラックパラメータ                                           |                 |
| カスタムutag.linkトラッキングのためのリンクID (`linkId`)            |                 |

### キャンペーントラッキング

| 変数                              | 説明 |
|:--------------------------------------|:------------|
| メディアコード (`mediaCode`)              |             |
| メディアコードクッキー (`mediaCodeCookie`) |             |
| キャンペーンID (`campaignId`)            |             |
| キャンペーンアクション (`campaignAction`)    |             |
| カスタムキャンペーンパラメータ1           |             |
| カスタムキャンペーンパラメータ2           |             |
| カスタムキャンペーンパラメータ3           |             |
| カスタムキャンペーンパラメータ4           |             |
| カスタムキャンペーンパラメータ5           |             |
| カスタムキャンペーンパラメータ6           |             |
| カスタムキャンペーンパラメータ7           |             |
| カスタムキャンペーンパラメータ8           |             |
| カスタムキャンペーンパラメータ9           |             |
| カスタムキャンペーンパラメータ10          |             |

### サーバートラッキング

| 変数                                                          | 説明      |
|:------------------------------------------------------------------|:-----------------|
| サーバー経由送信有効 (`sendViaServerActivated`)              | [`true`/`false`] |
| サーバー経由送信ドメイン (`sendViaServerDomain`)                    | [String]         |
| サーバー経由送信パス (`sendViaServerPath`)                        | [String]         |
| サーバー経由送信ドロップリクエスト (`sendViaServerDroppedRequests`) |                  |
| サーバー経由送信ブラックリスト (`sendViaServerBlacklist`)              |                  |

### クッキー

| 変数                                     | 説明 |
|:---------------------------------------------|:------------|
| クッキー更新 (`updateCookie`)               | [Boolean]   |
| クッキーセキュア (`cookieSecure`)               | [Boolean]   |
| クッキーEver IDタイムアウト (`cookieEidTimeout`)  | [Number]    |
| Ever IDの検証 (`validateEverId`)          | [Boolean]   |
| クッキーオプトアウト名 (`optoutName`)            | [String]    |
| クッキーオプトアウトタイムフレーム (`optoutTimeFrame`) |             |

### リクエストキュー

| 変数                                                  | 説明 |
|:----------------------------------------------------------|:------------|
| リクエストキュー有効 (`requestQueueActivated`)         | [Boolean]   |
| リクエストキュー再送間隔 (`requestQueueResendInterval`) | [Number]    |
| リクエストキューTTL (`requestQueueTTL`)                    | [Number]    |
| リクエストキューサイズ (`requestQueueSize`)                   | [Boolean]   |

### 匿名トラッキング

| 変数                                                              | 説明 |
|:----------------------------------------------------------------------|:------------|
| 匿名機能有効 (`enableAnonymousFunction`)                 | [Boolean]   |
| 匿名オプトイン (`anonymousOptIn`)                                   | [Boolean]   |
| 匿名クッキー名 (`anonymousCookieName`)                         | [String]    |
| 識別パラメータの抑制 (`suppressIdentificationParameter`) | [Array]     |

### E-コマース

| 変数                                | 説明                                                   |
|:----------------------------------------|:--------------------------------------------------------------|
| 注文ID (`order_id`)                   | ( `_corder` を上書きします)                                        |
| 注文合計 (`order_total`)             | ( `_ctotal` を上書きします)                                        |
| 通貨 (`order_currency`)             | ( `_ccurrency` を上書きします)                                     |
| クーポン値 (`order_couponValue`)      |                                                               |
| 名前のリスト (`product_name`)          | [Array]&lt;br&gt; ( `_cprodname` を上書きします)                         |
| 数量のリスト (`product_quantity`) | [Array]&lt;br&gt; ( `_cquan` を上書きします)                             |
| 価格のリスト (`product_unit_price`)   | [Array] &lt;br&gt; ( `_cprice` を上書きします)                           |
| 商品カテゴリ (`product_category`)    | [Array] &lt;br&gt; カテゴリのリスト &lt;br&gt; ( `_ccat` を上書きします)     |
| 商品ブランド (`product_brand`)       | [Array]&lt;br&gt; ブランドのリスト &lt;br&gt; ( `_cbrand` を上書きします)        |
| 商品サブカテゴリ (`product_subcategory`) | [Array]&lt;br&gt; サブカテゴリのリスト &lt;br&gt; ( `_ccat2` を上書きします) |
| 商品ステータス (`productStatus`)        |                                                               |
| 支払い方法 (`paymentMethod`)        | [String]                                                      |
| 配送サービス (`shippingService`)    | [String]                                                      |
| 配送速度 (`shippingSpeed`)        | [String]                                                      |
| 配送費用 (`shippingCosts`)        | [Number]                                                      |
| 粗利益 (`grossMargin`)            | [Number]                                                      |
| 注文ステータス (`orderStatus`)            | [String]                                                      |
| 商品バリエーション (`productVariant`)      | [String]                                                      |
| 商品売り切れ (`productSoldOut`)     | [`0`/`1`]                                                     |
| 商品カテゴリ1                      |                                                               |
| 商品カテゴリ2                      |                                                               |
| 商品カテゴリ3                      |                                                               |
| 商品カテゴリ4                      |                                                               |
| 商品カテゴリ5                      |                                                               |
| 商品カテゴリ6                      |                                                               |
| 商品カテゴリ7                      |                                                               |
| 商品カテゴリ8                      |                                                               |
| 商品カテゴリ9                      |                                                               |
| 商品カテゴリ10                     |                                                               |
| 商品カテゴリ11                     |                                                               |
| 商品カテゴリ12                     |                                                               |
| 商品カテゴリ13                     |                                                               |
| 商品カテゴリ14                     |                                                               |
| 商品カテゴリ15                     |                                                               |
| 商品カテゴリ16                     |                                                               |
| 商品カテゴリ17                     |                                                               |
| 商品カテゴリ18                     |                                                               |
| 商品カテゴリ19                     |                                                               |
| 商品カテゴリ20                           |                                                               |
| 商品カテゴリ21                           |                                                               |
| 商品カテゴリ22                           |                                                               |
| 商品カテゴリ23                           |                                                               |
| 商品カテゴリ24                           |                                                               |
| 商品カテゴリ25                           |                                                               |
| カスタムEコマースパラメータ1             |                                                               |
| カスタムEコマースパラメータ2             |                                                               |
| カスタムEコマースパラメータ3             |                                                               |
| カスタムEコマースパラメータ4             |                                                               |
| カスタムEコマースパラメータ5             |                                                               |
| カスタムEコマースパラメータ6             |                                                               |
| カスタムEコマースパラメータ7             |                                                               |
| カスタムEコマースパラメータ8             |                                                               |
| カスタムEコマースパラメータ9             |                                                               |
| カスタムEコマースパラメータ10            |                                                               |
| カスタムEコマースパラメータ11            |                                                               |
| カスタムEコマースパラメータ12            |                                                               |
| カスタムEコマースパラメータ13            |                                                               |
| カスタムEコマースパラメータ14            |                                                               |
| カスタムEコマースパラメータ15            |                                                               |
| カスタムEコマースパラメータ16            |                                                               |
| カスタムEコマースパラメータ17            |                                                               |
| カスタムEコマースパラメータ18            |                                                               |
| カスタムEコマースパラメータ19            |                                                               |
| カスタムEコマースパラメータ20            |                                                               |
| カスタムEコマースパラメータ21            |                                                               |
| カスタムEコマースパラメータ22            |                                                               |
| カスタムEコマースパラメータ23            |                                                               |
| カスタムEコマースパラメータ24            |                                                               |
| カスタムEコマースパラメータ25            |                                                               |
| カスタムEコマースパラメータ26            |                                                               |
| カスタムEコマースパラメータ27            |                                                               |
| カスタムEコマースパラメータ28            |                                                               |
| カスタムEコマースパラメータ29            |                                                               |
| カスタムEコマースパラメータ30            |                                                               |
| カスタムEコマースパラメータ31            |                                                               |
| カスタムEコマースパラメータ32            |                                                               |
| カスタムEコマースパラメータ33            |                                                               |
| カスタムEコマースパラメータ34            |                                                               |
| カスタムEコマースパラメータ35            |                                                               |
| カスタムEコマースパラメータ36            |                                                               |
| カスタムEコマースパラメータ37            |                                                               |
| カスタムEコマースパラメータ38            |                                                               |
| カスタムEコマースパラメータ39            |                                                               |
| カスタムEコマースパラメータ40            |                                                               |
| カスタムEコマースパラメータ41            |                                                               |
| カスタムEコマースパラメータ42            |                                                               |
| カスタムEコマースパラメータ43            |                                                               |
| カスタムEコマースパラメータ44            |                                                               |
| カスタムEコマースパラメータ45            |                                                               |
| カスタムEコマースパラメータ46            |                                                               |
| カスタムEコマースパラメータ47            |                                                               |
| カスタムEコマースパラメータ48            |                                                               |
| カスタムEコマースパラメータ49            |                                                               |
| カスタムEコマースパラメータ50            |                                                               |
