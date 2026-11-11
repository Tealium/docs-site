---
title: Customer Data Platform（CDP）向けAdobe Campaignコネクタ構成ガイド
description: この記事では、Customer Data HubアカウントでAdobe Campaignコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-campaign-connector/
---## 要件

* Adobe Campaignアカウント
* SOAP API認証情報  
認証情報については、Adobeの担当者にお問い合わせください。
* CDPサーバーの[IPアドレス](https://docs.tealium.com/ip-allow-list/)を許可リストに登録する  

<blockquote>
IPアドレスがAdobeの許可リストに登録されていない場合、トレース機能に次のエラーが表示されます：`Action Failure: Error: received non-successful http response status = 403`
</blockquote>


## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|カスタムSOAPリクエストを送信| ✓| ✗|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。


<blockquote>
このコネクタは、Adobe CampaignのSOAPログオンメソッドを使用してSOAP APIに接続します。詳細については、Adobe Campaignの接続に関するドキュメントを参照してください。
</blockquote>


ベンダーを構成するには、次の手順に従います。

1. 「構成」タブで、コネクタインスタンスのタイトルを入力します。
1. Adobeからアカウント用に提供されたSOAP APIのユーザー名とパスワードを入力します。
1. Adobeからアカウント用に提供されたSOAP APIエンドポイントを入力します。ドメインのみを含めてください。  
例：サーバーパスが`<http://example.com/nl/jsp/soaprouter.jsp>`の場合、このフィールドには「example.com」のみを入力します。
1. 実装に関する追加のメモを入力します。
1. **接続を確立**をクリックして、API接続を確認します。

## アクション構成 — パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション — カスタムSOAPリクエストを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|SOAP Actionヘッダー値|  <ul><li>このパラメータは必須です。</li><li>例：`xtk:workflow#PostEvent`。</li></ul> |
|SOAPリクエストボディテンプレート|  <ul><li>（必須）送信するSOAPリクエストボディテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>サポートされているフィールドに、テンプレート名を二重波括弧で囲んで挿入します。例：`{{SomeTemplateName}}`。</li><li>Adobe Campaign APIの呼び出しにはセッショントークンが必要です。必要な箇所でテンプレートに含めてください。<ul><li>予約済み（事前定義され、自動的に値が構成される）のテンプレートキーワード`{{sessionToken}}`を使用すると、このトークンをテンプレートに含めることができます。</li></ul> </li></ul> |
|SOAPレスポンスエラー識別子|  <ul><li>レスポンスに以下で指定したエラー文字列のいずれか（OR条件）が含まれる場合、失敗としてマークされます。</li><li>デフォルトでは、HTTPレスポンスステータスが200～299の範囲外の場合も失敗としてマークされます。</li></ul> |
|すべてのFault CodeおよびFault Stringレスポンスをエラーとしてスロー|  <ul><li>レスポンスボディに含まれるすべてのFault CodeまたはFault Stringが取得され、エラーとして返されます。</li></ul> |


<blockquote>
追加のヘルプについては、[Adobe Campaign v6.1構成ガイド](https://docs.campaign.adobe.com/doc/AC6.1/en/PDF/configuration-v6.1-en.pdf)を参照してください。
</blockquote>


### 補足事項

* SOAPリクエストボディテンプレートは必須です。
  * サポートされているフィールドにテンプレートを挿入するには、テンプレート名を二重波括弧で囲みます。例：`{{SomeTemplateName}}`。
  * 一般的な構文と拡張機能の詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。

* Adobe Campaign APIの呼び出しにはセッショントークンが必要です。
  * 必要な箇所でテンプレートに含めてください。
  * 予約済みのテンプレートキーワード`{{sessionToken}}`を使用すると、このトークンをテンプレートに含めることができます。
  * 予約済みキーワードは事前定義され、自動的に値が構成されます。

* テンプレート変数は任意です。
  * ネストされたテンプレート変数に名前を付けるには、ドット表記を使用します。例：`items.name`。
  * ネストされたテンプレート変数は通常、データレイヤーのリスト属性から構築されます。
  * 詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。

## 使用例

以下は、PostEvent SOAPリクエストを送信するための構成例です。

|**パラメータ — オプション**| **説明**|
|---| ---|
|SOAPActionヘッダー値|  <ul><li>カスタム値`xtk:workflow#PostEvent`を構成します。</li></ul> |
|SOAPリクエストボディテンプレート変数|  <ul><li>カスタム値`workflow1000 `を`strWorkflowId`に**マッピング**します。</li><li>カスタム値`importTask2000`を`strActivity`に**マッピング**します。</li></ul> |
|SOAPリクエストボディテンプレート|  ``` <SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  xmlns:ns0="urn:xtk:workflow">   <SOAP-ENV:Header />   <SOAP-ENV:Body>     <ns0:PostEvent>       <ns0:sessiontoken>{{sessionToken}}</ns0:sessiontoken>       <ns0:strWorkflowId>{{strWorkflowId}}</ns0:strWorkflowId>       <ns0:strActivity>{{strActivity}}</ns0:strActivity>     </ns0:PostEvent>   </SOAP-ENV:Body> </SOAP-ENV:Envelope> ``` |
|SOAPレスポンスエラー識別子|  <ul><li>カスタム値`SOAP-ENV:Fault`を構成します。</li></ul> |

### リクエスト例

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

### レスポンス例

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
### エラーレスポンスの例

SOAP 呼び出しレスポンスの HTTP ステータスが 200～299 の場合、または「SOAP Response Error Identifier」のいずれかの値が含まれている場合、アクションは失敗と見なされます。この例では、レスポンスに識別子「SOAP-ENV:Server」が含まれているため、アクションは失敗としてマークされます。

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

**Throw errors for any Fault Codes and Fault String Responses** パラメーターを有効にすると、コネクターは本文のレスポンスに含まれるフォールトコードまたはフォールト文字列をエラーとして返します。

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

## ベンダーのドキュメント

* [Adobe Campaign Classic v7：Web サービス呼び出し](https://experienceleague.adobe.com/docs/campaign-classic/using/configuring-campaign-classic/api/web-service-calls.html?lang=en)