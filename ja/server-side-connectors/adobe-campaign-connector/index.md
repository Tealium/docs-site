---
title: AudienceStream用Adobe Campaignコネクタ構成ガイド
description: この記事では、お客様のCustomer Data HubアカウントでAdobe Campaignコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-campaign-connector/
---## 必要条件

* Adobe Campaignアカウント
* SOAP APIクレデンシャル  
クレデンシャルについては、Adobeの担当者にお問い合わせください。
* AudienceStreamサーバーの[IPアドレス](https://docs.tealium.com/ip-allow-list/)をホワイトリストに登録  

<blockquote>
AdobeによってIPアドレスがホワイトリストに登録されていない場合、トレース機能は次のエラーを表示します：`Action Failure: Error: received non-successful http response status = 403`
</blockquote>


## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|カスタムSOAPリクエストの送信| ✓| ✗|

## 構成方法

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/)の記事を参照してください。


<blockquote>
このコネクタはAdobe CampaignのSOAPログオンメソッドを使用してSOAP APIに接続します。詳細については、Adobe Campaignの接続ドキュメントを参照してください。
</blockquote>


ベンダーを構成するには、以下の手順に従います：

1. 構成タブでコネクタインスタンスのタイトルを入力します。
1. Adobeから受け取ったアカウントのSOAP APIユーザー名とパスワードを入力します。
1. Adobeから受け取ったアカウントのSOAP APIエンドポイントを入力します。ドメインのみを含めます。  
例：サーバーパスが`<http://example.com/nl/jsp/soaprouter.jsp>`の場合、このフィールドに「example.com」とだけ入力します。
1. 実装に関する追加のメモを提供します。
1. **接続を確立**をクリックしてAPIの接続性を確認します。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - カスタムSOAPリクエストの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|SOAPアクションヘッダー値|  <ul><li>このパラメータは必須です</li><li>例：`xtk:workflow#PostEvent`。</li></ul> |
|SOAPリクエストボディテンプレート|  <ul><li>(必須) 送信するSOAPリクエストボディテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは名前で二重中括弧で囲まれたサポートされるフィールドに注入されます。例えば、`{{SomeTemplateName}}`。</li><li>Adobe Campaign APIコールにはセッショントークンが必要です。適切な場所にそれをテンプレートに含めてください。<ul><li>このトークンをテンプレートに含めるために、予約済みのテンプレートキーワード`{{sessionToken}}`を使用します。</li></ul></li></ul> |
|SOAPレスポンスエラー識別子|  <ul><li>レスポンスに以下のいずれかのエラー文字列が含まれている場合（OR条件）、それは失敗としてマークされます。</li><li>デフォルトでは、200-299の範囲外のHTTPレスポンスステータスも失敗としてマークされます。</li></ul> |
|任意のフォルトコードとフォルト文字列レスポンスに対してエラーを投げる|  <ul><li>ボディレスポンスに含まれる任意のフォルトコードまたはフォルト文字列はキャプチャされ、エラーとして返されます。</li></ul> |


