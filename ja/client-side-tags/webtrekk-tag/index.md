---
title: Webtrekk タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで Webtrekk タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/webtrekk-tag/
---## 必要条件

* Webtrekk アカウント

## サポートされるバージョン

* v5.5.1（推奨）
* v4.4.7
* v4.4.4

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。タグを追加する一般的な手順については、[タグ概要]()の記事を読んでください。

タグを追加する際には、以下の構成を構成します：

* **タイトル**
  * デフォルトは「Webtrekk」です。
  * 好みに応じて説明的な名前に置き換えることができます。
* **ライブラリバージョン**
  * このリストから Webtrekk ピクセルのバージョンを選択します。例：トラッキングスクリプト。
* **トラック ID**
  * Webtrekk から受け取った数値のトラック ID を入力します。
  * トラック ID は Webtrekk ツールの **システム構成 &amp;gt; データ収集** の下に位置しています。
* **トラックドメイン**
  * Webtrekk ピクセルで指定されたトラッキング URL（https/http プロトコルを除く）を入力します。例：`track.XXXX.net`
* **TagIntegration 顧客 ID**
  * SafeTag 識別子を入力します。
  * これは `safetag` オブジェクトで定義されており、Webtrekk サーバーから TagIntegration ファイルをロードする場合に必要です。
* **TagIntegration ドメイン**
  * SafeTag ドメインを入力します。
  * Webtrekk サーバーから TagIntegration ファイルをロードする場合に必要です。
* **パラメーター最初**
  * リクエストで渡すパラメーターのリストを入力し、順序を指定します。
  * パラメーターはセミコロン（**;**）で区切ります。
* **サイトドメイン**
  * （オプション）追跡されるサイトのドメインを入力します。
* **リンクトラッキング**
  * 訪問のアクション/イベント、クリック、ダウンロードなどのトラッキング構成を以下から選択します。
    * **リンク**（デフォルト）
      * `href` 属性の値、たとえばクリックされたリンクの目的地ページ URL をアクション/イベント名として送信します。
      * 例えば、クリックされたリンクが `&lt;a href=&#34;example.htm&#34;&gt;ここをクリック&lt;/a&gt;` の場合、`example.htm` の値が渡されます。
    * **標準**
      * `name` 属性の値をアクション/イベント名として送信します。
      * 例えば、クリックされたリンクが `&lt;a href=&#34;example.htm&#34; name=&#34;example_name&#34;&gt;ここをクリック&lt;/a&gt;` の場合、`example_name` の値が渡されます。
    * **なし**
      * タグインスタンスのリンク/イベントトラッキングを無効にします。
* **リンクトラック属性**
  * **標準** トラッキングオプションのオプション構成です。
  * アクション/イベント名を割り当てるために `name` 属性の代わりに使用する HTML 属性を入力します。
  * 例えば、このリンク `&lt;a href=&#34;example.htm&#34; name=&#34;internal_id&#34; rel=&#34;example&#34;&gt;ここをクリック&lt;/a&gt;` では、`name` の代わりに `rel` を使用することができます。
* **リンクトラックパラメータ**
  * （オプション）**リンク** トラッキングオプションの構成です。
  * クリックされたリンクをトラッキングするためのクエリ文字列パラメータの名前を入力します。
  * 複数のパラメータを区切るにはコンマを使用します。
  * 例：`&lt;a href=&#34;example.htm?page=10&#34;&gt;10ページへ行く&lt;/a&gt;`
* **リンクトラックダウンロード**
  * トラックするファイルタイプのリストを入力します。
  * 複数のエントリを区切るにはセミコロンを使用します。
  * 例：`zip;raw;doc`
* **ピクセルサンプリング**：
  * Webtrekk に報告されるトラフィックの割合を制御します。
  * 数値を入力します。
* **HTTPS 強制**：
  * リクエストをセキュアとして送信するかどうかを選択します。
  * デフォルト構成は OFF です。
* **クッキー処理**
  * サイトの訪問をトラッキングするために使用するクッキーのタイプを選択します。
    * 第一者
      * デフォルト
      * 推奨）
      * サイトドメインによって構成されるクッキー値
    * 第三者
      * Webtrekk によって構成されるクッキー値
