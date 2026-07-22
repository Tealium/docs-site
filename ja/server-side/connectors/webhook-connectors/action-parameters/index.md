---
title: アクションパラメータ
description: この記事では、Webhookコネクタアクションの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side/connectors/webhook-connectors/action-parameters/
---
コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタの管理](https://docs.tealium.com/manage-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **基本認証 - ユーザー名**  
APIエンドポイントが基本認証を要求する場合はユーザー名を入力
* **基本認証 - パスワード**  
APIエンドポイントが基本認証を要求する場合はパスワードを入力

コネクタの構成が完了したら、**完了**をクリックします。

## アクション

**続行**をクリックしてコネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - HTTPリクエストを介してイベントデータを送信

#### パラメータ

| パラメータ      | 説明 |
|:------------------|:-------------|
| メソッド       | <ul><li>(必須) リクエストメソッドを選択します。</li><li>**GET**が選択された場合、イベントデータはJSON URLエンコードされたクエリ文字列パラメータとして`data`キーで配信されます。</li></ul>     |
| URL       | <ul><li>(必須) リクエストを送信するURLを提供します。</li><li>テンプレートサポート：テンプレート名を参照してURLを生成します。</li></ul>    |
| URLパラメータ     | <ul><li>(オプション) URLに追加するパラメータを提供します。</li><li>テンプレートサポート：テンプレート名を参照してパラメータ値を生成します。</li></ul>  |
| ヘッダー      | <ul><li>(オプション) HTTPヘッダー値をヘッダー名にマッピングします。</li><li>テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。</li></ul>     |
| クッキー     | <ul><li>(オプション) クッキー値をクッキー名にマッピングします。</li><li>クッキーは単一のHTTPヘッダー値として追加されます。例：`Cookie: name1=value1; name2=value2`</li><li>テンプレートサポート：テンプレート名を参照してクッキー値を生成します。</li></ul>     |
| ボディコンテンツタイプ     | <ul><li>(オプション) 利用可能なタイプを選択するか、カスタム値を提供します。</li><li>すべてのタイプはUTF-8エンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`</li><li>ボディデータが提供される場合、コンテンツタイプが必要です。</li></ul>      |
| テンプレート変数    | <ul><li>(オプション) テンプレートのデータ入力としてテンプレート変数を提供します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記を使用してネストされたテンプレート変数に名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul>   |
| テンプレート             | <ul><li>(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは名前で二重中括弧を使用してサポートされるフィールドに注入されます。例：`{{SomeTemplateName}}`</li><li>OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されるトークンを参照します。</li></ul> |
| 属性名の印刷 | <ul><li>属性名が更新されると、ペイロードの名前が更新を反映します。</li></ul>   |
| リダイレクション           | <ul><li>メソッドがGETの場合のみリダイレクションを許可します。</li></ul>  |

### HTTPリクエストを介して訪問データを送信

#### パラメータ

| パラメータ   | 説明      |
|:----------------|:------------------|
| メソッド       | <ul><li>(必須) リクエストメソッドを選択します。</li><li>**GET**が選択された場合、イベントデータはJSON URLエンコードされたクエリ文字列パラメータとして`data`キーで配信されます。</li></ul>     |
| URL       | <ul><li>(必須) リクエストを送信するURLを提供します。</li><li>テンプレートサポート：テンプレート名を参照してURLを生成します。</li></ul>    |
| URLパラメータ     | <ul><li>(オプション) URLに追加するパラメータを提供します。</li><li>テンプレートサポート：テンプレート名を参照してパラメータ値を生成します。</li></ul>  |
| ヘッダー      | <ul><li>(オプション) HTTPヘッダー値をヘッダー名にマッピングします。</li><li>テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。</li></ul>     |
| クッキー     | <ul><li>(オプション) クッキー値をクッキー名にマッピングします。</li><li>クッキーは単一のHTTPヘッダー値として追加されます。例：`Cookie: name1=value1; name2=value2`</li><li>テンプレートサポート：テンプレート名を参照してクッキー値を生成します。</li></ul>     |
| ボディコンテンツタイプ     | <ul><li>(オプション) 利用可能なタイプを選択するか、カスタム値を提供します。</li><li>すべてのタイプはUTF-8エンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`</li><li>ボディデータが提供される場合、コンテンツタイプが必要です。</li></ul>      |
| テンプレート変数    | <ul><li>(オプション) テンプレートのデータ入力としてテンプレート変数を提供します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記を使用してネストされたテンプレート変数に名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul>   |
| テンプレート             | <ul><li>(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは名前で二重中括弧を使用してサポートされるフィールドに注入されます。例：`{{SomeTemplateName}}`</li><li>OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されるトークンを参照します。</li></ul> |
| 現在の訪問データを訪問データに含める | <ul><li>ペイロードに現在の訪問データを追加します。</li><li>これには、現在の訪問イベントデータが除外されていない場合のイベント訪問データが含まれます。</li></ul> |
| 現在の訪問イベントデータを除外 | <ul><li>現在の訪問データからイベントデータを除外します。</li></ul> |
| 属性名の印刷      | <ul><li>属性名が更新されると、ペイロードの名前が更新を反映します。</li></ul>     |
| リダイレクション    | <ul><li>メソッドがGETの場合のみリダイレクションを許可します。</li></ul>    |

### HTTPリクエストを介してカスタマイズされたデータを送信（高度）

カスタムリクエストがネストされたJSONやXMLなどの複雑なペイロードを必要とする場合は、**テンプレート**オプションを使用して、ベンダーのエンドポイントに必要な形式でペイロードを構築します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。
#### パラメータ

| パラメータ     | 説明    |
|:-------------------|:---------------------|
| メソッド    | <ul><li>(必須) 詳細については、[Webhook送信カスタムリクエストガイド](https://docs.tealium.com/webhook-connector-setup-guide/)を参照してください。</li><li>リクエストメソッドを選択してください。</li></ul>    |
| URL     | <ul><li>(必須) リクエストを送信するURLを提供してください。</li><li>テンプレートサポート：テンプレート名を参照してURLを生成します。</li></ul>     |
| URLパラメータ     | <ul><li>(オプション) URLに追加するパラメータを提供してください。</li><li>テンプレートサポート：テンプレート名を参照してパラメータ値を生成します。</li></ul>|
| ヘッダー    | <ul><li>(オプション) HTTPヘッダー値をヘッダー名にマッピングします。</li><li>テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。</li></ul>   |
| クッキー  | <ul><li>(オプション) クッキー値をクッキー名にマッピングします。</li><li>クッキーは単一のHTTPヘッダー値として追加されます。例：`Cookie: name1=value1; name2=value2`</li><li>テンプレートサポート：テンプレート名を参照してクッキー値を生成します。</li></ul>    |
| ボディコンテンツタイプ  | <ul><li>(オプション) 利用可能なタイプを選択するか、カスタム値を提供してください。</li><li>すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`</li><li>ボディデータが提供される場合、コンテンツタイプが必要です。</li></ul>     |
| ボディデータ   | <ul><li>(オプション) メッセージボディを構築するためのデータを提供してください。</li><li>テンプレートサポート：テンプレート名を参照してボディデータを生成します。</li><li>ボディコンテンツタイプが`multipart/form-data`または`application/x-www-form-urlencoded`の場合は、値を名前にマッピングします。それ以外の場合は、テンプレート名を参照して**ボディ**オプションのみを選択します。</li></ul>   |
| テンプレート変数 | <ul><li>(オプション) テンプレートのデータ入力としてテンプレート変数を提供してください。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記を使用してネストされたテンプレート変数に名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul>  |
| テンプレート     | <ul><li>(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供してください。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例：`{{SomeTemplateName}}`</li><li>OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されるトークンを指します。</li></ul> |
| リダイレクション    | <ul><li>メソッドがGETの場合のみリダイレクションを許可します。</li></ul>    |

## HTTPリクエストを介してバッチデータを送信

#### バッチ制限

このアクションは、バッチリクエストを使用してベンダーへの大量データ転送をサポートします。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。次のいずれかの閾値が満たされるか、プロファイルが公開されるまでリクエストがキューに入れられます：

* 最大リクエスト数：100
* 最古のリクエストからの最大時間：60分
* リクエストの最大サイズ：16 MB

#### パラメータ

| パラメータ      | 説明      |
|:------------|:------------------|
| メソッド       | <ul><li>(必須) 詳細については、[Webhook送信カスタムリクエストガイド](https://docs.tealium.com/webhook-connector-setup-guide/)を参照してください。</li><li>リクエストメソッドを選択してください。</li></ul>     |
| URL     | <ul><li>(必須) リクエストを送信するURLを提供してください。</li><li>テンプレートサポート：テンプレート名を参照してURLを生成します。</li></ul>     |
| URLパラメータ   | <ul><li>(オプション) URLに追加するパラメータを提供してください。</li><li>テンプレートサポート：テンプレート名を参照してパラメータ値を生成します。</li></ul> |
| ヘッダー   | <ul><li>(オプション) HTTPヘッダー値をヘッダー名にマッピングします。</li><li>テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。</li></ul>    |
| クッキー    | <ul><li>(オプション) クッキー値をクッキー名にマッピングします。</li><li>クッキーは単一のHTTPヘッダー値として追加されます。例：`Cookie: name1=value1; name2=value2`</li><li>テンプレートサポート：テンプレート名を参照してクッキー値を生成します。</li></ul>  |
| ボディコンテンツタイプ     | <ul><li>(オプション) 利用可能なタイプを選択するか、カスタム値を提供してください。</li><li>すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`</li><li>ボディデータが提供される場合、コンテンツタイプが必要です。</li></ul>     |
| テンプレート変数    | <ul><li>(オプション) テンプレートのデータ入力としてテンプレート変数を提供してください。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記を使用してネストされたテンプレート変数に名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul>   |
| テンプレート   | <ul><li>(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供してください。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例：`{{SomeTemplateName}}`</li><li>OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されるトークンを指します。</li></ul> |
| 現在の訪問データを含む | <ul><li>現在の訪問データを含める場合は、このチェックボックスを選択してください。</li></ul>   |
| 現在の訪問イベントデータを除外 | <ul><li>現在の訪問データからイベントデータを除外します。</li></ul> |
| 属性名を印刷      | <ul><li>属性名が更新された場合、ペイロードに反映される名前が更新されます。</li></ul>     |
| リダイレクション    | <ul><li>メソッドがGETの場合のみリダイレクションを許可します。</li></ul>    |
| タイムアウト | `HTTP`リクエストを介してデータを送信する際に、システムがバッチアクションを完了するのを待つ最大時間（秒）を構成します。最小値は`1`、最大値は`10`です。 |

### HTTPリクエストを介してバッチカスタムデータを送信（高度）

カスタムリクエストに複雑なペイロード（ネストされたJSONやXMLなど）が必要な場合は、**テンプレート**オプションを使用して、ベンダーのエンドポイントに必要な形式のペイロードを構築します。カスタムリクエスト用のテンプレートを使用する方法の詳細については、[カスタムリクエスト - テンプレート変数ガイド](https://docs.tealium.com/connector-template-variables/)を参照してください。


<blockquote>
[Trace](https://docs.tealium.com/about-trace/)を使用する場合、バッチ処理は無視されます。
</blockquote>


#### バッチ制限

このアクションは、バッチリクエストを使用してベンダーへの大量データ転送をサポートします。次の3つの閾値のいずれかが満たされるまでリクエストがキューに入れられます：

* 最大リクエスト数：100
* 最古のリクエストからの時間（生存時間、TTL）：1分から60分の間
* リクエストの最大サイズ：16 MB
#### パラメータ

| パラメータ      | 説明      |
|:------------|:------------------|
| メソッド       |  <ul><li>(必須) 詳細は[Webhook送信カスタムリクエストガイド](https://docs.tealium.com/webhook-connector-setup-guide/)を参照してください。</li><li>リクエストメソッドを選択します。</li></ul>     |
| URL     | <ul><li>(必須) リクエストを送信するURLを提供してください。</li><li>テンプレートサポート：テンプレート名を参照してURLを生成します。</li></ul>     |
| ボディコンテンツタイプ     | <ul><li>(オプション) 利用可能なタイプを選択するか、カスタム値を提供します。</li><li>すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`</li><li>ボディデータが提供されている場合、コンテンツタイプが必要です。</li></ul>     |
| ボディデータ    | <ul><li>(オプション) メッセージボディを構築するためのデータを提供します。</li><li>テンプレートサポート：テンプレート名を参照してボディデータを生成します。</li><li>ボディコンテンツタイプが`multipart/form-data`または`application/x-www-form-urlencoded`の場合は値を名前にマッピングし、それ以外の場合はテンプレート名を参照して`Body`オプションのみを選択します。</li></ul>     |
| プレフィックス | ボディデータの前に繰り返されないリクエストの部分です。JSON配列のプレフィックスは開き括弧(`[`)です。例として`Custom [`を**プレフィックス**にマッピングします。<br/> `[   {     "editable_in_signup": false,     "displayed_for_customers": true    },   {     "editable_in_signup": true,     "displayed_for_customers": true   } ] ` |
| ジョイナー | ボディデータ内の個々のデータ項目を分離する文字または文字列です。JSONオブジェクトのジョイナーはカンマ(`,`)です。例として`Custom ,`を**ジョイナー**にマッピングします。<br/> `[   {     "editable_in_signup": false,     "displayed_for_customers": true    },  {     "editable_in_signup": true,     "displayed_for_customers": true   } ]`  |
| サフィックス | ボディデータの後に繰り返されないリクエストの部分です。JSON配列のサフィックスは閉じ括弧(`]`)です。例として`Custom ]`を**サフィックス**にマッピングします。<br/> `[   {     "editable_in_signup": false,     "displayed_for_customers": true    },   {     "editable_in_signup": true,     "displayed_for_customers": true   } ] ` |
| レコード数の最大値   | <ul><li>最大レコード数。</li></ul>     |
| 生存時間 (分) | <ul><li>生存時間（分単位）。</li></ul>       |
| URLパラメータ   | <ul><li>(オプション) URLに追加するパラメータを提供します。</li><li>テンプレートサポート：テンプレート名を参照してパラメータ値を生成します。</li></ul> |
| ヘッダー   | <ul><li>(オプション) HTTPヘッダー値をヘッダー名にマッピングします。</li><li>テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。</li></ul>    |
| テンプレート変数    | <ul><li>(オプション) テンプレートにデータ入力としてテンプレート変数を提供します。詳細は[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記でネストされたテンプレート変数を名前付けします。例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul>   |
| テンプレート   | <ul><li>(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。詳細は[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例：`{{SomeTemplateName}}`。</li><li>OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されるトークンを参照します。</li></ul> |
| タイムアウト | `HTTP`リクエストを通じてデータを送信する際にシステムがバッチアクションを完了するのを待つ最大時間（秒単位）を構成します。最小値は`1`で、最大値は`10`です。 |

### イベントデータJSON

イベントに含まれる予想されるJSONペイロードには、イベントの一部であるすべての標準属性と、イベントを送信したプラットフォームに固有の追加属性が含まれます。例えば、ウェブサイトから受信したイベントにはDOMおよびcookie属性が含まれ、モバイルデバイスから受信したイベントにはデバイスおよびキャリア属性が含まれます。

イベントデータJSONオブジェクト形式の例：

```
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

### 訪問データJSON

訪問に含まれる予想されるJSONペイロードには、その訪問に適用されるすべての訪問属性が含まれます。データオブジェクトは属性タイプ別に整理されています。属性が割り当てられていない場合、訪問オブジェクトには表示されません。現在の訪問のデータも`current_visit`キーの下に含まれます。

訪問データJSONオブジェクト形式の例：

```
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