<blockquote>
追加のヘルプについては、[Adobe Campaign v6.1構成ガイド](https://docs.campaign.adobe.com/doc/AC6.1/en/PDF/configuration-v6.1-en.pdf)を参照してください。
</blockquote>


### 追加のメモ

* SOAPリクエストボディテンプレートが必要です。
  * テンプレートをサポートされるフィールドに注入するには、その名前を二重中括弧で囲みます。例えば、`{{SomeTemplateName}}`。
  * 一般的な構文と拡張についての詳細は、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。

* Adobe Campaign APIコールにはセッショントークンが必要です
  * 適切な場所にそれをテンプレートに含めてください。
  * このトークンをテンプレートに含めるために、予約済みのテンプレートキーワード`{{sessionToken}}`を使用します。
  * 予約済みキーワードはあらかじめ定義され、自動的に入力されます。

* テンプレート変数はオプションです。
  * ネストされたテンプレート変数に名前を付けるには、ドット表記を使用します。例えば、`items.name`。
  * ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。
  * 詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。


## 使用例

PostEvent SOAPリクエストを送信するためのサンプル構成です。

|**パラメータ - オプション**| **説明**|
|---| ---|
|SOAPアクションヘッダー値|  <ul><li>`xtk:workflow#PostEvent`のカスタム値を構成</li></ul> |
|SOAPリクエストボディテンプレート変数|  <ul><li>**Map** カスタム値の `workflow1000 `**To** `strWorkflowId`</li><li>**Map** カスタム値の `importTask2000` **To** `strActivity`</li></ul> |
|SOAPリクエストボディテンプレート|  ``` <SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  xmlns:ns0="urn:xtk:workflow">   <SOAP-ENV:Header />   <SOAP-ENV:Body>     <ns0:PostEvent>       <ns0:sessiontoken>{{sessionToken}}</ns0:sessiontoken>       <ns0:strWorkflowId>{{strWorkflowId}}</ns0:strWorkflowId>       <ns0:strActivity>{{strActivity}}</ns0:strActivity>     </ns0:PostEvent>   </SOAP-ENV:Body> </SOAP-ENV:Envelope> ``` |
|SOAPレスポンスエラー識別子|  <ul><li>`SOAP-ENV:Fault`のカスタム値を構成</li></ul> |

### 例のリクエスト

```xml
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"
	xmlns:ns0="urn:xtk:workflow">
	<SOAP-ENV:Header />
	<SOAP-ENV:Body>
		<ns0:PostEvent>
			<ns0:sessiontoken>EXAMPLE_TEALIUM_POPULATED_TOKEN</ns0:sessiontoken>
            <ns0:strWorkflowId>workflow1000</ns0:strWorkflowId>
            <ns0:strActivity>importTask2000</ns0:strActivity>
		</ns0:PostEvent>
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope>

```

### 例のレスポンス

```xml
<?xml version='1.0'?>
	<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema'
		xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:ns='urn:xtk:workflow'
		xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
		<SOAP-ENV:Body>
			<PostEventResponse xmlns='urn:xtk:workflow'
				SOAP-ENV:encodingStyle='http://schemas.xmlsoap.org/soap/encoding/'></PostEventResponse>
		</SOAP-ENV:Body>
	</SOAP-ENV:Envelope>

```
### 例外エラーレスポンス

SOAPコールレスポンスのHTTPステータスが200-299である場合、または「SOAPレスポンスエラー識別子」のいずれかを含む場合、アクションは失敗と見なされます。この例では、レスポンスに識別子「SOAP-ENV:Server」が含まれているため、アクションは失敗とマークされます。

```xml
<?xml version='1.0'?>
	<SOAP-ENV:Envelope xmlns:xsd='http://www.w3.org/2001/XMLSchema'
		xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance' xmlns:SOAP-ENV='http://schemas.xmlsoap.org/soap/envelope/'>
		<SOAP-ENV:Body>
			<SOAP-ENV:Fault>
				<faultcode>SOAP-ENV:Server</faultcode>
				<faultstring xsi:type='xsd:string'>SOP-330011 Error while executing
					the method 'PostEvent' of service 'xtk:workflow'.</faultstring>
			</SOAP-ENV:Fault>
		</SOAP-ENV:Body>
	</SOAP-ENV:Envelope>

```

**フォルトコードとフォルト文字列レスポンスのエラーを投げる** パラメータを有効にすると、コネクタはボディレスポンスに含まれるフォルトコードまたはフォルト文字列をエラーとして返します：

```xml
</soapenv:Body>
</soapenv:Envelope>; error_identifier = SOP-330011; Action Result Response: Http Response 200 <?xml version='1.0'?><SOAP-ENV:Envelope xmlns:xsd='<http://www.w3.org/2001/XMLSchema>' xmlns:xsi='<http://www.w3.org/2001/XMLSchema-instance>' xmlns:SOAP-ENV='<http://schemas.xmlsoap.org/soap/envelope/>'><SOAP-ENV:Body><SOAP-ENV:Fault><faultcode>SOAP-ENV:Server</faultcode><faultstring xsi:type='xsd:string'>SOP-330011 Error while executing the method 'addAbandonedCart' of service 'va:abandoned_cart_event'.</faultstring><detail xsi:type='xsd:string'>ODB-240000 ODBC error: [Microsoft][SQL Server Native Client 11.0][SQL Server]Transaction (Process ID 108) was deadlocked on lock | communication buffer resources with another process and has been chosen as the deadlock victim. Rerun the transaction. SQLState: 40001
XSV-350023 Unable to save document of type 'abandoned_cart_events (va:abandoned_cart_event)'.
SOP-330011 Error while executing the method 'Write' of service 'xtk:persist|xtk:session'.</detail>
</SOAP-ENV:Fault>
</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

```xml
 <soapenv:Body>
<urn:addAbandonedCart>
         <urn:sessiontoken> {{ sessionToken }} </urn:sessiontoken>
         <urn:days_to_departure> {{ days_to_departure }} </urn:days_to_departure>
         <urn:recipient_id> {{ recipient_id }} </urn:recipient_id>
         <urn:abandoned_type> {{ abandoned_type }} </urn:abandoned_type>
         <urn:msg_id> {{ msg_id }} </urn:msg_id>
         <urn:origin_code> {{ origin_code }} </urn:origin_code>
         <urn:triggerType> {{ triggerType }} </urn:triggerType>
         <urn:velocity_id> {{ velocity_id }} </urn:velocity_id>
         <urn:timeGMT> {{ timeGMT }} </urn:timeGMT>
         <urn:experianId> {{ experianId }} </urn:experianId>
         <urn:main_dest_code> {{ main_dest_code }} </urn:main_dest_code>
</urn:addAbandonedCart>
</soapenv:Body>
</soapenv:Envelope>; error_identifier = SOP-330011; Action Time: 5088 ms
```

## ベンダー文書

* [Adobe Campaign Classic v7: Webサービスコール](https://experienceleague.adobe.com/docs/campaign-classic/using/configuring-campaign-classic/api/web-service-calls.html?lang=en)