* **クッキードメイン**
  * 第一者クッキーにのみ適用されます。
  * トップレベルドメインが追加の識別子（`.co`、`.uk` など）で二重バレルされている場合、クッキーが正しく構成されるようにここで指定する必要があります。
* **mediaCode**
  * キャンペーンを識別してトラッキングするためのメディアコードパラメータを入力します。
* **mediaCodeCookie**
  * セッションごとに一度だけキャンペーンをトラッキングするためのメディアコードクッキーパラメータを入力します。
  * アドレスバーに `mediaCode` クエリパラメータがある場合、値を `sid` に構成します。
* **WT オブジェクト名**
  * `wt` で事前に入力されており、単一のタグインスタンスのデフォルトオブジェクトです。
  * 同じページ上で複数のタグインスタンスをロードしている場合は、それぞれのタグで一意のオブジェクト名に置き換えます。
* **ヒートマップトラッキング**
  * このタグインスタンスでヒートマップトラッキングを有効にするかどうかを選択します。
  * デフォルト構成は OFF です。
* **フォームトラッキング**
  * このタグインスタンスでフォームトラッキングを有効にするかどうかを選択します。
  * デフォルト構成は OFF です。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[ロードルール]()のドキュメントを参照してください。

推奨ルール：すべてのページ（デフォルト）

## データマッピング

データマッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)の指示を参照してください。
### 標準カテゴリ

これらの目的地にマッピングして、タグ構成を上書きするか動的に構成します。

これらのマッピングは、グローバルな `Webtrekk.js` 構成に適用されます。

