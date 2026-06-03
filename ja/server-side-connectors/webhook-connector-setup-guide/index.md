---
title: Webhookコネクタ構成ガイド
description: この記事では、Webhookコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/webhook-connector-setup-guide/
---
## 必要条件

* イベントデータ用にEventStreamが有効になっているTealiumアカウント
* 訪問データ用にAudienceStreamが有効になっているTealiumアカウント

## webhookコネクタについて

Webhookコネクタを使用すると、カスタマイズされたHTTPリクエストを使用してデータをベンダーに送信し、URL、URLパラメータ、ヘッダー、クッキー、ボディコンテンツタイプ、ボディデータなど、HTTPリクエストのすべての側面を構成できます。Webhookはバッチ処理と、複雑で動的なデータ形式を処理するために設計された強力なテンプレート機能もサポートしています。

ベンダーの認証要件に基づいて選択できるWebhookコネクタは4種類あります：

* **Webhook** (BasicAuth)：認証が不要、またはユーザー名とパスワードのみの基本認証が必要なサービス用。
* **Webhook OAuth2** (3-Legged)：ユーザーがサービスにログインしてアクセストークンを取得する必要があります。
* **Webhook OAuth2** (2-Legged)：ユーザーのサービスへのログインが不要です。認証に必要な情報でWebhookが構成されます。
* **Webhook JWT**：JSON Webトークン認証を使用します。ユーザーのサービスへのログインが不要です。認証に必要な情報でWebhookが構成されます。

Webhook OAuth2は、OAuth 2.0認証を明示的に要求するサービスに使用されます。

始めるには、コネクタマーケットプレイスにアクセスし、使用したいWebhookインスタンスを追加します。コネクタを追加する一般的な手順については、[コネクタ概要]()を参照してください。

次のセクションでは、各タイプのWebhookコネクタの構成について説明します。

### Webhook (BasicAuth)の構成

このWebhookは、HTTPヘッダーフィールド**Authorization**を使用して基本的なHTTP認証をサポートしています。認証情報は`{username}:{password}`のBase64エンコードされた文字列として渡されます。

BasicAuth Webhook構成のための以下の構成を使用します：

* **名前**：(必須) Webhookの説明的なタイトルを入力します。
* **BasicAuth ユーザー名**：Webhookの認証用ユーザー名を入力します。
* **BasicAuth パスワード**：Webhookの認証用パスワードを入力します。

**次へ**をクリックするか、**アクション**タブに進みます。

### Webhook OAuth2 (3-Legged)の構成

このWebhookのOAuth実装はサーバーサイドアプリケーションのみをサポートしています。

OAuth 2.0サービスにWebアプリケーションを登録することを忘れないでください。アプリケーションはリダイレクトURLを許可するように構成する必要があります：`https://my.tealiumiq.com/oauth/webhook/callback.html`

OAuth2 (3-legged) Webhook構成のための以下の構成を使用します：

* **名前**
  * (必須) Webhookの説明的なタイトルを入力します。
* **クライアントID**
  * (必須) OAuthサービスから割り当てられたアプリケーションのクライアント識別子を入力します。
* **クライアントシークレット**
  * (必須) OAuthサービスから割り当てられたアプリケーションのクライアントシークレットを入力します。
* **スコープ**
  * アプリケーションへのアクセスを要求する許可のタイプを選択します。
* **認証URL**
  * (必須) ユーザーを認証後にリダイレクトするURLを入力します。
* **認証URLクエリパラメータ**
  * 認証URLのための1つ以上の名前-値ペアを選択します。
  * 複数のペアをアンパサンド(`&amp;`)を使用して区切ります。
  * 先頭にアンパサンド(`&amp;`)を使用しないでください。
    * 正しい: `access_type=offline&amp;prompt=consent`
    * 誤り: `&amp;access_type=offline&amp;prompt=consent`
* **アクセストークンURL**
  * (必須) リフレッシュトークンを取得するためのトークンURLを入力します。
* **認証トークンの位置**
  * 認証トークンを配置する場所を指定します。
* **認証ヘッダープレフィックス**
  * デフォルト値は`Bearer`です。
  * 新しい値を指定して上書きします（一部のOAuth2サービスで必要です）。

接続をテストするために**接続を確立**をクリックします。

**次へ**をクリックするか、**アクション**タブに進みます。

### Webhook OAuth2 (2-Legged)の構成

TealiumのWebhook OAuth2コネクタは、OAuth2 Two-Legged認証を必要とするAPIに完全にカスタマイズされたデータをHTTPリクエストとして送信することができます。クライアント資格情報とリソース所有者のパスワード資格情報の付与をサポートしています。

コネクタを追加した後、OAuth2 2-Legged Webhook構成のための以下の構成を使用します：

* **名前**
  * (必須) Webhookの説明的なタイトルを入力します。
* **アクセストークンURL**
  * (必須) アクセストークンを要求するAPIエンドポイントURLを入力します。
* **クライアントID**
  * WebアプリケーションのクライアントIDを入力します。
  * クライアントIDは、クライアント資格情報の付与タイプを使用する場合に必要です。
* **クライアントシークレット**
  * Webアプリケーションのクライアントシークレットを入力します。
  * クライアントシークレットは、クライアント資格情報の付与タイプを使用する場合に必要です。
* **ユーザー名**
  * ユーザー名を入力します。
  * ユーザー名は、パスワードの付与タイプを使用する場合に必要です。
  * トークンエンドポイントが基本認証ヘッダーも必要とする場合は、クライアント認証IDとクライアント認証シークレットを入力します。
