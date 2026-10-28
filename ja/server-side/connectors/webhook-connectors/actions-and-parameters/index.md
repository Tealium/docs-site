---
title: Webhookのアクションとパラメータ
description: この記事では、サポートされているWebhookのアクションとパラメータについて説明します。
url: https://docs.tealium.com/ja/server-side/connectors/webhook-connectors/actions-and-parameters/
---
## アクション

認証タイプにかかわらず、HTTPベースのすべてのWebhookコネクタで次のアクションを使用できます。


<blockquote>
Webhookを使用してJDBC互換データベースにデータを送信する方法については、[Webhook JDBC](https://docs.tealium.com/webhook-jdbc/)を参照してください。
</blockquote>


### HTTPリクエストによるイベントデータの送信

| パラメータ | 説明 |
|:------------------|:-------------|
| メソッド | <ul><li>（必須）リクエストメソッドとして、`GET`、`POST`、`PUT`、`DELETE`、または`PATCH`を選択します。</li><li>**GET**を選択した場合、イベントデータは`data`キーを持つJSON形式のURLエンコードされたクエリ文字列パラメータとして配信されます。</li></ul> |
| URL | <ul><li>（必須）リクエストの送信先URLを指定します。</li><li>テンプレートのサポート：テンプレートからURLを生成するために、テンプレート名を参照します。</li></ul> |
| URLパラメータ | <ul><li>（任意）URLに追加するパラメータを指定します。</li><li>テンプレートのサポート：テンプレートからパラメータ値を生成するために、テンプレート名を参照します。</li></ul> |
| ヘッダー | <ul><li>（任意）HTTPヘッダー値をヘッダー名にマッピングします。</li><li>テンプレートのサポート：テンプレートからヘッダー値を生成するために、テンプレート名を参照します。</li></ul> |
| Cookie | <ul><li>（任意）Cookie値をCookie名にマッピングします。</li><li>Cookieは単一のHTTPヘッダー値として追加されます。例：`Cookie: name1=value1; name2=value2`</li><li>テンプレートのサポート：テンプレートからCookie値を生成するために、テンプレート名を参照します。</li></ul> |
| 本文のコンテンツタイプ | <ul><li>（任意）使用可能なタイプを選択するか、カスタム値を指定します。</li><li>すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`</li><li>本文データを指定する場合は、コンテンツタイプが必須です。</li></ul> |
| テンプレート変数 | <ul><li>（任意）テンプレートのデータ入力としてテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数にはドット表記で名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。</li></ul> |
| テンプレート | <ul><li>（任意）URL、URLパラメータ、ヘッダー、または本文データで参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、サポートされているフィールドに二重中括弧で囲んだ名前を使用して挿入されます。例：`{{SomeTemplateName}}`。</li><li>OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されたトークンを参照します。</li><li>予約変数`{{tealium_event_payload}}`と`{{tealium_visitor_payload}}`は、マッピングなしで常に使用できます。詳細については、[予約変数](https://docs.tealium.com/connector-template-variables/#reserved-variables)を参照してください。</li></ul> |
| 属性名を出力 | <ul><li>属性名が更新された場合、ペイロード内の名前にも更新が反映されます。</li></ul> |
| リダイレクト | <ul><li>メソッドがGETの場合にのみリダイレクトを許可します。</li></ul> |

### HTTPリクエストによる訪問データの送信

| パラメータ | 説明 |
|:----------------|:------------------|
| メソッド | <ul><li>（必須）リクエストメソッドとして、`GET`、`POST`、`PUT`、`DELETE`、または`PATCH`を選択します。</li><li>**GET**を選択した場合、イベントデータは`data`キーを持つJSON形式のURLエンコードされたクエリ文字列パラメータとして配信されます。</li></ul> |
| URL | <ul><li>（必須）リクエストの送信先URLを指定します。</li><li>テンプレートのサポート：テンプレートからURLを生成するために、テンプレート名を参照します。</li></ul> |
| URLパラメータ | <ul><li>（任意）URLに追加するパラメータを指定します。</li><li>テンプレートのサポート：テンプレートからパラメータ値を生成するために、テンプレート名を参照します。</li></ul> |
| ヘッダー | <ul><li>（任意）HTTPヘッダー値をヘッダー名にマッピングします。</li><li>テンプレートのサポート：テンプレートからヘッダー値を生成するために、テンプレート名を参照します。</li></ul> |
| Cookie | <ul><li>（任意）Cookie値をCookie名にマッピングします。</li><li>Cookieは単一のHTTPヘッダー値として追加されます。例：`Cookie: name1=value1; name2=value2`</li><li>テンプレートのサポート：テンプレートからCookie値を生成するために、テンプレート名を参照します。</li></ul> |
| 本文のコンテンツタイプ | <ul><li>（任意）使用可能なタイプを選択するか、カスタム値を指定します。</li><li>すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`</li><li>本文データを指定する場合は、コンテンツタイプが必須です。</li></ul> |
| テンプレート変数 | <ul><li>（任意）テンプレートのデータ入力としてテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数にはドット表記で名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。</li></ul> |
| テンプレート | <ul><li>（任意）URL、URLパラメータ、ヘッダー、または本文データで参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、サポートされているフィールドに二重中括弧で囲んだ名前を使用して挿入されます。例：`{{SomeTemplateName}}`。</li><li>OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されたトークンを参照します。</li><li>予約変数`{{tealium_event_payload}}`と`{{tealium_visitor_payload}}`は、マッピングなしで常に使用できます。詳細については、[予約変数](https://docs.tealium.com/connector-template-variables/#reserved-variables)を参照してください。</li></ul> |
| 訪問データに現在の訪問データを含める | <ul><li>現在の訪問データをペイロードに追加します。</li><li>「現在の訪問のイベントデータを除外」が選択されていない場合、これには訪問中のイベントデータも含まれます。</li></ul> |
| 現在の訪問のイベントデータを除外 | <ul><li>現在の訪問データからイベントデータを除外します。</li></ul> |
| 属性名を出力 | <ul><li>属性名が更新された場合、ペイロード内の名前にも更新が反映されます。</li></ul> |
| リダイレクト | <ul><li>メソッドがGETの場合にのみリダイレクトを許可します。</li></ul> |
### HTTPリクエストによるカスタマイズデータの送信（高度）

カスタムリクエストで、ネストされたJSONやXMLなどの複雑なペイロードが必要な場合は、**テンプレート**オプションを使用して、ベンダーのエンドポイントで必要とされる形式のペイロードを構築します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。

| パラメータ | 説明 |
|:-------------------|:---------------------|
| メソッド | <ul><li>（必須）リクエストメソッドとして、`GET`、`POST`、`PUT`、`DELETE`、または`PATCH`を選択します。</li></ul> |
| URL | <ul><li>（必須）リクエストの送信先URLを指定します。</li><li>テンプレートのサポート：テンプレートからURLを生成するには、テンプレート名を参照します。</li></ul> |
| URLパラメータ | <ul><li>（任意）URLに追加するパラメータを指定します。</li><li>テンプレートのサポート：テンプレートからパラメータ値を生成するには、テンプレート名を参照します。</li></ul>|
| ヘッダー | <ul><li>（任意）HTTPヘッダー値をヘッダー名にマッピングします。</li><li>テンプレートのサポート：テンプレートからヘッダー値を生成するには、テンプレート名を参照します。</li></ul> |
| Cookie | <ul><li>（任意）Cookie値をCookie名にマッピングします。</li><li>Cookieは、単一のHTTPヘッダー値として追加されます。例：`Cookie: name1=value1; name2=value2`</li><li>テンプレートのサポート：テンプレートからCookie値を生成するには、テンプレート名を参照します。</li></ul> |
| 本文のコンテンツタイプ | <ul><li>（任意）使用可能なタイプを選択するか、カスタム値を指定します。</li><li>すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`</li><li>本文データを指定する場合は、コンテンツタイプが必要です。</li></ul> |
| 本文データ | <ul><li>（任意）メッセージ本文を構築するためのデータを指定します。</li><li>テンプレートのサポート：テンプレートから本文データを生成するには、テンプレート名を参照します。</li><li>本文のコンテンツタイプが`multipart/form-data`または`application/x-www-form-urlencoded`の場合は値を名前にマッピングします。それ以外の場合は、テンプレート名を参照し、**本文**オプションのみを選択します。</li></ul> |
| テンプレート変数 | <ul><li>（任意）テンプレートへのデータ入力としてテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数には、ドット表記で名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は、通常、データレイヤーのリスト属性から構築されます。</li></ul> |
| テンプレート | <ul><li>（任意）URL、URLパラメータ、ヘッダー、または本文データで参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、サポートされているフィールドに二重波括弧を使用して名前で挿入されます。例：`{{SomeTemplateName}}`。</li><li>OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストから返されたトークンを参照します。</li><li>予約変数`{{tealium_event_payload}}`および`{{tealium_visitor_payload}}`は、マッピングなしで常に使用できます。詳細については、[予約変数](https://docs.tealium.com/connector-template-variables/#reserved-variables)を参照してください。</li></ul> |
| リダイレクト | <ul><li>メソッドがGETの場合にのみリダイレクトを許可します。</li></ul> |

### HTTPリクエストによるバッチデータの送信

#### バッチ制限

このアクションでは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに格納されます。

* リクエストの最大数：100
* 最も古いリクエストからの最大経過時間：60分
* リクエストの最大サイズ：16 MB

#### パラメータ

| パラメータ | 説明 |
|:------------|:------------------|
| メソッド | <ul><li>（必須）リクエストメソッドとして、`GET`、`POST`、`PUT`、`DELETE`、または`PATCH`を選択します。</li></ul> |
| URL | <ul><li>（必須）リクエストの送信先URLを指定します。</li><li>テンプレートのサポート：テンプレートからURLを生成するには、テンプレート名を参照します。</li></ul> |
| URLパラメータ | <ul><li>（任意）URLに追加するパラメータを指定します。</li><li>テンプレートのサポート：テンプレートからパラメータ値を生成するには、テンプレート名を参照します。</li></ul> |
| ヘッダー | <ul><li>（任意）HTTPヘッダー値をヘッダー名にマッピングします。</li><li>テンプレートのサポート：テンプレートからヘッダー値を生成するには、テンプレート名を参照します。</li></ul> |
| Cookie | <ul><li>（任意）Cookie値をCookie名にマッピングします。</li><li>Cookieは、単一のHTTPヘッダー値として追加されます。例：`Cookie: name1=value1; name2=value2`</li><li>テンプレートのサポート：テンプレートからCookie値を生成するには、テンプレート名を参照します。</li></ul> |
| 本文のコンテンツタイプ | <ul><li>（任意）使用可能なタイプを選択するか、カスタム値を指定します。</li><li>すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`</li><li>本文データを指定する場合は、コンテンツタイプが必要です。</li></ul> |
| テンプレート変数 | <ul><li>（任意）テンプレートへのデータ入力としてテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数には、ドット表記で名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は、通常、データレイヤーのリスト属性から構築されます。</li></ul> |
| テンプレート | <ul><li>（任意）URL、URLパラメータ、ヘッダー、または本文データで参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、サポートされているフィールドに二重波括弧を使用して名前で挿入されます。例：`{{SomeTemplateName}}`。</li><li>OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストから返されたトークンを参照します。</li><li>予約変数`{{tealium_event_payload}}`および`{{tealium_visitor_payload}}`は、マッピングなしで常に使用できます。詳細については、[予約変数](https://docs.tealium.com/connector-template-variables/#reserved-variables)を参照してください。</li></ul> |
| 現在の訪問データを含める | <ul><li>現在の訪問データを含める場合は、このチェックボックスをオンにします。</li></ul> |
| 現在の訪問のイベントデータを除外 | <ul><li>現在の訪問データからイベントデータを除外します。</li></ul> |
| 属性名を出力 | <ul><li>属性名が更新された場合、ペイロード内の名前にも更新が反映されます。</li></ul> |
| リダイレクト | <ul><li>メソッドがGETの場合にのみリダイレクトを許可します。</li></ul> |
| タイムアウト | `HTTP`リクエストを介してデータを送信するときに、バッチアクションの完了をシステムが待機する最大時間（秒）を構成します。最小値は`1`、最大値は`10`です。 |

### HTTPリクエストによるカスタマイズされたバッチデータの送信（高度）

カスタムリクエストで、ネストされたJSONやXMLなどの複雑なペイロードが必要な場合は、**テンプレート**オプションを使用して、ベンダーのエンドポイントで必要とされる形式のペイロードを構築します。カスタムリクエストでのテンプレートの使用方法については、[カスタムリクエストの送信 - テンプレート変数ガイド](https://docs.tealium.com/connector-template-variables/)を参照してください。


<blockquote>
[Trace](https://docs.tealium.com/about-trace/)を使用する場合、バッチ処理は無視されます。
</blockquote>


#### バッチ制限

このアクションでは、ベンダーへの大量データ転送をサポートするためにバッチリクエストを使用します。次の3つのしきい値のいずれかに達するまで、リクエストはキューに格納されます。

* リクエストの最大数：100
* 最も古いリクエストからの経過時間（存続時間、TTL）：1～60分
* リクエストの最大サイズ：16 MB
#### パラメータ

| パラメータ      | 説明      |
|:------------|:------------------|
| メソッド       |  <ul><li>（必須）リクエストメソッドとして `GET`、`POST`、`PUT`、`DELETE`、または `PATCH` を選択します。</li></ul>      |
| URL     | <ul><li>（必須）リクエストの送信先URLを指定します。</li><li>テンプレートのサポート：テンプレートからURLを生成するには、テンプレート名を参照します。</li></ul>     |
| 本文のコンテンツタイプ     | <ul><li>（任意）利用可能なタイプを選択するか、カスタム値を指定します。</li><li>すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`</li><li>本文データを指定する場合は、コンテンツタイプが必要です。</li></ul>     |
| 本文データ    | <ul><li>（任意）メッセージ本文を作成するためのデータを指定します。</li><li>テンプレートのサポート：テンプレートから本文データを生成するには、テンプレート名を参照します。</li><li>本文のコンテンツタイプが `multipart/form-data` または `application/x-www-form-urlencoded` の場合は、値を名前にマッピングします。それ以外の場合は、テンプレート名を参照し、`Body` オプションのみを選択します。</li></ul>     |
| プレフィックス | 本文データの前に配置される、リクエスト内で繰り返されない部分です。JSON配列のプレフィックスは開始角括弧（`[`）です。`Custom [` を **プレフィックス** にマッピングします。例：<br/> `[   {     "editable_in_signup": false,     "displayed_for_customers": true    },   {     "editable_in_signup": true,     "displayed_for_customers": true   } ] ` |
| 結合文字列 | 本文データ内の個々のデータ項目を区切る文字または文字列です。JSONオブジェクトの結合文字はコンマ（`,`）です。`Custom ,` を **結合文字列** にマッピングします。例：<br/> `[   {     "editable_in_signup": false,     "displayed_for_customers": true    },  {     "editable_in_signup": true,     "displayed_for_customers": true   } ]`  |
| サフィックス | 本文データの後に配置される、リクエスト内で繰り返されない部分です。JSON配列のプレフィックスは終了角括弧（`]`）です。`Custom ]` を **サフィックス** にマッピングします。例：<br/> `[   {     "editable_in_signup": false,     "displayed_for_customers": true    },   {     "editable_in_signup": true,     "displayed_for_customers": true   } ] ` |
| 最大レコード数   | <ul><li>レコード数の上限です。</li></ul>     |
| 有効期間（分） | <ul><li>有効期間（分単位）です。</li></ul>       |
| URLパラメータ   | <ul><li>（任意）URLに追加するパラメータを指定します。</li><li>テンプレートのサポート：テンプレートからパラメータ値を生成するには、テンプレート名を参照します。</li></ul> |
| ヘッダー   | <ul><li>（任意）HTTPヘッダー値をヘッダー名にマッピングします。</li><li>テンプレートのサポート：テンプレートからヘッダー値を生成するには、テンプレート名を参照します。</li></ul>    |
| ヘッダー   | <ul><li>（任意）HTTPヘッダー値をヘッダー名にマッピングします。</li><li>テンプレートのサポート：テンプレートからヘッダー値を生成するには、テンプレート名を参照します。</li></ul>    |
| テンプレート変数    | <ul><li>（任意）テンプレートへのデータ入力としてテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数にはドット表記で名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。</li></ul>   |
| テンプレート   | <ul><li>（任意）URL、URLパラメータ、ヘッダー、または本文データで参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、サポートされているフィールドに二重波括弧を使用して名前で挿入されます。例：`{{SomeTemplateName}}`。</li><li>OAuthを使用する場合、テンプレート変数 `{{webhook_access_token}}` は認証リクエストによって返されたトークンを参照します。</li><li>予約変数 `{{tealium_event_payload}}` および `{{tealium_visitor_payload}}` は、マッピングなしで常に利用できます。詳細については、[予約変数](https://docs.tealium.com/connector-template-variables/#reserved-variables)を参照してください。</li></ul> |
| タイムアウト | `HTTP` リクエストを介してデータを送信する際に、システムがバッチアクションの完了を待機する最大時間（秒単位）を構成します。最小値は `1`、最大値は `10` です。 |

## イベントデータJSON

イベントに想定されるJSONペイロードには、イベントを構成するすべての標準属性に加えて、イベントを送信したプラットフォーム固有の追加属性が含まれます。たとえば、Webサイトから受信したイベントにはDOM属性とCookie属性が含まれ、モバイルデバイスから受信したイベントにはデバイス属性と通信事業者属性が含まれます。

イベントデータJSONオブジェクト形式の例：

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
            "utag_main__st": 1383678970903,
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

訪問に想定されるJSONペイロードには、その訪問に該当するすべての訪問属性が含まれます。データオブジェクトは属性タイプ別に整理されています。属性が割り当てられていない場合、その属性は訪問オブジェクトに表示されません。現在の訪問に関するデータも、`current_visit` キーの下に含まれます。

訪問データJSONオブジェクト形式の例：

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