|タグの目的地| 説明|
|---| ---|
|WT オブジェクト名|  &lt;ul&gt;&lt;li&gt;タグインスタンスを一意に識別するためのオブジェクト名。&lt;/li&gt;&lt;li&gt;デフォルト値は `wt` です。&lt;/li&gt;&lt;/ul&gt; |
|Cookie OptOut 名|  &lt;ul&gt;&lt;li&gt;`webtrekkOptOut` クッキーの名前&lt;/li&gt;&lt;/ul&gt; |
|Cookie OptOut 有効期間|  &lt;ul&gt;&lt;li&gt;`webtrekkoptout` クッキーの寿命&lt;/li&gt;&lt;/ul&gt; |
|最初に含めるパラメータ|  &lt;ul&gt;&lt;li&gt;セミコロンで区切られたパラメータのリスト。&lt;/li&gt;&lt;li&gt;変数にリストされた順序でパラメータが送信されます。&lt;/li&gt;&lt;/ul&gt; |
|プリレンダリングを無視|  &lt;ul&gt;&lt;li&gt;プリレンダリングされたページを追跡するかどうかを決定するフラグ（ブール値）&lt;/li&gt;&lt;/ul&gt; |
|フォームパス分析|  &lt;ul&gt;&lt;li&gt;フォームフィールドの追跡を有効または無効にするフラグ（ブール値）&lt;/li&gt;&lt;/ul&gt; |
|tabBrowsing|  &lt;ul&gt;&lt;li&gt;ブラウザタブのビューを追跡するためのフラグ（ブール値）。&lt;/li&gt;&lt;li&gt;デフォルト値は false です&lt;/li&gt;&lt;/ul&gt; |
|globalVisitorIds|
|execRTA|  &lt;ul&gt;&lt;li&gt;Webtrekkのリアルタイム入札（RTB）サービスを有効または無効にするフラグ（ブール値）&lt;/li&gt;&lt;/ul&gt; |
|execCDB|  &lt;ul&gt;&lt;li&gt;Webtrekkのクロスデバイスブリッジ（CDB）技術を有効または無効にするフラグ（ブール値）&lt;/li&gt;&lt;/ul&gt; |
|useCDBCache|  &lt;ul&gt;&lt;li&gt;画像キャッシュクッキーの使用を有効または無効にするフラグ（ブール値）&lt;/li&gt;&lt;/ul&gt; |
|useCDBScript|
|requestLimitAmount|  &lt;ul&gt;&lt;li&gt;送信できる最大リクエスト数&lt;/li&gt;&lt;/ul&gt; |
|requestLimitTime|  &lt;ul&gt;&lt;li&gt;最大リクエスト数を送信する許容時間制限&lt;/li&gt;&lt;/ul&gt; |
|Track ID|  &lt;ul&gt;&lt;li&gt;Webtrekkから受け取ったトラッキングピクセルの数値識別子。&lt;/li&gt;&lt;li&gt;Track IDはWebtrekkツールの **システム構成 &amp;gt; データ収集** で見つけることができます。&lt;/li&gt;&lt;/ul&gt; |
|Track Domain|  &lt;ul&gt;&lt;li&gt;Webtrekkピクセルで指定されたトラッキングURL（https/httpプロトコルを除く）。&lt;/li&gt;&lt;/ul&gt; |
|Site Domain|  &lt;ul&gt;&lt;li&gt;追跡されるサイトのドメイン。&lt;/li&gt;&lt;/ul&gt; |
|Link Tracking|  &lt;ul&gt;&lt;li&gt;訪問のアクション、クリック、ダウンロードを追跡するためのイベント追跡構成。&lt;/li&gt;&lt;li&gt;Webtrekkは「Link」と「Standard」の2つのオプションをサポートしています。&lt;/li&gt;&lt;/ul&gt; |
|Link Track Attribute|  &lt;ul&gt;&lt;li&gt;「Standard」追跡オプションに適用されます。&lt;/li&gt;&lt;li&gt;この属性はイベント/アクションの名前を決定するために使用されます。&lt;/li&gt;&lt;li&gt;この目的地にマッピングするとデフォルトの「name」が上書きされます。&lt;/li&gt;&lt;/ul&gt; |
|Link Track Params|  &lt;ul&gt;&lt;li&gt;グローバル構成の「Link」追跡オプションに適用されます。&lt;/li&gt;&lt;li&gt;この目的地にマッピングすると、クリックされたリンクを追跡するためのクエリ文字列パラメータが送信されます。&lt;/li&gt;&lt;/ul&gt; |
|Link Track Pattern|  &lt;ul&gt;&lt;li&gt;Link Track Parameterのクエリ文字列から望ましくないパラメータを除外するための正規表現。&lt;/li&gt;&lt;/ul&gt; |
|Link Track Replace|  &lt;ul&gt;&lt;li&gt;フィルタリングされたパラメータを置き換えるための置換文字。&lt;/li&gt;&lt;/ul&gt; |
|Link Track Ignore Pattern|  &lt;ul&gt;&lt;li&gt;個々のリンクを追跡から除外するための正規表現&lt;/li&gt;&lt;/ul&gt; |
|No Delay Link Track Attribute|  &lt;ul&gt;&lt;li&gt;このパラメータで明示的にタグ付けされたリンクの遅延を無効にします&lt;/li&gt;&lt;/ul&gt; |
|Link Track Downloads|  &lt;ul&gt;&lt;li&gt;グローバル構成でダウンロードを追跡するために追跡したいファイルタイプのリスト。&lt;/li&gt;&lt;li&gt;例：`zip;raw;doc`&lt;/li&gt;&lt;/ul&gt; |
|Pixel Sampling|  &lt;ul&gt;&lt;li&gt;Webtrekkに報告されるトラフィックの割合。&lt;/li&gt;&lt;/ul&gt; |
|Force HTTPS|  &lt;ul&gt;&lt;li&gt;リクエストをセキュアとして強制送信します。&lt;/li&gt;&lt;li&gt;データソースにはアクティベーションのための値 `1` が含まれている必要があります。&lt;/li&gt;&lt;/ul&gt; |
|Cookie Handling|  &lt;ul&gt;&lt;li&gt;サイトの訪問を追跡するためのファーストパーティまたはサードパーティクッキー。&lt;/li&gt;&lt;li&gt;ファーストパーティがデフォルトで推奨されます。&lt;/li&gt;&lt;/ul&gt; |
|Cookie Domain|  &lt;ul&gt;&lt;li&gt;`firstparty` クッキーにのみ適用されます。&lt;/li&gt;&lt;li&gt;トップレベルドメインが二重バレルである場合、この目的地にマッピングします。たとえば、`.co`、`.uk`などの追加識別子で接尾辞が付けられています。&lt;/li&gt;&lt;/ul&gt; |
|contentId|  &lt;ul&gt;&lt;li&gt;URLではなく、そのユニークな名前によってページを識別します。&lt;/li&gt;&lt;/ul&gt; |
|Heat map|  &lt;ul&gt;&lt;li&gt;グローバル構成でヒートマップを有効/無効にします。&lt;/li&gt;&lt;li&gt;データソースの値はアクティベーションのために `1` と等しくなければなりません。&lt;/li&gt;&lt;/ul&gt; |
|Form|  &lt;ul&gt;&lt;li&gt;グローバル構成でフォーム追跡を有効/無効にします。&lt;/li&gt;&lt;li&gt;データソースの値はアクティベーションのために `1` と等しくなければなりません。&lt;/li&gt;&lt;/ul&gt; |
|executePluginFuntion|  &lt;ul&gt;&lt;li&gt;プラグイン機能のリスト&lt;/li&gt;&lt;/ul&gt; |
|Media Code|  &lt;ul&gt;&lt;li&gt;キャンペーンを追跡するためのパラメータ。&lt;/li&gt;&lt;/ul&gt; |
|Media Code cookie|  &lt;ul&gt;&lt;li&gt;セッションごとにキャンペーンを1回のみ追跡するためのパラメータ。&lt;/li&gt;&lt;/ul&gt; |
|SafeTag Async|  &lt;ul&gt;&lt;li&gt;タグを非同期でロードするかどうかを決定するフラグ（ブール値）&lt;/li&gt;&lt;/ul&gt; |
|SafeTag Timeout|  &lt;ul&gt;&lt;li&gt;TagIntegrationファイルのロードを待つ最大時間。&lt;/li&gt;&lt;/ul&gt; |
|SafeTag Domain|  &lt;ul&gt;&lt;li&gt;TagIntegrationドメイン&lt;/li&gt;&lt;/ul&gt; |
|SafeTag Customer ID|  &lt;ul&gt;&lt;li&gt;TagIntegrationの顧客識別子&lt;/li&gt;&lt;/ul&gt; |
|SafeTag Custom Domain|  &lt;ul&gt;&lt;li&gt;TagIntegrationファイルをロードするカスタムドメイン&lt;/li&gt;&lt;/ul&gt; |
|SafeTag CustomPath|  &lt;ul&gt;&lt;li&gt;カスタムドメインのJavaScriptファイルのパス&lt;/li&gt;&lt;/ul&gt; |
|SafeTag Option [Object]|  &lt;ul&gt;&lt;li&gt;追加のTagIntegration情報&lt;/li&gt;&lt;/ul&gt; |
|SafeTag Option|
|Custom wt config item|