* **パスワード**
  * パスワードを入力します。
  * パスワードは、パスワードの付与タイプを使用する場合に必要です。
* **クライアント認証ID**
  * 認証ヘッダーの一部として送信するクライアントID。
* **クライアント認証シークレット**
  * 認証ヘッダーの一部として送信するクライアントシークレット。
* **スコープ**
  * 要求する権限の範囲を選択します（一部のOAuth2サービスで必要です）。
* **追加の認証パラメータ**
  * 追加の認証パラメータを追加します（一部のOAuth2サービスで必要です）。
  * 複数のパラメータを`&amp;`で区切ります。
* **認証URL**
  * (必須) 認証コードを要求するAPIエンドポイントURLを入力します。
* **認証トークンの位置**
  * 認証トークンを配置する場所を指定します。
* **認証ヘッダープレフィックス**
  * デフォルト値は`Bearer`です。
  * 新しい値を指定して上書きします（一部のOAuth2サービスで必要です）。
* **カスタムヘッダー**
  * 認証コールに追加したいカスタムヘッダーのキーと値のペアをコンマ区切りで指定します。たとえば、`&#39;var1:value1&#39;,&#39;var2:value2&#39;,&#39;var3:value3,value4&#39;,&#39;var4:{&#34;field&#34;: {&#34;name&#34;: &#34;TEST&#34;, &#34;version&#34;: &#34;1.0.0&#34;}}&#39;`は次のようになります：
  ```
  VERSION: HTTP/1.1
  CONNECTION: close
  ACCEPT-ENCODING: gzip
  X-HEADER-KEY: header_value
  VAR1: value1
  VAR2: value2
  VAR3: value3, value4
  VAR4: {&#34;field&#34;: {&#34;name&#34;: &#34;TEST&#34;, &#34;version&#34;: &#34;1.0.0&#34;}}
  COOKIE: cookie_key=cookie_value
  CONTENT-TYPE: application/json; charset=UTF-8
  USER-AGENT: Apache-HttpClient/4.5.1 (Java/1.8.0_111)
  CONTENT-LENGTH: 13
  ```
* **カスタムボディ値**
  * キーと値のペアをコンマ区切りで定義します。たとえば、`&#39;var1:value1&#39;,&#39;var2:value2&#39;,&#39;var3:varx,vary&#39;`。これらは**ボディコンテンツタイプ**フィールドで構成された形式に従ってボディに使用されます。
* **ボディコンテンツタイプ**
  * ボディコンテンツタイプを指定します。
* **認証値の位置**
  * 認証値（クライアントID、クライアントシークレット、ユーザー名、パスワード、スコープ）の位置を指定します。

**次へ**をクリックするか、**アクション**タブに進みます。

### Webhook (JWT)の構成

このWebhookは、JSON Webトークン（JWT）を使用して認証をサポートしています。

Webhook (JWT)構成のための以下の構成を使用します：

* **名前**
  * 必須
  * Webhookの説明的なタイトルを入力します。
* **JWTトークン**
  * JSON Webトークンを入力します。

**次へ**をクリックするか、**アクション**タブに進みます。
## すべてのWebhookアクションのアクションパラメータ

以下のパラメータは、すべてのWebhookアクションで利用可能です。

| 入力フィールド        | 必須/任意      | テンプレートサポート | 備考         |
|:-------------------|:------------|:-----------------|:-------------|
| メソッド             | 必須     | 次のメソッドをサポート: &lt;ul&gt;&lt;li&gt;GET&lt;/li&gt;&lt;li&gt;POST&lt;/li&gt;&lt;li&gt;PUT&lt;/li&gt;&lt;li&gt;DELETE&lt;/li&gt;&lt;li&gt;PATCH&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                       |
| URL                | 必須                                                                                                                                                                     | ✔                | &lt;ul&gt;&lt;li&gt;リクエストを送信するURLを提供する&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                            |
| URLパラメータ     | 任意                                                                                                                                                                     | ✔                | &lt;ul&gt;&lt;li&gt;**Map** ドロップダウンリストから、送信したい属性の値を選択します。&lt;/li&gt;&lt;li&gt;**To** フィールドに、構成するURLパラメータの名前を入力します。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                    |
| ヘッダー            | Webhook（BasicAuth）では任意、[Webhook OAuth2]()では必須 | ✔                | &lt;ul&gt;&lt;li&gt;**Map** ドロップダウンリストから、送信したい属性の値を選択します。&lt;/li&gt;&lt;li&gt;**To** フィールドに、ヘッダー名を入力します。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                     |
| クッキー            | 任意                                                                                                                                                                     | ✔                | &lt;ul&gt;&lt;li&gt;**Map** ドロップダウンリストから、送信したい属性の値を選択します。&lt;/li&gt;&lt;li&gt;**To** フィールドに、クッキー名を入力します。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                     |
| ボディコンテンツタイプ  | 任意                                                                                                                                                                     |                  | &lt;ul&gt;&lt;li&gt;`Content-Type` ヘッダーを指定します。&lt;/li&gt;&lt;li&gt;すべてのタイプはUTF-8文字セットを使用します。&lt;/li&gt;&lt;li&gt;GETメソッドの場合はこの構成を無視します。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                             |
| ボディデータ          | 任意                                                                                                                                                                     | ✔                | &lt;ul&gt;&lt;li&gt;**HTTPリクエストを介してカスタマイズされたデータを送信** アクションのみサポートされます&lt;/li&gt;&lt;li&gt;GETメソッドの場合はこの構成を無視します。&lt;/li&gt;&lt;li&gt;ボディコンテンツタイプが `application/x-www-form-urlencoded` の場合は、名前/値のペアを提供します&lt;/li&gt;&lt;li&gt;より複雑なペイロードの場合は、テンプレート名を提供します。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                 |
| バッチングオプション   | 任意                                                                                                                                                                     | ✔                | &lt;ul&gt;&lt;li&gt;レコード数の最大値は10から10,000まで。&lt;/li&gt;&lt;li&gt;有効期限は、5分から60分まで。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                        |
| テンプレート変数 | 任意                                                                                                                                                                     |                  | &lt;ul&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                             |
| テンプレート          | 任意                                                                                                                                                                     |                  | &lt;ul&gt;&lt;li&gt;詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;各テンプレートには一意の名前が必要です&lt;/li&gt;&lt;li&gt;サポートされているフィールドにテンプレートを注入するには、その名前を二重中括弧で囲んで参照します&lt;/li&gt;&lt;li&gt;URL、URLパラメータ、ヘッダー、クッキー、またはボディデータフィールドにテンプレートを注入できます&lt;/li&gt;&lt;/ul&gt; |

