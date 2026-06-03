---
title: Adobe Campaign Classic コネクタ構成ガイド
description: この記事では、Customer Data Hub アカウントで Adobe Campaign Classic コネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-campaign-classic-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| カスタムSOAPリクエスト送信（バッチ処理） | ✓ | ✓ |
|カスタムSOAPリクエスト送信| ✓| ✓ |

## 構成の構成

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて]() の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **サーバーホスト**
  * サーバーホストまたはサーバーアドレスのいずれかが必要です。
  * 例：ドメイン &#34;serverURL&#34; の場合、次の例のURLから `serverURL` をコピーして貼り付けます：`&lt;https://serverURL/nl/jsp/soaprouter.jsp&gt;`
  * 認証には、SOAPリクエストボディプレフィックスの一部としてユーザー名とパスワードを提供します。
  * 詳細については、Adobe Campaign Classic アクセス管理ヘルプドキュメントの [アクセス管理](https://experienceleague.adobe.com/docs/campaign-classic/using/configuring-campaign-classic/api/web-service-calls.html?lang=en#connectivity) を参照してください。

* **サーバーアドレス**
  * Adobe Campaign サーバーへの完全なURLを指定します。
  * サーバーホストまたはサーバーアドレスのいずれかが必要です。
  * アドレスが提供された場合、ホストは無視されます。

## アクション構成 - パラメータとオプション

**次へ** をクリックするか、**アクション** タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### カスタムSOAPリクエスト送信（バッチ処理）

#### バッチ制限

このアクションは、バッチリクエストを使用してベンダーへの大量データ転送をサポートします。詳細については、[バッチ処理アクション]()を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：200
* 最古のリクエストからの最大時間：10分
* リクエストの最大サイズ：1 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| SOAPアクション | 例：`xtk:session#Logon`。&lt;br&gt;この値はSOAPAction HTTPヘッダーに割り当てられます。 |
|SOAPリクエストテンプレート変数|  &lt;ul&gt;&lt;li&gt;SOAPリクエストボディプレフィックス、SOAPリクエストボディデータ、SOAPリクエストボディサフィックスのデータ入力用にテンプレート変数を提供します。詳細については  を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を名付けます。&lt;/li&gt;&lt;li&gt;例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt; |
|SOAPリクエストボディプレフィックス|  &lt;ul&gt;&lt;li&gt;SOAPリクエストの開始部分のテンプレートを提供します。&lt;/li&gt;&lt;li&gt;例：``` &lt;soapenv:Envelope xmlns:soapenv=&#34;http://schemas.xmlsoap.org/soap/envelope/&#34; xmlns:urn=&#34;urn:xtk:session&#34;&gt;&lt;soapenv:Header/&gt;&lt;soapenv:Body&gt;&lt;urn:Logon&gt;&lt;urn:strLogin&gt;USERNAME&lt;/urn:strLogin&gt;&lt;urn:strPassword&gt;PASSWORD&lt;/urn:strPassword&gt;&lt;urn:elemParameters&gt; ``` &lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;`USERNAME` と `PASSWORD` の場所にあなたのAdobeユーザー名とパスワードを使用します。&lt;/li&gt;&lt;li&gt;**SOAPリクエストボディプレフィックス** でテンプレート変数を使用します。&lt;/li&gt;&lt;li&gt;詳細については  を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|SOAPリクエストボディデータ|  &lt;ul&gt;&lt;li&gt;送信されるSOAPリクエストバッチアイテムのテンプレートを提供します。&lt;/li&gt;&lt;li&gt;SOAPリクエストボディデータでテンプレート変数を使用します。&lt;/li&gt;&lt;/ul&gt; |
|SOAPリクエストボディジョイナー|  &lt;ul&gt;&lt;li&gt;バッチ処理時にボディアイテム間で使用する文字または文字列。&lt;/li&gt;&lt;li&gt;指定されていない場合、空文字列が使用されます。&lt;/li&gt;&lt;/ul&gt; |
|SOAPリクエストボディサフィックス|  &lt;ul&gt;&lt;li&gt;SOAPリクエストの終了部分のテンプレートを提供します。&lt;/li&gt;&lt;li&gt;例：``` &lt;/urn:elemParameters&gt;&lt;/urn:Logon&gt;&lt;/soapenv:Body&gt;&lt;/soapenv:Envelope&gt; ``` &lt;/li&gt;&lt;li&gt;SOAPリクエストボディサフィックスでテンプレート変数を使用します。&lt;/li&gt;&lt;/ul&gt; |
|SOAPレスポンスエラー識別子|  &lt;ul&gt;&lt;li&gt;レスポンスに指定されたエラー文字列のいずれか（OR条件）が含まれている場合、それは失敗としてマークされます。&lt;/li&gt;&lt;li&gt;デフォルトでは、200-299の範囲外のHTTPレスポンスステータスも失敗としてマークされます。&lt;/li&gt;&lt;/ul&gt; |
| 任意のフォルトコードとフォルト文字列レスポンスに対してエラーを投げる | このチェックボックスを選択して、任意のフォルトコードとフォルト文字列レスポンスに対してエラーを投げます。|

### アクション - カスタムSOAPリクエスト送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
| SOAPアクションヘッダー値 | このパラメータは必須です&lt;br&gt;例：`xtk:workflow#PostEvent`。 |
| SOAPリクエストテンプレート変数|  &lt;ul&gt;&lt;li&gt;SOAPリクエストボディプレフィックス、SOAPリクエストボディデータ、SOAPリクエストボディサフィックスのデータ入力用にテンプレート変数を提供します。詳細については  を参照してください。&lt;/li&gt;&lt;li&gt;ドット表記でネストされたテンプレート変数を名付けます。&lt;/li&gt;&lt;li&gt;例：`items.name`&lt;/li&gt;&lt;li&gt;ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。&lt;/li&gt;&lt;/ul&gt; |
| SOAPリクエストボディテンプレート | このパラメータは必須です&lt;br&gt;送信されるSOAPリクエストボディテンプレートを提供します。詳細については  を参照してください。&lt;br&gt;テンプレートは、対応するフィールドに名前で注入されます。例：`{{SomeTemplateName}}`。&lt;br&gt;注：Adobe Campaign APIコールにはセッショントークンが必要です。適切な場所にこのトークンを含めることを確認してください。予約されたテンプレートキーワード `{{sessionToken}}` を使用して、このトークンが自動的にテンプレートに含まれるようにします。 |
|SOAPレスポンスエラー識別子|  &lt;ul&gt;&lt;li&gt;レスポンスに指定されたエラー文字列のいずれか（OR条件）が含まれている場合、それは失敗としてマークされます。&lt;/li&gt;&lt;li&gt;デフォルトでは、200-299の範囲外のHTTPレスポンスステータスも失敗としてマークされます。&lt;/li&gt;&lt;/ul&gt; |