### 一般カテゴリ

訪問ID、セッション、カテゴリなどのカスタム/オプションパラメータの報告のためにこれらの目的地にマッピングします。

|タグの目的地| 説明|
|---| ---|
|カスタム訪問ID|  &lt;ul&gt;&lt;li&gt;一意の訪問識別子を送信するためにこの目的地にマッピングします。&lt;/li&gt;&lt;/ul&gt; |
|URMカテゴリ|  &lt;ul&gt;&lt;li&gt;あなたのWebtrekkツールのURMカテゴリ&lt;/li&gt;&lt;/ul&gt; |
|Email RID|  &lt;ul&gt;&lt;li&gt;メール受信者ID&lt;/li&gt;&lt;/ul&gt; |
|Email Opt-In|  &lt;ul&gt;&lt;li&gt;メールオプトインステータス。&lt;/li&gt;&lt;li&gt;可能な値:  &lt;ul&gt;&lt;li&gt;`1`（はい）&lt;/li&gt;&lt;li&gt;`2`（いいえ）&lt;/li&gt;&lt;li&gt;`3`（不明）&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|性別|  &lt;ul&gt;&lt;li&gt;性別&lt;/li&gt;&lt;li&gt;可能な値:  &lt;ul&gt;&lt;li&gt;`1`（男性）&lt;/li&gt;&lt;li&gt;`2`（女性）&lt;/li&gt;&lt;li&gt;`3`（不明） &lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|誕生日|  &lt;ul&gt;&lt;li&gt;生年月日（`YYYYMMDD`）&lt;/li&gt;&lt;/ul&gt; |
|誕生年|  &lt;ul&gt;&lt;li&gt;生年（`YYYY`）&lt;/li&gt;&lt;/ul&gt; |
|誕生月|  &lt;ul&gt;&lt;li&gt;誕生月（`MM`）&lt;/li&gt;&lt;/ul&gt; |
|誕生日|  &lt;ul&gt;&lt;li&gt;誕生日（`DD`）&lt;/li&gt;&lt;/ul&gt; |
|CRMカテゴリ1から10|  &lt;ul&gt;&lt;li&gt;会員タイプ、年齢、性別などのCRM情報を送信するためのカスタムカテゴリ。&lt;/li&gt;&lt;li&gt;マッピングする前に、カテゴリがあなたのWebtrekkツールで定義されていることを確認してください。&lt;/li&gt;&lt;/ul&gt; |
|カスタムセッションパラメータ1から10|  &lt;ul&gt;&lt;li&gt;ログインステータス、登録ステータス、A/Bテストのテストグループなどの追加の訪問/セッション情報を送信するためのカスタムパラメータ。&lt;/li&gt;&lt;li&gt;マッピングする前に、セッションパラメータがあなたのWebtrekkツールで定義されていることを確認してください。&lt;/li&gt;&lt;/ul&gt; |

