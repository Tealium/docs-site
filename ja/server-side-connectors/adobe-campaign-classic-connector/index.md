---
title: Adobe Campaign Classicコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでAdobe Campaign Classicコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-campaign-classic-connector/
---
## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| カスタムSOAPリクエストを送信（バッチ） | ✓ | ✓ |
|カスタムSOAPリクエストを送信| ✓| ✓ |

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の項目を構成します。

* **サーバーホスト**
  * サーバーホストまたはサーバーアドレスのいずれかが必要です。
  * 例：ドメインについては、次のURL例から「serverURL」をコピーして貼り付けます：`<https://serverURL/nl/jsp/soaprouter.jsp>`
  * 認証については、SOAPリクエストボディのプレフィックスの一部としてユーザー名とパスワードを指定します。
  * 詳細については、Adobe Campaign Classicのアクセス管理ヘルプドキュメントにある[アクセス管理](https://experienceleague.adobe.com/docs/campaign-classic/using/configuring-campaign-classic/api/web-service-calls.html?lang=en#connectivity)を参照してください。

* **サーバーアドレス**
  * Adobe Campaignサーバーの完全なURLを指定します。
  * サーバーホストまたはサーバーアドレスのいずれかが必要です。
  * アドレスを指定した場合、ホストは無視されます。

## アクション構成 - パラメーターとオプション

**続行**をクリックしてコネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### カスタムSOAPリクエストを送信（バッチ）

#### バッチの制限

このアクションでは、ベンダーへの大量データ転送に対応するため、バッチリクエストを使用します。詳細については、[バッチアクション](https://docs.tealium.com/batched-actions/)を参照してください。以下のいずれかのしきい値に達するか、プロファイルがパブリッシュされるまで、リクエストはキューに格納されます。

* リクエストの最大数：200
* 最も古いリクエストからの最大経過時間：10分
* リクエストの最大サイズ：1 MB

#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| SOAPアクション | SOAPアクション（例：`xtk:session#Logon`）。<br>この値はSOAPAction HTTPヘッダーに割り当てられます。 |
|SOAPリクエストテンプレート変数| <ul><li>SOAPリクエストボディのプレフィックス、SOAPリクエストボディのデータ、およびSOAPリクエストボディのサフィックスへのデータ入力として、テンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数にはドット表記で名前を付けます。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は、通常、データレイヤーのリスト属性から構築されます。</li></ul> |
|SOAPリクエストボディのプレフィックス| <ul><li>SOAPリクエストの開始部分のテンプレートを指定します。</li><li>例：``` <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:xtk:session"><soapenv:Header/><soapenv:Body><urn:Logon><urn:strLogin>USERNAME</urn:strLogin><urn:strPassword>PASSWORD</urn:strPassword><urn:elemParameters> ``` </li></ul> <ul><li>`USERNAME`と`PASSWORD`をAdobeのユーザー名とパスワードに置き換えてください。</li><li>**SOAPリクエストボディのプレフィックス**でテンプレート変数を使用します。</li><li>詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li></ul> |
|SOAPリクエストボディのデータ| <ul><li>送信するSOAPリクエストのバッチ項目のテンプレートを指定します。</li><li>SOAPリクエストボディのデータでテンプレート変数を使用します。</li></ul> |
|SOAPリクエストボディの結合文字列| <ul><li>バッチ処理時にボディ項目間で使用する文字または文字列です。</li><li>指定しない場合は、空文字列が使用されます。</li></ul> |
|SOAPリクエストボディのサフィックス| <ul><li>SOAPリクエストの終了部分のテンプレートを指定します。</li><li>例：``` </urn:elemParameters></urn:Logon></soapenv:Body></soapenv:Envelope> ``` </li><li>SOAPリクエストボディのサフィックスでテンプレート変数を使用します。</li></ul> |
|SOAPレスポンスエラー識別子| <ul><li>レスポンスに、以下で指定したエラー文字列のいずれか（OR条件）が含まれている場合、失敗としてマークされます。</li><li>デフォルトでは、200～299の範囲外のHTTPレスポンスステータスも失敗としてマークされます。</li></ul> |
| Fault CodeおよびFault Stringレスポンスに対してエラーをスロー | Fault CodeまたはFault Stringレスポンスが返されたときにエラーをスローするには、このチェックボックスを選択します。|

### アクション - カスタムSOAPリクエストを送信

#### パラメーター

|**パラメーター**| **説明**|
|---| ---|
| SOAPアクションヘッダー値 | このパラメーターは必須です。<br>例：`xtk:workflow#PostEvent`。 |
| SOAPリクエストテンプレート変数| <ul><li>SOAPリクエストボディのプレフィックス、SOAPリクエストボディのデータ、およびSOAPリクエストボディのサフィックスへのデータ入力として、テンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数にはドット表記で名前を付けます。</li><li>例：`items.name`</li><li>ネストされたテンプレート変数は、通常、データレイヤーのリスト属性から構築されます。</li></ul> |
| SOAPリクエストボディテンプレート | このパラメーターは必須です。<br>送信するSOAPリクエストボディテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。<br>テンプレートは、サポート対象フィールドに二重波括弧を使用して名前で挿入されます。例：`{{SomeTemplateName}}`。<br>注：Adobe Campaign APIの呼び出しにはセッショントークンが必要です。必要に応じて、テンプレートにセッショントークンを含めてください。事前定義され、自動的に値が構成される予約済みテンプレートキーワード`{{sessionToken}}`を使用すると、このトークンをテンプレートに含めることができます。 |
|SOAPレスポンスエラー識別子| <ul><li>レスポンスに、以下で指定したエラー文字列のいずれか（OR条件）が含まれている場合、失敗としてマークされます。</li><li>デフォルトでは、200～299の範囲外のHTTPレスポンスステータスも失敗としてマークされます。</li></ul> |