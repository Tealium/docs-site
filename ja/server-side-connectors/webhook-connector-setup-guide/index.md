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

始めるには、コネクタマーケットプレイスにアクセスし、使用したいWebhookインスタンスを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](https://docs.tealium.com/about-connectors/)を参照してください。

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


<blockquote>
OAuth 2.0サービスにWebアプリケーションを登録することを忘れないでください。アプリケーションはリダイレクトURLを許可するように構成する必要があります：`https://my.tealiumiq.com/oauth/webhook/callback.html`
</blockquote>


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
  * 複数のペアをアンパサンド(`&`)を使用して区切ります。
  * 先頭にアンパサンド(`&`)を使用しないでください。
    * 正しい: `access_type=offline&prompt=consent`
    * 誤り: `&access_type=offline&prompt=consent`
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
  * 複数のパラメータを`&`で区切ります。
* **認証URL**
  * (必須) 認証コードを要求するAPIエンドポイントURLを入力します。
* **認証トークンの位置**
  * 認証トークンを配置する場所を指定します。
* **認証ヘッダープレフィックス**
  * デフォルト値は`Bearer`です。
  * 新しい値を指定して上書きします（一部のOAuth2サービスで必要です）。
* **カスタムヘッダー**
  * 認証コールに追加したいカスタムヘッダーのキーと値のペアをコンマ区切りで指定します。たとえば、`'var1:value1','var2:value2','var3:value3,value4','var4:{"field": {"name": "TEST", "version": "1.0.0"}}'`は次のようになります：
  ```
  VERSION: HTTP/1.1
  CONNECTION: close
  ACCEPT-ENCODING: gzip
  X-HEADER-KEY: header_value
  VAR1: value1
  VAR2: value2
  VAR3: value3, value4
  VAR4: {"field": {"name": "TEST", "version": "1.0.0"}}
  COOKIE: cookie_key=cookie_value
  CONTENT-TYPE: application/json; charset=UTF-8
  USER-AGENT: Apache-HttpClient/4.5.1 (Java/1.8.0_111)
  CONTENT-LENGTH: 13
  ```
* **カスタムボディ値**
  * キーと値のペアをコンマ区切りで定義します。たとえば、`'var1:value1','var2:value2','var3:varx,vary'`。これらは**ボディコンテンツタイプ**フィールドで構成された形式に従ってボディに使用されます。
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
| メソッド             | 必須     | 次のメソッドをサポート: <ul><li>GET</li><li>POST</li><li>PUT</li><li>DELETE</li><li>PATCH</li></ul>                                                                                                                                                                                                                                                                                                                       |
| URL                | 必須                                                                                                                                                                     | ✔                | <ul><li>リクエストを送信するURLを提供する</li></ul>                                                                                                                                                                                                                                                                                                                                                                            |
| URLパラメータ     | 任意                                                                                                                                                                     | ✔                | <ul><li>**Map** ドロップダウンリストから、送信したい属性の値を選択します。</li><li>**To** フィールドに、構成するURLパラメータの名前を入力します。</li></ul>                                                                                                                                                                                                                                                    |
| ヘッダー            | Webhook（BasicAuth）では任意、[Webhook OAuth2](https://docs.tealium.com/validate-webhook-action/)では必須 | ✔                | <ul><li>**Map** ドロップダウンリストから、送信したい属性の値を選択します。</li><li>**To** フィールドに、ヘッダー名を入力します。</li></ul>                                                                                                                                                                                                                                     |
| クッキー            | 任意                                                                                                                                                                     | ✔                | <ul><li>**Map** ドロップダウンリストから、送信したい属性の値を選択します。</li><li>**To** フィールドに、クッキー名を入力します。</li></ul>                                                                                                                                                                                                                                     |
| ボディコンテンツタイプ  | 任意                                                                                                                                                                     |                  | <ul><li>`Content-Type` ヘッダーを指定します。</li><li>すべてのタイプはUTF-8文字セットを使用します。</li><li>GETメソッドの場合はこの構成を無視します。</li></ul>                                                                                                                                                                                                                                                                             |
| ボディデータ          | 任意                                                                                                                                                                     | ✔                | <ul><li>**HTTPリクエストを介してカスタマイズされたデータを送信** アクションのみサポートされます</li><li>GETメソッドの場合はこの構成を無視します。</li><li>ボディコンテンツタイプが `application/x-www-form-urlencoded` の場合は、名前/値のペアを提供します</li><li>より複雑なペイロードの場合は、テンプレート名を提供します。</li></ul>                                                                                                                                 |
| バッチングオプション   | 任意                                                                                                                                                                     | ✔                | <ul><li>レコード数の最大値は10から10,000まで。</li><li>有効期限は、5分から60分まで。</li></ul>                                                                                                                                                                                                                                                                                                        |
| テンプレート変数 | 任意                                                                                                                                                                     |                  | <ul><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li></ul>                                                                                                                                                                                                                                                             |
| テンプレート          | 任意                                                                                                                                                                     |                  | <ul><li>詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>各テンプレートには一意の名前が必要です</li><li>サポートされているフィールドにテンプレートを注入するには、その名前を二重中括弧で囲んで参照します</li><li>URL、URLパラメータ、ヘッダー、クッキー、またはボディデータフィールドにテンプレートを注入できます</li></ul> |

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
| メソッド       | <ul><li>(必須) リクエストメソッドを選択します。</li><li>**GET** が選択された場合、イベントデータは `data` キーを持つ JSON URLエンコードされたクエリ文字列パラメータとして配信されます。</li></ul>     |
| URL       | <ul><li>(必須) リクエストを送信するURLを提供します。</li><li>テンプレートサポート: テンプレート名を参照してURLを生成します。</li></ul>    |
| URL パラメータ     | <ul><li>(オプション) URLに追加するパラメータを提供します。</li><li>テンプレートサポート: テンプレート名を参照してパラメータ値を生成します。</li></ul>  |
| ヘッダー      | <ul><li>(オプション) HTTPヘッダー値をヘッダー名にマッピングします。</li><li>テンプレートサポート: テンプレート名を参照してヘッダー値を生成します。</li></ul>     |
| クッキー     | <ul><li>(オプション) クッキー値をクッキー名にマッピングします。</li><li>クッキーは単一のHTTPヘッダー値として追加されます。例: `Cookie: name1=value1; name2=value2`</li><li>テンプレートサポート: テンプレート名を参照してクッキー値を生成します。</li></ul>     |
| ボディコンテンツタイプ     | <ul><li>(オプション) 利用可能なタイプを選択するか、カスタム値を提供します。</li><li>すべてのタイプはUTF-8エンコードされ、ヘッダーとして追加されます。例: `Content-Type: text/plain; charset=UTF-8`</li><li>ボディデータが提供される場合、コンテンツタイプが必要です。</li></ul>      |
| テンプレート変数    | <ul><li>(オプション) テンプレートのデータ入力としてテンプレート変数を提供します。詳細は [connector-template-variables](https://docs.tealium.com/connector-template-variables/) を参照してください。</li><li>ドット表記でネストされたテンプレート変数を名前付けします。例: `items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul>   |
| テンプレート             | <ul><li>(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。詳細は [about-connector-templates](https://docs.tealium.com/about-connector-templates/) を参照してください。</li><li>テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例: `{{SomeTemplateName}}`</li><li>OAuthを使用する場合、テンプレート変数 `{{webhook_access_token}}` は認証リクエストによって返されるトークンを指します。</li></ul> |
| 属性名の印刷 | <ul><li>属性名が更新された場合、ペイロードに名前が反映されます。</li></ul>   |
| リダイレクション           | <ul><li>メソッドがGETの場合のみリダイレクションを許可します。</li></ul>  |

### HTTPリクエストを介して訪問データを送信

#### パラメータ

| パラメータ   | 説明      |
|:----------------|:------------------|
| メソッド       | <ul><li>(必須) リクエストメソッドを選択します。</li><li>**GET** が選択された場合、イベントデータは `data` キーを持つ JSON URLエンコードされたクエリ文字列パラメータとして配信されます。</li></ul>     |
| URL       | <ul><li>(必須) リクエストを送信するURLを提供します。</li><li>テンプレートサポート: テンプレート名を参照してURLを生成します。</li></ul>    |
| URL パラメータ     | <ul><li>(オプション) URLに追加するパラメータを提供します。</li><li>テンプレートサポート: テンプレート名を参照してパラメータ値を生成します。</li></ul>  |
| ヘッダー      | <ul><li>(オプション) HTTPヘッダー値をヘッダー名にマッピングします。</li><li>テンプレートサポート: テンプレート名を参照してヘッダー値を生成します。</li></ul>     |
| クッキー     | <ul><li>(オプション) クッキー値をクッキー名にマッピングします。</li><li>クッキーは単一のHTTPヘッダー値として追加されます。例: `Cookie: name1=value1; name2=value2`</li><li>テンプレートサポート: テンプレート名を参照してクッキー値を生成します。</li></ul>     |
| ボディコンテンツタイプ     | <ul><li>(オプション) 利用可能なタイプを選択するか、カスタム値を提供します。</li><li>すべてのタイプはUTF-8エンコードされ、ヘッダーとして追加されます。例: `Content-Type: text/plain; charset=UTF-8`</li><li>ボディデータが提供される場合、コンテンツタイプが必要です。</li></ul>      |
| テンプレート変数    | <ul><li>(オプション) テンプレートのデータ入力としてテンプレート変数を提供します。詳細は [connector-template-variables](https://docs.tealium.com/connector-template-variables/) を参照してください。</li><li>ドット表記でネストされたテンプレート変数を名前付けします。例: `items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul>   |
| テンプレート             | <ul><li>(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。詳細は [about-connector-templates](https://docs.tealium.com/about-connector-templates/) を参照してください。</li><li>テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例: `{{SomeTemplateName}}`</li><li>OAuthを使用する場合、テンプレート変数 `{{webhook_access_token}}` は認証リクエストによって返されるトークンを指します。</li></ul> |
| 現在の訪問データを訪問データに含める | <ul><li>ペイロードに現在の訪問データを追加します。</li><li>これには、現在の訪問イベントデータが除外されていない場合のイベント訪問データが含まれます。</li></ul> |
| 現在の訪問イベントデータを除外 | <ul><li>現在の訪問データからイベントデータを除外します。</li></ul> |
| 属性名の印刷      | <ul><li>属性名が更新された場合、ペイロードに名前が反映されます。</li></ul>     |
| リダイレクション    | <ul><li>メソッドがGETの場合のみリダイレクションを許可します。</li></ul>    |

### HTTPリクエストを介してカスタマイズされたデータを送信 (高度)

#### パラメータ

| パラメータ     | 説明    |
|:-------------------|:---------------------|
| メソッド    | <ul><li>(必須) 詳細は [Webhook Send Custom Request Guide](https://docs.tealium.com/webhook-connector-setup-guide/) を参照してください。</li><li>リクエストメソッドを選択します。</li></ul>    |
| URL     | <ul><li>(必須) リクエストを送信するURLを提供します。</li><li>テンプレートサポート: テンプレート名を参照してURLを生成します。</li></ul>     |
| URL パラメータ     | <ul><li>(オプション) URLに追加するパラメータを提供します。</li><li>テンプレートサポート: テンプレート名を参照してパラメータ値を生成します。</li></ul>|
| ヘッダー    | <ul><li>(オプション) HTTPヘッダー値をヘッダー名にマッピングします。</li><li>テンプレートサポート: テンプレート名を参照してヘッダー値を生成します。</li></ul>   |
| クッキー  | <ul><li>(オプション) クッキー値をクッキー名にマッピングします。</li><li>クッキーは単一のHTTPヘッダー値として追加されます。例: `Cookie: name1=value1; name2=value2`</li><li>テンプレートサポート: テンプレート名を参照してクッキー値を生成します。</li></ul>    |
| ボディコンテンツタイプ  | <ul><li>(オプション) 利用可能なタイプを選択するか、カスタム値を提供します。</li><li>すべてのタイプはUTF-8エンコードされ、ヘッダーとして追加されます。例: `Content-Type: text/plain; charset=UTF-8`</li><li>ボディデータが提供される場合、コンテンツタイプが必要です。</li></ul>     |
| ボディデータ   | <ul><li>(オプション) メッセージボディを構築するためのデータを提供します。</li><li>テンプレートサポート: テンプレート名を参照してボディデータを生成します。</li><li>ボディコンテンツタイプが `multipart/form-data` または `application/x-www-form-urlencoded` の場合、値を名前にマッピングします。それ以外の場合はテンプレート名を参照し、**Body** オプションのみを選択します。</li></ul>   |
| テンプレート変数 | <ul><li>(オプション) テンプレートのデータ入力としてテンプレート変数を提供します。詳細は [connector-template-variables](https://docs.tealium.com/connector-template-variables/) を参照してください。</li><li>ドット表記でネストされたテンプレート変数を名前付けします。例: `items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul>  |
| テンプレート     | <ul><li>(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。詳細は [about-connector-templates](https://docs.tealium.com/about-connector-templates/) を参照してください。</li><li>テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例: `{{SomeTemplateName}}`</li><li>OAuthを使用する場合、テンプレート変数 `{{webhook_access_token}}` は認証リクエストによって返されるトークンを指します。</li></ul> |
| リダイレクション    | <ul><li>メソッドがGETの場合のみリダイレクションを許可します。</li></ul>    |

### HTTPリクエストを介してバッチデータを送信
#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：100
* 最古のリクエストからの最大時間：60分
* リクエストの最大サイズ：16 MB

#### パラメータ

| パラメータ      | 説明      |
|:------------|:------------------|
| メソッド       | <ul><li>(必須) 詳細については、[Webhook送信カスタムリクエストガイド](https://docs.tealium.com/webhook-connector-setup-guide/)を参照してください。</li><li>リクエストメソッドを選択します。</li></ul>     |
| URL     | <ul><li>(必須) リクエストを送信するURLを提供してください。</li><li>テンプレートサポート：テンプレート名を参照してURLを生成します。</li></ul>     |
| URLパラメータ   | <ul><li>(オプション) URLに追加するパラメータを提供してください。</li><li>テンプレートサポート：テンプレート名を参照してパラメータ値を生成します。</li></ul> |
| ヘッダー   | <ul><li>(オプション) HTTPヘッダー名にヘッダー値をマッピングします。</li><li>テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。</li></ul>    |
| クッキー    | <ul><li>(オプション) クッキー名にクッキー値をマッピングします。</li><li>クッキーは単一のHTTPヘッダー値として追加されます。例：`Cookie: name1=value1; name2=value2`</li><li>テンプレートサポート：テンプレート名を参照してクッキー値を生成します。</li></ul>  |
| ボディコンテンツタイプ     | <ul><li>(オプション) 利用可能なタイプを選択するか、カスタム値を提供してください。</li><li>すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`</li><li>ボディデータが提供されている場合、コンテンツタイプが必要です。</li></ul>     |
| テンプレート変数    | <ul><li>(オプション) テンプレートのデータ入力としてテンプレート変数を提供してください。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記でネストされたテンプレート変数を名前付けします。例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul>   |
| テンプレート   | <ul><li>(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供してください。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例：`{{SomeTemplateName}}`</li><li>OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されたトークンを参照します。</li></ul> |
| 現在の訪問データを含む | <ul><li>現在の訪問データを含める場合は、このチェックボックスを選択します。</li></ul>   |
| 現在の訪問イベントデータを除外 | <ul><li>現在の訪問データからイベントデータを除外します。</li></ul> |
| 属性名を印刷      | <ul><li>属性名が更新された場合、ペイロードに名前が反映されます。</li></ul>     |
| リダイレクション    | <ul><li>メソッドがGETの場合のみリダイレクションを許可します。</li></ul>    |
| タイムアウト | `HTTP`リクエストを通じてデータを送信する際、システムがバッチアクションを完了するのを待つ最大時間（秒）を構成します。最小値は`1`、最大値は`10`です。 |

### HTTPリクエストを介してバッチカスタマイズデータを送信する（高度）

#### バッチ制限

このアクションは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：100
* 最古のリクエストからの最大時間：60分
* リクエストの最大サイズ：16 MB

#### パラメータ

| パラメータ      | 説明      |
|:------------|:------------------|
| メソッド       | <ul><li>(必須) 詳細については、[Webhook送信カスタムリクエストガイド](https://docs.tealium.com/webhook-connector-setup-guide/)を参照してください。</li><li>リクエストメソッドを選択します。</li></ul>     |
| URL     | <ul><li>(必須) リクエストを送信するURLを提供してください。</li><li>テンプレートサポート：テンプレート名を参照してURLを生成します。</li></ul>     |
| ボディコンテンツタイプ     | <ul><li>(オプション) 利用可能なタイプを選択するか、カスタム値を提供してください。</li><li>すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`</li><li>ボディデータが提供されている場合、コンテンツタイプが必要です。</li></ul>     |
| ボディデータ    | <ul><li>(オプション) メッセージボディを構築するためのデータを提供してください。</li><li>テンプレートサポート：テンプレート名を参照してボディデータを生成します。</li><li>ボディコンテンツタイプが`multipart/form-data`または`application/x-www-form-urlencoded`の場合は、値を名前にマッピングします。それ以外の場合は、テンプレート名を参照し、`Body`オプションのみを選択します。</li></ul>     |
| プレフィックス | リクエストのボディデータの前に繰り返されない部分です。JSON配列のプレフィックスは開き括弧(`[`)です。`Custom [`を**プレフィックス**にマッピングします。例：<br/> `[   {     "editable_in_signup": false,     "displayed_for_customers": true    },   {     "editable_in_signup": true,     "displayed_for_customers": true   } ] ` |
| ジョイナー | ボディデータ内の個々のデータ項目を区切る文字または文字列です。JSONオブジェクトのジョイナーはカンマ(`,`)です。`Custom ,`を**ジョイナー**にマッピングします。例：<br/> `[   {     "editable_in_signup": false,     "displayed_for_customers": true    },  {     "editable_in_signup": true,     "displayed_for_customers": true   } ]`  |
| サフィックス | リクエストのボディデータの後に繰り返されない部分です。JSON配列のプレフィックスは閉じ括弧(`]`)です。`Custom ]`を**サフィックス**にマッピングします。例：<br/> `[   {     "editable_in_signup": false,     "displayed_for_customers": true    },   {     "editable_in_signup": true,     "displayed_for_customers": true   } ] ` |
| レコード数の最大値   | <ul><li>最大レコード数。</li></ul>     |
| 生存時間 (分) | <ul><li>分単位の生存時間。</li></ul>       |
| URLパラメータ   | <ul><li>(オプション) URLに追加するパラメータを提供してください。</li><li>テンプレートサポート：テンプレート名を参照してパラメータ値を生成します。</li></ul> |
| ヘッダー   | <ul><li>(オプション) HTTPヘッダー名にヘッダー値をマッピングします。</li><li>テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。</li></ul>    |
| ヘッダー   | <ul><li>(オプション) HTTPヘッダー名にヘッダー値をマッピングします。</li><li>テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。</li></ul>    |
| テンプレート変数    | <ul><li>(オプション) テンプレートのデータ入力としてテンプレート変数を提供してください。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記でネストされたテンプレート変数を名前付けします。例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul>   |
| テンプレート   | <ul><li>(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供してください。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例：`{{SomeTemplateName}}`</li><li>OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されたトークンを参照します。</li></ul> |
| タイムアウト | `HTTP`リクエストを通じてデータを送信する際、システムがバッチアクションを完了するのを待つ最大時間（秒）を構成します。最小値は`1`、最大値は`10`です。 |
## イベントデータJSON

イベントに含まれる予想されるJSONペイロードには、イベントの標準属性すべてと、イベントを送信したプラットフォーム固有の追加属性が含まれます。例えば、ウェブサイトから受け取ったイベントにはDOMやクッキーの属性が含まれ、モバイルデバイスから受け取ったイベントにはデバイスやキャリアの属性が含まれます。

イベントデータJSONオブジェクトの形式例：

```json
{
    "account": "tealium",
    "profile": "main",
    "env": "prod",
    "data": {
        "dom": {
            "referrer": "",
            "domain": "tealium.com",
            "title": "Tealium | Customer Data Hub and Enterprise Tag Management",
            "query_string": "",
            "url": "http://tealium.com/",
            "pathname": "/"
        },
        "udo": {
            "tealium_event": "page_view",
            "page_name": "Tealium | Customer Data Hub and Enterprise Tag Management",
            "page_type": "home",
            "device_type": "desktop"
        },
        "firstparty_tealium_cookies": {
            "trace_id": "",
            "s_fid": "3EF757DF6253B144-0D0194366CD4479B",
            "utag_main_ses_id": 1383677957942,
            "s_cc": "true",
            "utag_mainst": 1383678970903,
            "TID": "2cff51e585ed4a5a9330324d5dbc6bb7",
            "s_sq": "[[B]]"
        }
    },
    "post_time": 1500999541000,
    "useragent": "PostmanRuntime/6.1.6",
    "event_id": "1a1ee055-1456-46f8-ab4d-779628c05dd4",
    "visitor_id": "1a1ee055145646f8ab4d779628c05dd4"
}

```

## 訪問データJSON

訪問に関する予想されるJSONペイロードには、その訪問に適用可能なすべての訪問属性が含まれます。データオブジェクトは属性タイプごとに整理されています。属性が割り当てられていない場合、訪問オブジェクトには表示されません。現在の訪問のデータも `current_visit` キーの下に含まれます。

訪問データJSONオブジェクトの形式例：

```json
{
    "metrics": {
        "Weeks since first visit": 0.0,
        "Lifetime visit count": 1.0,
        "Lifetime event count": 1.0,
        "Total direct visits": 1.0
    },
    "dates": {
        "Last visit": 1500999541000,
        "last_visit_start_ts": 1500999541000,
        "First visit": 1500999541000
    },
    "properties": {
        "profile": "main",
        "visitor_id": "1a1ee055145646f8ab4d779628c05dd4",
        "account": "tealium"
    },
    "flags": {
        "Is Registered": false
    },
    "audiences": [
        "New Users"
    ],
    "badges": [
        "Product Browser"
    ],
    "preloaded": false,
    "creation_ts": 1500999541000,
    "_id": "1a1ee055145646f8ab4d779628c05dd4",
    "_partition": 0,
    "shard_token": 0,
    "current_visit": {
        "metrics": {
            "Event count": 1.0
        },
        "dates": {
            "Visit start": 1500999541000,
            "last_event_ts": 1500999541000
        },
        "properties": {
            "Active browser type": "Chrome",
            "Active operating system": "MacOS",
            "Active browser version": "53",
            "Active platform": "browser",
            "Active device": "other"
        },
        "flags": {
            "Direct visit": true
        },
        "property_sets": {
            "Active devices": [
                "other"
            ],
            "Active browser versions": [
                "53"
            ],
            "Active operating systems": [
                "MacOS"
            ],
            "Active platforms": [
                "browser"
            ],
            "Active browser types": [
                "Chrome"
            ]
        },
        "creation_ts": 1500999541000,
        "_id": "9a20caf81d4adc55cfb958da81a513feff62e3324e9f840ed8bf28ca8a39a37d",
        "shard_token": 0,
        "_dc_ttl_": 60000,
        "total_event_count": 1,
        "events_compressed": false
    },
    "_dctrace": [
        "local_visitor_processor_visitor_processor"
    ],
    "new_visitor": true,
    "audiences_joined_at": {
        "tealium_main_101": 1500999542434
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
    "foo" : "bar"
}
```

結果のURLエンコードされたJSON文字列は次のとおりです：

`%7B%22foo%22%3A%22bar%22%7D`

これは最終的なGETリクエストで次のクエリ文字列パラメータとして表示されます：

`data=%7B%22foo%22%3A%22bar%22%7D`

```
**GET** /webhook-service?data=%7B%22foo%22%3A%22bar%22%7D&param1=value1

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
    "foo": "bar"
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

* [Kony API](https://docs.tealium.com/webhook-kony-api/)
* [Keen.io API](https://docs.tealium.com/webhook-keenio-api/)
* [Salesforce Predictive Intelligence (formerly iGoDigital) API](https://docs.tealium.com/webhook-salesforce-predictive-intelligence-api/)
* [Facebook App Events API](https://docs.tealium.com/webhook-facebook-app-events-api/)

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