### ページデータカテゴリ

|タグの目的地| 説明|
|---| ---|
|ページコンテンツID|  &lt;ul&gt;&lt;li&gt;URLではなく、そのユニークな名前によってページを識別し、ページ固有の構成で構成されます。&lt;/li&gt;&lt;/ul&gt; |
|コンテンツグループ1から25|  &lt;ul&gt;&lt;li&gt;ページに最大50のカスタムパラメータを送信するためにこれらの目的地にマッピングします。&lt;/li&gt;&lt;li&gt;マッピングするコンテンツグループがあなたのWebtrekkツールで定義されていることも確認してください。&lt;/li&gt;&lt;/ul&gt; |
|カスタムパラメータ1から50|  &lt;ul&gt;&lt;li&gt;ページに最大50のカスタムパラメータを送信するためにこれらの目的地にマッピングします。&lt;/li&gt;&lt;/ul&gt; |
### 検索とフォーム追跡

内部検索やフォーム入力パラメータを送信するための目的地をマッピングします。

|タグの目的地| 説明|
|---| ---|
|内部検索|  &lt;ul&gt;&lt;li&gt;訪問がサイトを検索するために使用した検索キーワード/用語&lt;/li&gt;&lt;/ul&gt; |
|フォーム追跡|  &lt;ul&gt;&lt;li&gt;ページ固有の構成でフォーム追跡を有効/無効にする&lt;/li&gt;&lt;li&gt;データソースは有効化のために値 `1` を、無効化のために を含む必要があります。&lt;/li&gt;&lt;/ul&gt; |
|フォーム属性|  &lt;ul&gt;&lt;li&gt;この属性はフォームの名前を決定するために使用されます。&lt;/li&gt;&lt;li&gt;この目的地へのマッピングはデフォルトの &#34;name&#34; 属性を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|フォーム値属性|  &lt;ul&gt;&lt;li&gt;この属性はフォームフィールドが &#39;radio&#39; や &#39;checkbox&#39; の場合のフォームの名前を決定するために使用されます。&lt;/li&gt;&lt;li&gt;この目的地へのマッピングはデフォルトの `value` 属性を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|フォームフィールド属性| ---|
|全内容フォーム追跡| 自由記述フィールドの最初の30文字を送信します。|
|匿名フォーム追跡|  &lt;ul&gt;&lt;li&gt;フォームの内容はWebtrekkに送信されません。&lt;/li&gt;&lt;li&gt;この目的地へのマッピングによりフォームデータが匿名化されます。&lt;/li&gt;&lt;/ul&gt; |
|フォームHTML ID|  &lt;ul&gt;&lt;li&gt;Ajaxによってリロードされたフォームを追跡する方法。&lt;/li&gt;&lt;li&gt;この目的地へのマッピングによりその方法が呼び出されます&lt;/li&gt;&lt;/ul&gt; |