**テンプレートサポートについて**: カスタムテンプレートからフィールド値を入力することができます。たとえば、テンプレートが `some-template` という名前の場合、その内容はフィールドに `{{some-template}}` と参照することで注入されます。

## アクション

| アクション名    | 説明    | Webhook (BasicAuth) | Webhook OAuth2 |
|:--------|:--------|:------|:-----|
| [HTTPリクエストを介してイベントデータを送信](#send-event-data-via-http-request)  | イベントオブジェクト全体を、URLエンコードされたJSON文字列またはJSONペイロードとして送信します。     | ✓      | ✓     |
| [HTTPリクエストを介して訪問データを送信](#send-visitor-data-via-http-request)  | 訪問プロファイルオブジェクト全体を、URLエンコードされたJSON文字列またはJSONペイロードとして送信します。 | ✓    | ✓      |
| [HTTPリクエストを介してカスタマイズされたデータを送信（高度）](#send-custom-data-via-http-request-advanced)    | マッピングで指定された個々のイベント/訪問属性を送信します。          | ✓      | ✓       |
| [HTTPリクエストを介してバッチデータを送信](#send-batched-data-via-http-request)  | イベントオブジェクト全体を、URLエンコードされたJSON文字列またはJSONペイロードとして送信します。     | ✓      | ✓     |
| [HTTPリクエストを介してバッチカスタマイズデータを送信（高度）](#send-batched-customized-data-via-http-request-advanced) | マッピングで指定されたバッチイベント/訪問属性を送信します。    | ✓      | ✓          |

**次へ**をクリックするか、**アクション**タブに進んでください。ここでコネクタアクションの構成を行います。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### HTTPリクエストを介してイベントデータを送信


#### パラメータ

| パラメータ      | 説明 |
|:------------------|:-------------|
| メソッド       | &lt;ul&gt;&lt;li&gt;(必須) リクエストメソッドを選択します。&lt;/li&gt;&lt;li&gt;**GET** が選択された場合、イベントデータは `data` キーを持つ JSON URLエンコードされたクエリ文字列パラメータとして配信されます。&lt;/li&gt;&lt;/ul&gt;     |
| URL       | &lt;ul&gt;&lt;li&gt;(必須) リクエストを送信するURLを提供します。&lt;/li&gt;&lt;li&gt;テンプレートサポート: テンプレート名を参照してURLを生成します。&lt;/li&gt;&lt;/ul&gt;    |
| URL パラメータ     | &lt;ul&gt;&lt;li&gt;(オプション) URLに追加するパラメータを提供します。&lt;/li&gt;&lt;li&gt;テンプレートサポート: テンプレート名を参照してパラメータ値を生成します。&lt;/li&gt;&lt;/ul&gt;  |
| ヘッダー      | &lt;ul&gt;&lt;li&gt;(オプション) HTTPヘッダー値をヘッダー名にマッピングします。&lt;/li&gt;&lt;li&gt;テンプレートサポート: テンプレート名を参照してヘッダー値を生成します。&lt;/li&gt;&lt;/ul&gt;     |
| クッキー     | &lt;ul&gt;&lt;li&gt;(オプション) クッキー値をクッキー名にマッピングします。&lt;/li&gt;&lt;li&gt;クッキーは単一のHTTPヘッダー値として追加されます。例: `Cookie: name1=value1; name2=value2`&lt;/li&gt;&lt;li&gt;テンプレートサポート: テンプレート名を参照してクッキー値を生成します。&lt;/li&gt;&lt;/ul&gt;     |
| ボディコンテンツタイプ     | &lt;ul&gt;&lt;li&gt;(オプション) 利用可能なタイプを選択するか、カスタム値を提供します。&lt;/li&gt;&lt;li&gt;すべてのタイプはUTF-8エンコードされ、ヘッダーとして追加されます。例: `Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;ボディデータが提供される場合、コンテンツタイプが必要です。&lt;/li&gt;&lt;/ul&gt;      |
| テンプレート変数    | &lt;ul&gt;&lt;li&gt;(オプション) テンプレートのデータ入力としてテンプレート変数を提供します。詳細は  を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を名前付けします。例: `items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt;   |
| テンプレート             | &lt;ul&gt;&lt;li&gt;(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。詳細は  を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例: `{{SomeTemplateName}}`&lt;/li&gt;&lt;li&gt;OAuthを使用する場合、テンプレート変数 `{{webhook_access_token}}` は認証リクエストによって返されるトークンを指します。&lt;/li&gt;&lt;/ul&gt; |
| 属性名の印刷 | &lt;ul&gt;&lt;li&gt;属性名が更新された場合、ペイロードに名前が反映されます。&lt;/li&gt;&lt;/ul&gt;   |
| リダイレクション           | &lt;ul&gt;&lt;li&gt;メソッドがGETの場合のみリダイレクションを許可します。&lt;/li&gt;&lt;/ul&gt;  |

### HTTPリクエストを介して訪問データを送信

#### パラメータ

| パラメータ   | 説明      |
|:----------------|:------------------|
| メソッド       | &lt;ul&gt;&lt;li&gt;(必須) リクエストメソッドを選択します。&lt;/li&gt;&lt;li&gt;**GET** が選択された場合、イベントデータは `data` キーを持つ JSON URLエンコードされたクエリ文字列パラメータとして配信されます。&lt;/li&gt;&lt;/ul&gt;     |
| URL       | &lt;ul&gt;&lt;li&gt;(必須) リクエストを送信するURLを提供します。&lt;/li&gt;&lt;li&gt;テンプレートサポート: テンプレート名を参照してURLを生成します。&lt;/li&gt;&lt;/ul&gt;    |
| URL パラメータ     | &lt;ul&gt;&lt;li&gt;(オプション) URLに追加するパラメータを提供します。&lt;/li&gt;&lt;li&gt;テンプレートサポート: テンプレート名を参照してパラメータ値を生成します。&lt;/li&gt;&lt;/ul&gt;  |
| ヘッダー      | &lt;ul&gt;&lt;li&gt;(オプション) HTTPヘッダー値をヘッダー名にマッピングします。&lt;/li&gt;&lt;li&gt;テンプレートサポート: テンプレート名を参照してヘッダー値を生成します。&lt;/li&gt;&lt;/ul&gt;     |
| クッキー     | &lt;ul&gt;&lt;li&gt;(オプション) クッキー値をクッキー名にマッピングします。&lt;/li&gt;&lt;li&gt;クッキーは単一のHTTPヘッダー値として追加されます。例: `Cookie: name1=value1; name2=value2`&lt;/li&gt;&lt;li&gt;テンプレートサポート: テンプレート名を参照してクッキー値を生成します。&lt;/li&gt;&lt;/ul&gt;     |
| ボディコンテンツタイプ     | &lt;ul&gt;&lt;li&gt;(オプション) 利用可能なタイプを選択するか、カスタム値を提供します。&lt;/li&gt;&lt;li&gt;すべてのタイプはUTF-8エンコードされ、ヘッダーとして追加されます。例: `Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;ボディデータが提供される場合、コンテンツタイプが必要です。&lt;/li&gt;&lt;/ul&gt;      |
| テンプレート変数    | &lt;ul&gt;&lt;li&gt;(オプション) テンプレートのデータ入力としてテンプレート変数を提供します。詳細は  を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を名前付けします。例: `items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt;   |
| テンプレート             | &lt;ul&gt;&lt;li&gt;(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。詳細は  を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例: `{{SomeTemplateName}}`&lt;/li&gt;&lt;li&gt;OAuthを使用する場合、テンプレート変数 `{{webhook_access_token}}` は認証リクエストによって返されるトークンを指します。&lt;/li&gt;&lt;/ul&gt; |
| 現在の訪問データを訪問データに含める | &lt;ul&gt;&lt;li&gt;ペイロードに現在の訪問データを追加します。&lt;/li&gt;&lt;li&gt;これには、現在の訪問イベントデータが除外されていない場合のイベント訪問データが含まれます。&lt;/li&gt;&lt;/ul&gt; |
| 現在の訪問イベントデータを除外 | &lt;ul&gt;&lt;li&gt;現在の訪問データからイベントデータを除外します。&lt;/li&gt;&lt;/ul&gt; |
| 属性名の印刷      | &lt;ul&gt;&lt;li&gt;属性名が更新された場合、ペイロードに名前が反映されます。&lt;/li&gt;&lt;/ul&gt;     |
| リダイレクション    | &lt;ul&gt;&lt;li&gt;メソッドがGETの場合のみリダイレクションを許可します。&lt;/li&gt;&lt;/ul&gt;    |

### HTTPリクエストを介してカスタマイズされたデータを送信 (高度)

#### パラメータ

| パラメータ     | 説明    |
|:-------------------|:---------------------|
| メソッド    | &lt;ul&gt;&lt;li&gt;(必須) 詳細は [Webhook Send Custom Request Guide]() を参照してください。&lt;/li&gt;&lt;li&gt;リクエストメソッドを選択します。&lt;/li&gt;&lt;/ul&gt;    |
| URL     | &lt;ul&gt;&lt;li&gt;(必須) リクエストを送信するURLを提供します。&lt;/li&gt;&lt;li&gt;テンプレートサポート: テンプレート名を参照してURLを生成します。&lt;/li&gt;&lt;/ul&gt;     |
| URL パラメータ     | &lt;ul&gt;&lt;li&gt;(オプション) URLに追加するパラメータを提供します。&lt;/li&gt;&lt;li&gt;テンプレートサポート: テンプレート名を参照してパラメータ値を生成します。&lt;/li&gt;&lt;/ul&gt;|
| ヘッダー    | &lt;ul&gt;&lt;li&gt;(オプション) HTTPヘッダー値をヘッダー名にマッピングします。&lt;/li&gt;&lt;li&gt;テンプレートサポート: テンプレート名を参照してヘッダー値を生成します。&lt;/li&gt;&lt;/ul&gt;   |
| クッキー  | &lt;ul&gt;&lt;li&gt;(オプション) クッキー値をクッキー名にマッピングします。&lt;/li&gt;&lt;li&gt;クッキーは単一のHTTPヘッダー値として追加されます。例: `Cookie: name1=value1; name2=value2`&lt;/li&gt;&lt;li&gt;テンプレートサポート: テンプレート名を参照してクッキー値を生成します。&lt;/li&gt;&lt;/ul&gt;    |
| ボディコンテンツタイプ  | &lt;ul&gt;&lt;li&gt;(オプション) 利用可能なタイプを選択するか、カスタム値を提供します。&lt;/li&gt;&lt;li&gt;すべてのタイプはUTF-8エンコードされ、ヘッダーとして追加されます。例: `Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;ボディデータが提供される場合、コンテンツタイプが必要です。&lt;/li&gt;&lt;/ul&gt;     |
| ボディデータ   | &lt;ul&gt;&lt;li&gt;(オプション) メッセージボディを構築するためのデータを提供します。&lt;/li&gt;&lt;li&gt;テンプレートサポート: テンプレート名を参照してボディデータを生成します。&lt;/li&gt;&lt;li&gt;ボディコンテンツタイプが `multipart/form-data` または `application/x-www-form-urlencoded` の場合、値を名前にマッピングします。それ以外の場合はテンプレート名を参照し、**Body** オプションのみを選択します。&lt;/li&gt;&lt;/ul&gt;   |
| テンプレート変数 | &lt;ul&gt;&lt;li&gt;(オプション) テンプレートのデータ入力としてテンプレート変数を提供します。詳細は  を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を名前付けします。例: `items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt;  |
| テンプレート     | &lt;ul&gt;&lt;li&gt;(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。詳細は  を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例: `{{SomeTemplateName}}`&lt;/li&gt;&lt;li&gt;OAuthを使用する場合、テンプレート変数 `{{webhook_access_token}}` は認証リクエストによって返されるトークンを指します。&lt;/li&gt;&lt;/ul&gt; |
| リダイレクション    | &lt;ul&gt;&lt;li&gt;メソッドがGETの場合のみリダイレクションを許可します。&lt;/li&gt;&lt;/ul&gt;    |

### HTTPリクエストを介してバッチデータを送信
#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション]()を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：100
* 最古のリクエストからの最大時間：60分
* リクエストの最大サイズ：16 MB

#### パラメータ

| パラメータ      | 説明      |
|:------------|:------------------|
| メソッド       | &lt;ul&gt;&lt;li&gt;(必須) 詳細については、[Webhook送信カスタムリクエストガイド]()を参照してください。&lt;/li&gt;&lt;li&gt;リクエストメソッドを選択します。&lt;/li&gt;&lt;/ul&gt;     |
| URL     | &lt;ul&gt;&lt;li&gt;(必須) リクエストを送信するURLを提供してください。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してURLを生成します。&lt;/li&gt;&lt;/ul&gt;     |
| URLパラメータ   | &lt;ul&gt;&lt;li&gt;(オプション) URLに追加するパラメータを提供してください。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してパラメータ値を生成します。&lt;/li&gt;&lt;/ul&gt; |
| ヘッダー   | &lt;ul&gt;&lt;li&gt;(オプション) HTTPヘッダー名にヘッダー値をマッピングします。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。&lt;/li&gt;&lt;/ul&gt;    |
| クッキー    | &lt;ul&gt;&lt;li&gt;(オプション) クッキー名にクッキー値をマッピングします。&lt;/li&gt;&lt;li&gt;クッキーは単一のHTTPヘッダー値として追加されます。例：`Cookie: name1=value1; name2=value2`&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してクッキー値を生成します。&lt;/li&gt;&lt;/ul&gt;  |
| ボディコンテンツタイプ     | &lt;ul&gt;&lt;li&gt;(オプション) 利用可能なタイプを選択するか、カスタム値を提供してください。&lt;/li&gt;&lt;li&gt;すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;ボディデータが提供されている場合、コンテンツタイプが必要です。&lt;/li&gt;&lt;/ul&gt;     |
| テンプレート変数    | &lt;ul&gt;&lt;li&gt;(オプション) テンプレートのデータ入力としてテンプレート変数を提供してください。詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を名前付けします。例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt;   |
| テンプレート   | &lt;ul&gt;&lt;li&gt;(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供してください。詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例：`{{SomeTemplateName}}`&lt;/li&gt;&lt;li&gt;OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されたトークンを参照します。&lt;/li&gt;&lt;/ul&gt; |
| 現在の訪問データを含む | &lt;ul&gt;&lt;li&gt;現在の訪問データを含める場合は、このチェックボックスを選択します。&lt;/li&gt;&lt;/ul&gt;   |
| 現在の訪問イベントデータを除外 | &lt;ul&gt;&lt;li&gt;現在の訪問データからイベントデータを除外します。&lt;/li&gt;&lt;/ul&gt; |
| 属性名を印刷      | &lt;ul&gt;&lt;li&gt;属性名が更新された場合、ペイロードに名前が反映されます。&lt;/li&gt;&lt;/ul&gt;     |
| リダイレクション    | &lt;ul&gt;&lt;li&gt;メソッドがGETの場合のみリダイレクションを許可します。&lt;/li&gt;&lt;/ul&gt;    |
| タイムアウト | `HTTP`リクエストを通じてデータを送信する際、システムがバッチアクションを完了するのを待つ最大時間（秒）を構成します。最小値は`1`、最大値は`10`です。 |

### HTTPリクエストを介してバッチカスタマイズデータを送信する（高度）

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション]()を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：100
* 最古のリクエストからの最大時間：60分
* リクエストの最大サイズ：16 MB

#### パラメータ

| パラメータ      | 説明      |
|:------------|:------------------|
| メソッド       | &lt;ul&gt;&lt;li&gt;(必須) 詳細については、[Webhook送信カスタムリクエストガイド]()を参照してください。&lt;/li&gt;&lt;li&gt;リクエストメソッドを選択します。&lt;/li&gt;&lt;/ul&gt;     |
| URL     | &lt;ul&gt;&lt;li&gt;(必須) リクエストを送信するURLを提供してください。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してURLを生成します。&lt;/li&gt;&lt;/ul&gt;     |
| ボディコンテンツタイプ     | &lt;ul&gt;&lt;li&gt;(オプション) 利用可能なタイプを選択するか、カスタム値を提供してください。&lt;/li&gt;&lt;li&gt;すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;ボディデータが提供されている場合、コンテンツタイプが必要です。&lt;/li&gt;&lt;/ul&gt;     |
| ボディデータ    | &lt;ul&gt;&lt;li&gt;(オプション) メッセージボディを構築するためのデータを提供してください。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してボディデータを生成します。&lt;/li&gt;&lt;li&gt;ボディコンテンツタイプが`multipart/form-data`または`application/x-www-form-urlencoded`の場合は、値を名前にマッピングします。それ以外の場合は、テンプレート名を参照し、`Body`オプションのみを選択します。&lt;/li&gt;&lt;/ul&gt;     |
| プレフィックス | リクエストのボディデータの前に繰り返されない部分です。JSON配列のプレフィックスは開き括弧(`[`)です。`Custom [`を**プレフィックス**にマッピングします。例：&lt;br/&gt; `[   {     &#34;editable_in_signup&#34;: false,     &#34;displayed_for_customers&#34;: true    },   {     &#34;editable_in_signup&#34;: true,     &#34;displayed_for_customers&#34;: true   } ] ` |
| ジョイナー | ボディデータ内の個々のデータ項目を区切る文字または文字列です。JSONオブジェクトのジョイナーはカンマ(`,`)です。`Custom ,`を**ジョイナー**にマッピングします。例：&lt;br/&gt; `[   {     &#34;editable_in_signup&#34;: false,     &#34;displayed_for_customers&#34;: true    },  {     &#34;editable_in_signup&#34;: true,     &#34;displayed_for_customers&#34;: true   } ]`  |
| サフィックス | リクエストのボディデータの後に繰り返されない部分です。JSON配列のプレフィックスは閉じ括弧(`]`)です。`Custom ]`を**サフィックス**にマッピングします。例：&lt;br/&gt; `[   {     &#34;editable_in_signup&#34;: false,     &#34;displayed_for_customers&#34;: true    },   {     &#34;editable_in_signup&#34;: true,     &#34;displayed_for_customers&#34;: true   } ] ` |
| レコード数の最大値   | &lt;ul&gt;&lt;li&gt;最大レコード数。&lt;/li&gt;&lt;/ul&gt;     |
| 生存時間 (分) | &lt;ul&gt;&lt;li&gt;分単位の生存時間。&lt;/li&gt;&lt;/ul&gt;       |
| URLパラメータ   | &lt;ul&gt;&lt;li&gt;(オプション) URLに追加するパラメータを提供してください。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してパラメータ値を生成します。&lt;/li&gt;&lt;/ul&gt; |
| ヘッダー   | &lt;ul&gt;&lt;li&gt;(オプション) HTTPヘッダー名にヘッダー値をマッピングします。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。&lt;/li&gt;&lt;/ul&gt;    |
| ヘッダー   | &lt;ul&gt;&lt;li&gt;(オプション) HTTPヘッダー名にヘッダー値をマッピングします。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。&lt;/li&gt;&lt;/ul&gt;    |
| テンプレート変数    | &lt;ul&gt;&lt;li&gt;(オプション) テンプレートのデータ入力としてテンプレート変数を提供してください。詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を名前付けします。例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt;   |
| テンプレート   | &lt;ul&gt;&lt;li&gt;(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供してください。詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例：`{{SomeTemplateName}}`&lt;/li&gt;&lt;li&gt;OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されたトークンを参照します。&lt;/li&gt;&lt;/ul&gt; |
| タイムアウト | `HTTP`リクエストを通じてデータを送信する際、システムがバッチアクションを完了するのを待つ最大時間（秒）を構成します。最小値は`1`、最大値は`10`です。 |
## イベントデータJSON

イベントに含まれる予想されるJSONペイロードには、イベントの標準属性すべてと、イベントを送信したプラットフォーム固有の追加属性が含まれます。例えば、ウェブサイトから受け取ったイベントにはDOMやクッキーの属性が含まれ、モバイルデバイスから受け取ったイベントにはデバイスやキャリアの属性が含まれます。

イベントデータJSONオブジェクトの形式例：

```json
{
    &#34;account&#34;: &#34;tealium&#34;,
    &#34;profile&#34;: &#34;main&#34;,
    &#34;env&#34;: &#34;prod&#34;,
    &#34;data&#34;: {
        &#34;dom&#34;: {
            &#34;referrer&#34;: &#34;&#34;,
            &#34;domain&#34;: &#34;tealium.com&#34;,
            &#34;title&#34;: &#34;Tealium | Customer Data Hub and Enterprise Tag Management&#34;,
            &#34;query_string&#34;: &#34;&#34;,
            &#34;url&#34;: &#34;http://tealium.com/&#34;,
            &#34;pathname&#34;: &#34;/&#34;
        },
        &#34;udo&#34;: {
            &#34;tealium_event&#34;: &#34;page_view&#34;,
            &#34;page_name&#34;: &#34;Tealium | Customer Data Hub and Enterprise Tag Management&#34;,
            &#34;page_type&#34;: &#34;home&#34;,
            &#34;device_type&#34;: &#34;desktop&#34;
        },
        &#34;firstparty_tealium_cookies&#34;: {
            &#34;trace_id&#34;: &#34;&#34;,
            &#34;s_fid&#34;: &#34;3EF757DF6253B144-0D0194366CD4479B&#34;,
            &#34;utag_main_ses_id&#34;: 1383677957942,
            &#34;s_cc&#34;: &#34;true&#34;,
            &#34;utag_mainst&#34;: 1383678970903,
            &#34;TID&#34;: &#34;2cff51e585ed4a5a9330324d5dbc6bb7&#34;,
            &#34;s_sq&#34;: &#34;[[B]]&#34;
        }
    },
    &#34;post_time&#34;: 1500999541000,
    &#34;useragent&#34;: &#34;PostmanRuntime/6.1.6&#34;,
    &#34;event_id&#34;: &#34;1a1ee055-1456-46f8-ab4d-779628c05dd4&#34;,
    &#34;visitor_id&#34;: &#34;1a1ee055145646f8ab4d779628c05dd4&#34;
}

```

## 訪問データJSON

訪問に関する予想されるJSONペイロードには、その訪問に適用可能なすべての訪問属性が含まれます。データオブジェクトは属性タイプごとに整理されています。属性が割り当てられていない場合、訪問オブジェクトには表示されません。現在の訪問のデータも `current_visit` キーの下に含まれます。

訪問データJSONオブジェクトの形式例：

```json
{
    &#34;metrics&#34;: {
        &#34;Weeks since first visit&#34;: 0.0,
        &#34;Lifetime visit count&#34;: 1.0,
        &#34;Lifetime event count&#34;: 1.0,
        &#34;Total direct visits&#34;: 1.0
    },
    &#34;dates&#34;: {
        &#34;Last visit&#34;: 1500999541000,
        &#34;last_visit_start_ts&#34;: 1500999541000,
        &#34;First visit&#34;: 1500999541000
    },
    &#34;properties&#34;: {
        &#34;profile&#34;: &#34;main&#34;,
        &#34;visitor_id&#34;: &#34;1a1ee055145646f8ab4d779628c05dd4&#34;,
        &#34;account&#34;: &#34;tealium&#34;
    },
    &#34;flags&#34;: {
        &#34;Is Registered&#34;: false
    },
    &#34;audiences&#34;: [
        &#34;New Users&#34;
    ],
    &#34;badges&#34;: [
        &#34;Product Browser&#34;
    ],
    &#34;preloaded&#34;: false,
    &#34;creation_ts&#34;: 1500999541000,
    &#34;_id&#34;: &#34;1a1ee055145646f8ab4d779628c05dd4&#34;,
    &#34;_partition&#34;: 0,
    &#34;shard_token&#34;: 0,
    &#34;current_visit&#34;: {
        &#34;metrics&#34;: {
            &#34;Event count&#34;: 1.0
        },
        &#34;dates&#34;: {
            &#34;Visit start&#34;: 1500999541000,
            &#34;last_event_ts&#34;: 1500999541000
        },
        &#34;properties&#34;: {
            &#34;Active browser type&#34;: &#34;Chrome&#34;,
            &#34;Active operating system&#34;: &#34;MacOS&#34;,
            &#34;Active browser version&#34;: &#34;53&#34;,
            &#34;Active platform&#34;: &#34;browser&#34;,
            &#34;Active device&#34;: &#34;other&#34;
        },
        &#34;flags&#34;: {
            &#34;Direct visit&#34;: true
        },
        &#34;property_sets&#34;: {
            &#34;Active devices&#34;: [
                &#34;other&#34;
            ],
            &#34;Active browser versions&#34;: [
                &#34;53&#34;
            ],
            &#34;Active operating systems&#34;: [
                &#34;MacOS&#34;
            ],
            &#34;Active platforms&#34;: [
                &#34;browser&#34;
            ],
            &#34;Active browser types&#34;: [
                &#34;Chrome&#34;
            ]
        },
        &#34;creation_ts&#34;: 1500999541000,
        &#34;_id&#34;: &#34;9a20caf81d4adc55cfb958da81a513feff62e3324e9f840ed8bf28ca8a39a37d&#34;,
        &#34;shard_token&#34;: 0,
        &#34;_dc_ttl_&#34;: 60000,
        &#34;total_event_count&#34;: 1,
        &#34;events_compressed&#34;: false
    },
    &#34;_dctrace&#34;: [
        &#34;local_visitor_processor_visitor_processor&#34;
    ],
    &#34;new_visitor&#34;: true,
    &#34;audiences_joined_at&#34;: {
        &#34;tealium_main_101&#34;: 1500999542434
    }
}

```

## 使用例

このセクションでは、HTTPリクエストの例を提供します。これらの例では明確さのために単純なJSONオブジェクトが使用されています。実際に送信されるデータは完全なイベントまたは訪問オブジェクトです。また、追加のパラメータがどのように送信されるかを示すために、`param1` が `value1` の値を受け取る単一のURLパラメータも含まれています。

### イベント/訪問の送信 - GETメソッド

Send Event DataまたはSend Visitor Dataアクションを使用する場合、GETメソッドではデータが `data` という名前の単一のクエリ文字列パラメータとして送信されます。値はイベント/訪問データオブジェクトのURLエンコードされたJSON文字列です。構成されたURLパラメータは追加のクエリ文字列パラメータとして追加されます。

この例では、データは次のとおりです：

```json
{
    &#34;foo&#34; : &#34;bar&#34;
}
```

結果のURLエンコードされたJSON文字列は次のとおりです：

`%7B%22foo%22%3A%22bar%22%7D`

これは最終的なGETリクエストで次のクエリ文字列パラメータとして表示されます：

`data=%7B%22foo%22%3A%22bar%22%7D`

```
**GET** /webhook-service?data=%7B%22foo%22%3A%22bar%22%7D&amp;param1=value1

VERSION: HTTP/1.1
CONNECTION: close
ACCEPT-ENCODING: gzip
X-HEADER-KEY: header_value
COOKIE: cookie_key=cookie_valie,cfduid=d63c6b0e0a23195e9a7142f314360b4e11502122913
USER-AGENT: Apache-HttpClient/4.5.1 (Java/1.8.0_111)
```

### イベント/訪問の送信 - POSTメソッド

次に、**`application/json`** および `application/x-www-form-urlencoded` コンテンツタイプのPOSTリクエストのサンプルを示します。

#### Content-Type: application/json

本文データはJSONペイロードとして送信されます。

```
POST /webhook-service?param1=value1

VERSION: HTTP/1.1
CONNECTION: close
ACCEPT-ENCODING: gzip
X-HEADER-KEY: header_value
COOKIE: cookie_key=cookie_valie
CONTENT-TYPE: application/json; charset=UTF-8
USER-AGENT: Apache-HttpClient/4.5.1 (Java/1.8.0_111)
CONTENT-LENGTH: 13

{
    &#34;foo&#34;: &#34;bar&#34;
}

```

#### Content-Type: application/x-form-urlencoded

本文データは `data` という名前のフォームデータフィールドを使用してURLエンコードされたJSON文字列として送信されます。

```
POST /webhook-service?param1=value1

VERSION: HTTP/1.1
CONNECTION: close
ACCEPT-ENCODING: gzip
X-HEADER-KEY: header_value
COOKIE: cookie_key=cookie_valie,cfduid=d63c6b0e0a23195e9a7142f314360b4e11502122913
CONTENT-TYPE: application/x-www-form-urlencoded; charset=UTF-8
USER-AGENT: Apache-HttpClient/4.5.1 (Java/1.8.0_111)
CONTENT-LENGTH: 32

data=%7B%22foo%22%3A%22bar%22%7D
```

## ベンダーの使用例

次のリソースは、高度なWebhook構成の例を提供し、カスタムリクエストで可能なことの良い基盤と概要を提供します。

* [Kony API]()
* [Keen.io API]()
* [Salesforce Predictive Intelligence (formerly iGoDigital) API]()
* [Facebook App Events API]()

## FAQ

### HTTPレスポンスクッキーはどのように扱われますか？

クッキーベースのセッション管理はウェブブラウザでは一般的ですが、ステートレスAPIと通信するサーバー間環境では一般的に推奨されません。そのため、Webhookコネクタはクッキーベースのセッションを追跡せず、HTTPレスポンスの `Set-Cookie` ヘッダー値を効果的に無視します。

## 変更ログ

#### 2024年7月10日

* すべてのEventStream WebhookにHTTPリクエストを介してイベントデータを送信するアクションを追加しました。
* すべてのAudienceStream WebhookにHTTPリクエストを介して訪問データを送信するアクションとバッチ訪問データを送信するアクションを追加しました。

#### 2021年11月30日

* Webhookコネクタが302レスポンスをサポートするための構成オプションを追加しました。

#### 2021年7月20日

* コネクタアクションテーブルに各アクションへのリンクを追加しました。

#### 2021年6月7日

* HTTPリクエストを介してバッチカスタマイズデータを送信するアクション（Advanced）とバッチ制限セクションを追加しました。

#### 2020年11月5日

* Webhook 2-Legged OAuth2および3-Legged OAuth2コネクタのバッチサポートを追加しました。

#### 2018年12月18日

* WebhookコネクタのApacheクッキー管理を無効にし、ドメインレベルのクッキーが共有されるのを防ぎました。
#### 2017年08月24日

* 新たに2つのアクションを追加：HTTPリクエストを通じてイベントデータを送信、HTTPリクエストを通じて訪問データを送信。

#### 2017年03月02日

* OAuthサービスをサポートするための新しいWebhook OAuth2コネクタを追加。このサービスはWebhook（BasicAuth）コネクタとは別です。

#### 2016年11月13日

* 複雑なJSONおよびXMLペイロードをサポートする新しいカスタムリクエスト送信アクションを追加。ネストされたJSONを翻訳するための組み込みテンプレートユーティリティをサポート。
* GET、POST、およびPUTメソッドを新しいアクションの下に移動。これらはもはや別のアクションとして扱われません。

#### 2016年06月14日

* AudienceDirectコネクタはWebhookに置き換えられて廃止されました。
* POST-visitorおよびPUT-Visitorアクションは新しいWebhook（BasicAuth）コネクタに統合されました。
* プロファイルに廃止された/機能しないAudienceDirectアクションが含まれている場合、新しいWebhookインスタンスで再構成する必要があります。