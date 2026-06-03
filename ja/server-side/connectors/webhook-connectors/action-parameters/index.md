---
title: アクションパラメータ
description: この記事では、Webhookコネクタアクションの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side/connectors/webhook-connectors/action-parameters/
---
コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタの管理]()を参照してください。

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
| メソッド       | &lt;ul&gt;&lt;li&gt;(必須) リクエストメソッドを選択します。&lt;/li&gt;&lt;li&gt;**GET**が選択された場合、イベントデータはJSON URLエンコードされたクエリ文字列パラメータとして`data`キーで配信されます。&lt;/li&gt;&lt;/ul&gt;     |
| URL       | &lt;ul&gt;&lt;li&gt;(必須) リクエストを送信するURLを提供します。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してURLを生成します。&lt;/li&gt;&lt;/ul&gt;    |
| URLパラメータ     | &lt;ul&gt;&lt;li&gt;(オプション) URLに追加するパラメータを提供します。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してパラメータ値を生成します。&lt;/li&gt;&lt;/ul&gt;  |
| ヘッダー      | &lt;ul&gt;&lt;li&gt;(オプション) HTTPヘッダー値をヘッダー名にマッピングします。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。&lt;/li&gt;&lt;/ul&gt;     |
| クッキー     | &lt;ul&gt;&lt;li&gt;(オプション) クッキー値をクッキー名にマッピングします。&lt;/li&gt;&lt;li&gt;クッキーは単一のHTTPヘッダー値として追加されます。例：`Cookie: name1=value1; name2=value2`&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してクッキー値を生成します。&lt;/li&gt;&lt;/ul&gt;     |
| ボディコンテンツタイプ     | &lt;ul&gt;&lt;li&gt;(オプション) 利用可能なタイプを選択するか、カスタム値を提供します。&lt;/li&gt;&lt;li&gt;すべてのタイプはUTF-8エンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;ボディデータが提供される場合、コンテンツタイプが必要です。&lt;/li&gt;&lt;/ul&gt;      |
| テンプレート変数    | &lt;ul&gt;&lt;li&gt;(オプション) テンプレートのデータ入力としてテンプレート変数を提供します。詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記を使用してネストされたテンプレート変数に名前を付けます。例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt;   |
| テンプレート             | &lt;ul&gt;&lt;li&gt;(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で二重中括弧を使用してサポートされるフィールドに注入されます。例：`{{SomeTemplateName}}`&lt;/li&gt;&lt;li&gt;OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されるトークンを参照します。&lt;/li&gt;&lt;/ul&gt; |
| 属性名の印刷 | &lt;ul&gt;&lt;li&gt;属性名が更新されると、ペイロードの名前が更新を反映します。&lt;/li&gt;&lt;/ul&gt;   |
| リダイレクション           | &lt;ul&gt;&lt;li&gt;メソッドがGETの場合のみリダイレクションを許可します。&lt;/li&gt;&lt;/ul&gt;  |

### HTTPリクエストを介して訪問データを送信

#### パラメータ

| パラメータ   | 説明      |
|:----------------|:------------------|
| メソッド       | &lt;ul&gt;&lt;li&gt;(必須) リクエストメソッドを選択します。&lt;/li&gt;&lt;li&gt;**GET**が選択された場合、イベントデータはJSON URLエンコードされたクエリ文字列パラメータとして`data`キーで配信されます。&lt;/li&gt;&lt;/ul&gt;     |
| URL       | &lt;ul&gt;&lt;li&gt;(必須) リクエストを送信するURLを提供します。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してURLを生成します。&lt;/li&gt;&lt;/ul&gt;    |
| URLパラメータ     | &lt;ul&gt;&lt;li&gt;(オプション) URLに追加するパラメータを提供します。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してパラメータ値を生成します。&lt;/li&gt;&lt;/ul&gt;  |
| ヘッダー      | &lt;ul&gt;&lt;li&gt;(オプション) HTTPヘッダー値をヘッダー名にマッピングします。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。&lt;/li&gt;&lt;/ul&gt;     |
| クッキー     | &lt;ul&gt;&lt;li&gt;(オプション) クッキー値をクッキー名にマッピングします。&lt;/li&gt;&lt;li&gt;クッキーは単一のHTTPヘッダー値として追加されます。例：`Cookie: name1=value1; name2=value2`&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してクッキー値を生成します。&lt;/li&gt;&lt;/ul&gt;     |
| ボディコンテンツタイプ     | &lt;ul&gt;&lt;li&gt;(オプション) 利用可能なタイプを選択するか、カスタム値を提供します。&lt;/li&gt;&lt;li&gt;すべてのタイプはUTF-8エンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;ボディデータが提供される場合、コンテンツタイプが必要です。&lt;/li&gt;&lt;/ul&gt;      |
| テンプレート変数    | &lt;ul&gt;&lt;li&gt;(オプション) テンプレートのデータ入力としてテンプレート変数を提供します。詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記を使用してネストされたテンプレート変数に名前を付けます。例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt;   |
| テンプレート             | &lt;ul&gt;&lt;li&gt;(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で二重中括弧を使用してサポートされるフィールドに注入されます。例：`{{SomeTemplateName}}`&lt;/li&gt;&lt;li&gt;OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されるトークンを参照します。&lt;/li&gt;&lt;/ul&gt; |
| 現在の訪問データを訪問データに含める | &lt;ul&gt;&lt;li&gt;ペイロードに現在の訪問データを追加します。&lt;/li&gt;&lt;li&gt;これには、現在の訪問イベントデータが除外されていない場合のイベント訪問データが含まれます。&lt;/li&gt;&lt;/ul&gt; |
| 現在の訪問イベントデータを除外 | &lt;ul&gt;&lt;li&gt;現在の訪問データからイベントデータを除外します。&lt;/li&gt;&lt;/ul&gt; |
| 属性名の印刷      | &lt;ul&gt;&lt;li&gt;属性名が更新されると、ペイロードの名前が更新を反映します。&lt;/li&gt;&lt;/ul&gt;     |
| リダイレクション    | &lt;ul&gt;&lt;li&gt;メソッドがGETの場合のみリダイレクションを許可します。&lt;/li&gt;&lt;/ul&gt;    |

### HTTPリクエストを介してカスタマイズされたデータを送信（高度）

カスタムリクエストがネストされたJSONやXMLなどの複雑なペイロードを必要とする場合は、**テンプレート**オプションを使用して、ベンダーのエンドポイントに必要な形式でペイロードを構築します。詳細については、を参照してください。
#### パラメータ

| パラメータ     | 説明    |
|:-------------------|:---------------------|
| メソッド    | &lt;ul&gt;&lt;li&gt;(必須) 詳細については、[Webhook送信カスタムリクエストガイド]()を参照してください。&lt;/li&gt;&lt;li&gt;リクエストメソッドを選択してください。&lt;/li&gt;&lt;/ul&gt;    |
| URL     | &lt;ul&gt;&lt;li&gt;(必須) リクエストを送信するURLを提供してください。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してURLを生成します。&lt;/li&gt;&lt;/ul&gt;     |
| URLパラメータ     | &lt;ul&gt;&lt;li&gt;(オプション) URLに追加するパラメータを提供してください。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してパラメータ値を生成します。&lt;/li&gt;&lt;/ul&gt;|
| ヘッダー    | &lt;ul&gt;&lt;li&gt;(オプション) HTTPヘッダー値をヘッダー名にマッピングします。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。&lt;/li&gt;&lt;/ul&gt;   |
| クッキー  | &lt;ul&gt;&lt;li&gt;(オプション) クッキー値をクッキー名にマッピングします。&lt;/li&gt;&lt;li&gt;クッキーは単一のHTTPヘッダー値として追加されます。例：`Cookie: name1=value1; name2=value2`&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してクッキー値を生成します。&lt;/li&gt;&lt;/ul&gt;    |
| ボディコンテンツタイプ  | &lt;ul&gt;&lt;li&gt;(オプション) 利用可能なタイプを選択するか、カスタム値を提供してください。&lt;/li&gt;&lt;li&gt;すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;ボディデータが提供される場合、コンテンツタイプが必要です。&lt;/li&gt;&lt;/ul&gt;     |
| ボディデータ   | &lt;ul&gt;&lt;li&gt;(オプション) メッセージボディを構築するためのデータを提供してください。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してボディデータを生成します。&lt;/li&gt;&lt;li&gt;ボディコンテンツタイプが`multipart/form-data`または`application/x-www-form-urlencoded`の場合は、値を名前にマッピングします。それ以外の場合は、テンプレート名を参照して**ボディ**オプションのみを選択します。&lt;/li&gt;&lt;/ul&gt;   |
| テンプレート変数 | &lt;ul&gt;&lt;li&gt;(オプション) テンプレートのデータ入力としてテンプレート変数を提供してください。詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記を使用してネストされたテンプレート変数に名前を付けます。例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt;  |
| テンプレート     | &lt;ul&gt;&lt;li&gt;(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供してください。詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例：`{{SomeTemplateName}}`&lt;/li&gt;&lt;li&gt;OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されるトークンを指します。&lt;/li&gt;&lt;/ul&gt; |
| リダイレクション    | &lt;ul&gt;&lt;li&gt;メソッドがGETの場合のみリダイレクションを許可します。&lt;/li&gt;&lt;/ul&gt;    |

## HTTPリクエストを介してバッチデータを送信

#### バッチ制限

このアクションは、バッチリクエストを使用してベンダーへの大量データ転送をサポートします。詳細については、[バッチアクション]()を参照してください。次のいずれかの閾値が満たされるか、プロファイルが公開されるまでリクエストがキューに入れられます：

* 最大リクエスト数：100
* 最古のリクエストからの最大時間：60分
* リクエストの最大サイズ：16 MB

#### パラメータ

| パラメータ      | 説明      |
|:------------|:------------------|
| メソッド       | &lt;ul&gt;&lt;li&gt;(必須) 詳細については、[Webhook送信カスタムリクエストガイド]()を参照してください。&lt;/li&gt;&lt;li&gt;リクエストメソッドを選択してください。&lt;/li&gt;&lt;/ul&gt;     |
| URL     | &lt;ul&gt;&lt;li&gt;(必須) リクエストを送信するURLを提供してください。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してURLを生成します。&lt;/li&gt;&lt;/ul&gt;     |
| URLパラメータ   | &lt;ul&gt;&lt;li&gt;(オプション) URLに追加するパラメータを提供してください。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してパラメータ値を生成します。&lt;/li&gt;&lt;/ul&gt; |
| ヘッダー   | &lt;ul&gt;&lt;li&gt;(オプション) HTTPヘッダー値をヘッダー名にマッピングします。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。&lt;/li&gt;&lt;/ul&gt;    |
| クッキー    | &lt;ul&gt;&lt;li&gt;(オプション) クッキー値をクッキー名にマッピングします。&lt;/li&gt;&lt;li&gt;クッキーは単一のHTTPヘッダー値として追加されます。例：`Cookie: name1=value1; name2=value2`&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してクッキー値を生成します。&lt;/li&gt;&lt;/ul&gt;  |
| ボディコンテンツタイプ     | &lt;ul&gt;&lt;li&gt;(オプション) 利用可能なタイプを選択するか、カスタム値を提供してください。&lt;/li&gt;&lt;li&gt;すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;ボディデータが提供される場合、コンテンツタイプが必要です。&lt;/li&gt;&lt;/ul&gt;     |
| テンプレート変数    | &lt;ul&gt;&lt;li&gt;(オプション) テンプレートのデータ入力としてテンプレート変数を提供してください。詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記を使用してネストされたテンプレート変数に名前を付けます。例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt;   |
| テンプレート   | &lt;ul&gt;&lt;li&gt;(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供してください。詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例：`{{SomeTemplateName}}`&lt;/li&gt;&lt;li&gt;OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されるトークンを指します。&lt;/li&gt;&lt;/ul&gt; |
| 現在の訪問データを含む | &lt;ul&gt;&lt;li&gt;現在の訪問データを含める場合は、このチェックボックスを選択してください。&lt;/li&gt;&lt;/ul&gt;   |
| 現在の訪問イベントデータを除外 | &lt;ul&gt;&lt;li&gt;現在の訪問データからイベントデータを除外します。&lt;/li&gt;&lt;/ul&gt; |
| 属性名を印刷      | &lt;ul&gt;&lt;li&gt;属性名が更新された場合、ペイロードに反映される名前が更新されます。&lt;/li&gt;&lt;/ul&gt;     |
| リダイレクション    | &lt;ul&gt;&lt;li&gt;メソッドがGETの場合のみリダイレクションを許可します。&lt;/li&gt;&lt;/ul&gt;    |
| タイムアウト | `HTTP`リクエストを介してデータを送信する際に、システムがバッチアクションを完了するのを待つ最大時間（秒）を構成します。最小値は`1`、最大値は`10`です。 |

### HTTPリクエストを介してバッチカスタムデータを送信（高度）

カスタムリクエストに複雑なペイロード（ネストされたJSONやXMLなど）が必要な場合は、**テンプレート**オプションを使用して、ベンダーのエンドポイントに必要な形式のペイロードを構築します。カスタムリクエスト用のテンプレートを使用する方法の詳細については、[カスタムリクエスト - テンプレート変数ガイド]()を参照してください。

 [Trace]()を使用する場合、バッチ処理は無視されます。

#### バッチ制限

このアクションは、バッチリクエストを使用してベンダーへの大量データ転送をサポートします。次の3つの閾値のいずれかが満たされるまでリクエストがキューに入れられます：

* 最大リクエスト数：100
* 最古のリクエストからの時間（生存時間、TTL）：1分から60分の間
* リクエストの最大サイズ：16 MB
#### パラメータ

| パラメータ      | 説明      |
|:------------|:------------------|
| メソッド       |  &lt;ul&gt;&lt;li&gt;(必須) 詳細は[Webhook送信カスタムリクエストガイド]()を参照してください。&lt;/li&gt;&lt;li&gt;リクエストメソッドを選択します。&lt;/li&gt;&lt;/ul&gt;     |
| URL     | &lt;ul&gt;&lt;li&gt;(必須) リクエストを送信するURLを提供してください。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してURLを生成します。&lt;/li&gt;&lt;/ul&gt;     |
| ボディコンテンツタイプ     | &lt;ul&gt;&lt;li&gt;(オプション) 利用可能なタイプを選択するか、カスタム値を提供します。&lt;/li&gt;&lt;li&gt;すべてのタイプはUTF-8でエンコードされ、ヘッダーとして追加されます。例：`Content-Type: text/plain; charset=UTF-8`&lt;/li&gt;&lt;li&gt;ボディデータが提供されている場合、コンテンツタイプが必要です。&lt;/li&gt;&lt;/ul&gt;     |
| ボディデータ    | &lt;ul&gt;&lt;li&gt;(オプション) メッセージボディを構築するためのデータを提供します。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してボディデータを生成します。&lt;/li&gt;&lt;li&gt;ボディコンテンツタイプが`multipart/form-data`または`application/x-www-form-urlencoded`の場合は値を名前にマッピングし、それ以外の場合はテンプレート名を参照して`Body`オプションのみを選択します。&lt;/li&gt;&lt;/ul&gt;     |
| プレフィックス | ボディデータの前に繰り返されないリクエストの部分です。JSON配列のプレフィックスは開き括弧(`[`)です。例として`Custom [`を**プレフィックス**にマッピングします。&lt;br/&gt; `[   {     &#34;editable_in_signup&#34;: false,     &#34;displayed_for_customers&#34;: true    },   {     &#34;editable_in_signup&#34;: true,     &#34;displayed_for_customers&#34;: true   } ] ` |
| ジョイナー | ボディデータ内の個々のデータ項目を分離する文字または文字列です。JSONオブジェクトのジョイナーはカンマ(`,`)です。例として`Custom ,`を**ジョイナー**にマッピングします。&lt;br/&gt; `[   {     &#34;editable_in_signup&#34;: false,     &#34;displayed_for_customers&#34;: true    },  {     &#34;editable_in_signup&#34;: true,     &#34;displayed_for_customers&#34;: true   } ]`  |
| サフィックス | ボディデータの後に繰り返されないリクエストの部分です。JSON配列のサフィックスは閉じ括弧(`]`)です。例として`Custom ]`を**サフィックス**にマッピングします。&lt;br/&gt; `[   {     &#34;editable_in_signup&#34;: false,     &#34;displayed_for_customers&#34;: true    },   {     &#34;editable_in_signup&#34;: true,     &#34;displayed_for_customers&#34;: true   } ] ` |
| レコード数の最大値   | &lt;ul&gt;&lt;li&gt;最大レコード数。&lt;/li&gt;&lt;/ul&gt;     |
| 生存時間 (分) | &lt;ul&gt;&lt;li&gt;生存時間（分単位）。&lt;/li&gt;&lt;/ul&gt;       |
| URLパラメータ   | &lt;ul&gt;&lt;li&gt;(オプション) URLに追加するパラメータを提供します。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してパラメータ値を生成します。&lt;/li&gt;&lt;/ul&gt; |
| ヘッダー   | &lt;ul&gt;&lt;li&gt;(オプション) HTTPヘッダー値をヘッダー名にマッピングします。&lt;/li&gt;&lt;li&gt;テンプレートサポート：テンプレート名を参照してヘッダー値を生成します。&lt;/li&gt;&lt;/ul&gt;    |
| テンプレート変数    | &lt;ul&gt;&lt;li&gt;(オプション) テンプレートにデータ入力としてテンプレート変数を提供します。詳細はを参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を名前付けします。例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt;   |
| テンプレート   | &lt;ul&gt;&lt;li&gt;(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。詳細はを参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で二重中括弧によってサポートされるフィールドに注入されます。例：`{{SomeTemplateName}}`。&lt;/li&gt;&lt;li&gt;OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されるトークンを参照します。&lt;/li&gt;&lt;/ul&gt; |
| タイムアウト | `HTTP`リクエストを通じてデータを送信する際にシステムがバッチアクションを完了するのを待つ最大時間（秒単位）を構成します。最小値は`1`で、最大値は`10`です。 |

### イベントデータJSON

イベントに含まれる予想されるJSONペイロードには、イベントの一部であるすべての標準属性と、イベントを送信したプラットフォームに固有の追加属性が含まれます。例えば、ウェブサイトから受信したイベントにはDOMおよびcookie属性が含まれ、モバイルデバイスから受信したイベントにはデバイスおよびキャリア属性が含まれます。

イベントデータJSONオブジェクト形式の例：

```
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
            &#34;utag_main__st&#34;: 1383678970903,
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

### 訪問データJSON

訪問に含まれる予想されるJSONペイロードには、その訪問に適用されるすべての訪問属性が含まれます。データオブジェクトは属性タイプ別に整理されています。属性が割り当てられていない場合、訪問オブジェクトには表示されません。現在の訪問のデータも`current_visit`キーの下に含まれます。

訪問データJSONオブジェクト形式の例：

```
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