### クリック追跡

|タグの目的地| 説明|
|---| ---|
|ヒートマップ|  &lt;ul&gt;&lt;li&gt;ページ固有の構成でヒートマップを有効/無効にする。&lt;/li&gt;&lt;li&gt;データソースの値は有効化のために `1` と等しくなければならず、無効化のために と等しくなければなりません。&lt;/li&gt;&lt;/ul&gt; |
|ヒートマップ参照点ID|  &lt;ul&gt;&lt;li&gt;ヒートマップの参照点として使用される要素のID。&lt;/li&gt;&lt;/ul&gt; |
|リンク追跡|  &lt;ul&gt;&lt;li&gt;ページ固有の構成でのイベント追跡構成。&lt;/li&gt;&lt;li&gt;Webtrekkは &#39;Link&#39; と &#39;Standard&#39; の構成をサポートしています。&lt;/li&gt;&lt;/ul&gt; |
|リンク追跡属性|  &lt;ul&gt;&lt;li&gt;ページ固有の構成での &#34;Standard&#34; 追跡オプションに適用されます。&lt;/li&gt;&lt;li&gt;この属性はイベント/アクションの名前を決定するために使用されます。&lt;/li&gt;&lt;li&gt;この目的地へのマッピングはデフォルトの &#34;name&#34; を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|リンク追跡パラメータ|  &lt;ul&gt;&lt;li&gt;ページ固有の構成での &#34;Link&#34; 追跡オプションに適用されます。&lt;/li&gt;&lt;li&gt;この目的地へのマッピングにより追跡されたリンクのクエリ文字列パラメータが送信されます。&lt;/li&gt;&lt;/ul&gt; |
|リンク追跡パターン|  &lt;ul&gt;&lt;li&gt;リンク追跡パラメータのクエリ文字列から望ましくないパラメータを除外するための正規表現。&lt;/li&gt;&lt;li&gt;ページ固有の構成に適用されます。&lt;/li&gt;&lt;/ul&gt; |
|リンク追跡置換|  &lt;ul&gt;&lt;li&gt;リンク追跡パラメータでフィルタリングされたパラメータを置換するための置換文字。&lt;/li&gt;&lt;li&gt;ページ固有の構成に適用されます。&lt;/li&gt;&lt;/ul&gt; |
|リンク追跡ダウンロード|  &lt;ul&gt;&lt;li&gt;ダウンロードの追跡を希望するファイルタイプのリスト。&lt;/li&gt;&lt;li&gt;ページ固有の構成に適用されます。&lt;/li&gt;&lt;li&gt;例: `zip;raw;doc`&lt;/li&gt;&lt;/ul&gt; |
|カスタム utag.link 追跡用リンクID|  &lt;ul&gt;&lt;li&gt;追跡されるリンクの名前。&lt;/li&gt;&lt;/ul&gt; |
|カスタムクリックパラメータ1から10|  &lt;ul&gt;&lt;li&gt;クリック追跡のためのカスタムパラメータ。&lt;/li&gt;&lt;li&gt;カスタムクリックパラメータを送信するためには、リンクID値をマッピングする必要があります。&lt;/li&gt;&lt;li&gt;マッピングする前に、パラメータがWebtrekkツールで定義されていることを確認してください。&lt;/li&gt;&lt;/ul&gt; |

### キャンペーン追跡

オプショナルおよびカスタムキャンペーンパラメータを送信するための目的地をマッピングします

これらのマッピングはページ固有の構成に適用されます。

