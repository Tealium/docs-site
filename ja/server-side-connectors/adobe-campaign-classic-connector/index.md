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

コネクタマーケットプレイスに移動して新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/) の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **サーバーホスト**
  * サーバーホストまたはサーバーアドレスのいずれかが必要です。
  * 例：ドメイン "serverURL" の場合、次の例のURLから `serverURL` をコピーして貼り付けます：`<https://serverURL/nl/jsp/soaprouter.jsp>`
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

このアクションは、バッチリクエストを使用してベンダーへの大量データ転送をサポートします。詳細については、[バッチ処理アクション](https://docs.tealium.com/batched-actions/)を参照してください。リクエストは、次のいずれかの閾値に達するか、プロファイルが公開されるまでキューに入れられます：

* 最大リクエスト数：200
* 最古のリクエストからの最大時間：10分
* リクエストの最大サイズ：1 MB

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| SOAPアクション | 例：`xtk:session#Logon`。<br>この値はSOAPAction HTTPヘッダーに割り当てられます。 |
|SOAPリクエストテンプレート変数|  <ul><li>SOAPリクエストボディプレフィックス、SOAPリクエストボディデータ、SOAPリクエストボディサフィックスのデータ入力用にテンプレート変数を提供します。詳細については [connector-template-variables](https://docs.tealium.com/connector-template-variables/) を参照してください。</li><li>ドット表記でネストされたテンプレート変数を名付けます。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul> |
|SOAPリクエストボディプレフィックス|  <ul><li>SOAPリクエストの開始部分のテンプレートを提供します。</li><li>例：``` <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:xtk:session"><soapenv:Header/><soapenv:Body><urn:Logon><urn:strLogin>USERNAME</urn:strLogin><urn:strPassword>PASSWORD</urn:strPassword><urn:elemParameters> ``` </li></ul> <ul><li>`USERNAME` と `PASSWORD` の場所にあなたのAdobeユーザー名とパスワードを使用します。</li><li>**SOAPリクエストボディプレフィックス** でテンプレート変数を使用します。</li><li>詳細については [about-connector-templates](https://docs.tealium.com/about-connector-templates/) を参照してください。</li></ul> |
|SOAPリクエストボディデータ|  <ul><li>送信されるSOAPリクエストバッチアイテムのテンプレートを提供します。</li><li>SOAPリクエストボディデータでテンプレート変数を使用します。</li></ul> |
|SOAPリクエストボディジョイナー|  <ul><li>バッチ処理時にボディアイテム間で使用する文字または文字列。</li><li>指定されていない場合、空文字列が使用されます。</li></ul> |
|SOAPリクエストボディサフィックス|  <ul><li>SOAPリクエストの終了部分のテンプレートを提供します。</li><li>例：``` </urn:elemParameters></urn:Logon></soapenv:Body></soapenv:Envelope> ``` </li><li>SOAPリクエストボディサフィックスでテンプレート変数を使用します。</li></ul> |
|SOAPレスポンスエラー識別子|  <ul><li>レスポンスに指定されたエラー文字列のいずれか（OR条件）が含まれている場合、それは失敗としてマークされます。</li><li>デフォルトでは、200-299の範囲外のHTTPレスポンスステータスも失敗としてマークされます。</li></ul> |
| 任意のフォルトコードとフォルト文字列レスポンスに対してエラーを投げる | このチェックボックスを選択して、任意のフォルトコードとフォルト文字列レスポンスに対してエラーを投げます。|

### アクション - カスタムSOAPリクエスト送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
| SOAPアクションヘッダー値 | このパラメータは必須です<br>例：`xtk:workflow#PostEvent`。 |
| SOAPリクエストテンプレート変数|  <ul><li>SOAPリクエストボディプレフィックス、SOAPリクエストボディデータ、SOAPリクエストボディサフィックスのデータ入力用にテンプレート変数を提供します。詳細については [connector-template-variables](https://docs.tealium.com/connector-template-variables/) を参照してください。</li><li>ドット表記でネストされたテンプレート変数を名付けます。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul> |
| SOAPリクエストボディテンプレート | このパラメータは必須です<br>送信されるSOAPリクエストボディテンプレートを提供します。詳細については [about-connector-templates](https://docs.tealium.com/about-connector-templates/) を参照してください。<br>テンプレートは、対応するフィールドに名前で注入されます。例：`{{SomeTemplateName}}`。<br>注：Adobe Campaign APIコールにはセッショントークンが必要です。適切な場所にこのトークンを含めることを確認してください。予約されたテンプレートキーワード `{{sessionToken}}` を使用して、このトークンが自動的にテンプレートに含まれるようにします。 |
|SOAPレスポンスエラー識別子|  <ul><li>レスポンスに指定されたエラー文字列のいずれか（OR条件）が含まれている場合、それは失敗としてマークされます。</li><li>デフォルトでは、200-299の範囲外のHTTPレスポンスステータスも失敗としてマークされます。</li></ul> |