|タグの目的地| 説明|
|---| ---|
|メディアコード|  &lt;ul&gt;&lt;li&gt;キャンペーン追跡のためのパラメータ。&lt;/li&gt;&lt;/ul&gt; |
|メディアコードクッキー|  &lt;ul&gt;&lt;li&gt;セッションごとに1回だけキャンペーンを追跡するためのパラメータ。&lt;/li&gt;&lt;/ul&gt; |
|キャンペーンID|  &lt;ul&gt;&lt;li&gt;メディアコードパラメータに続いて `%3D` とパラメータ値が続きます&lt;/li&gt;&lt;/ul&gt; |
|キャンペーンアクション|  &lt;ul&gt;&lt;li&gt;訪問のキャンペーンへの反応が &#39;view&#39; か &#39;click&#39; かを決定します。&lt;/li&gt;&lt;/ul&gt; |
|カスタムキャンペーンパラメータ1から10|  &lt;ul&gt;&lt;li&gt;キャンペーン追跡のためのカスタムパラメータ。&lt;/li&gt;&lt;li&gt;マッピングする前に、パラメータがWebtrekkツールで定義されていることを確認してください。&lt;/li&gt;&lt;/ul&gt; |

### E-コマースカテゴリ

WebtrekkタグはE-コマース対応であり、デフォルトの [E-Commerce Extension]() マッピングを自動的に使用します。次の場合を除き、手動でのマッピングは一般的に必要ありません：

* 拡張マッピングを上書きしたい場合
* 拡張機能で提供されていないE-コマース変数が必要な場合

|タグの目的地| 説明| E-コマース拡張マッピング |
|---| ---| ---|
|注文ID|  &lt;ul&gt;&lt;li&gt;最終注文の一意の識別子&lt;/li&gt;&lt;/ul&gt; | `_corder`|
|注文合計|  &lt;ul&gt;&lt;li&gt;送料と税後の合計金額。&lt;/li&gt;&lt;/ul&gt; | `_ctotal`|
|通貨|  &lt;ul&gt;&lt;li&gt;顧客が支払いに使用した通貨&lt;/li&gt;&lt;/ul&gt; | `_ccurrency`|
|クーポン値|  &lt;ul&gt;&lt;li&gt;注文で使用されたクーポンの値&lt;/li&gt;&lt;/ul&gt; | N//A|
|製品名リスト|  &lt;ul&gt;&lt;li&gt;製品配列の各製品の名前&lt;/li&gt;&lt;/ul&gt; | `_cprodname`|
|製品数量リスト|  &lt;ul&gt;&lt;li&gt;製品配列の各製品の数量&lt;/li&gt;&lt;/ul&gt; | `_cquan`|
|製品価格リスト|  &lt;ul&gt;&lt;li&gt;製品配列の各製品の単価&lt;/li&gt;&lt;/ul&gt; | `_cprice`|
|製品カテゴリリスト (productCategories[1])|  &lt;ul&gt;&lt;li&gt;製品配列の各製品のカテゴリ&lt;/li&gt;&lt;/ul&gt; | `_ccat`|
|製品ブランドリスト (productCategory[2])|  &lt;ul&gt;&lt;li&gt;製品配列の各製品のブランド&lt;/li&gt;&lt;/ul&gt; | `_cbrand`|
|製品サブカテゴリリスト (productCategory[3])|  &lt;ul&gt;&lt;li&gt;製品配列の各製品のサブカテゴリ&lt;/li&gt;&lt;/ul&gt; | `_ccat2`|
|製品ステータス|  &lt;ul&gt;&lt;li&gt;製品が閲覧されたか、カートに追加されたか、カートからチェックアウトされたかを示します。&lt;/li&gt;&lt;/ul&gt; | N/A|
|製品カテゴリ1から25|  &lt;ul&gt;&lt;li&gt;製品が一度だけ関連付けられるカスタムカテゴリ。&lt;/li&gt;&lt;li&gt;最大25のユニークなカテゴリをマッピングできます。&lt;/li&gt;&lt;li&gt;マッピングする前に、製品カテゴリがWebtrekkツールで定義されていることを確認してください。&lt;/li&gt;&lt;/ul&gt; | N/A|
|カスタムE-コマースパラメータ1から50|  &lt;ul&gt;&lt;li&gt;追加の製品および注文レベルのデータを送信するためのカスタムパラメータ。&lt;/li&gt;&lt;li&gt;最大50のユニークなパラメータをマッピングできます。&lt;/li&gt;&lt;li&gt;マッピングする前に、パラメータがWebtrekkツールで定義されていることを確認してください。&lt;/li&gt;&lt;/ul&gt; | N/A|

