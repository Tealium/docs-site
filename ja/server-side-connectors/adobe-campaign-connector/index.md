---
title: AudienceStream用Adobe Campaignコネクタ構成ガイド
description: この記事では、お客様のCustomer Data HubアカウントでAdobe Campaignコネクタを構成する方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-campaign-connector/
---## 必要条件

* Adobe Campaignアカウント
* SOAP APIクレデンシャル  
クレデンシャルについては、Adobeの担当者にお問い合わせください。
* AudienceStreamサーバーの[IPアドレス]()をホワイトリストに登録  
AdobeによってIPアドレスがホワイトリストに登録されていない場合、トレース機能は次のエラーを表示します：`Action Failure: Error: received non-successful http response status = 403`

## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|カスタムSOAPリクエストの送信| ✓| ✗|

## 構成方法

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて]()の記事を参照してください。

このコネクタはAdobe CampaignのSOAPログオンメソッドを使用してSOAP APIに接続します。詳細については、Adobe Campaignの接続ドキュメントを参照してください。

ベンダーを構成するには、以下の手順に従います：

1. 構成タブでコネクタインスタンスのタイトルを入力します。
1. Adobeから受け取ったアカウントのSOAP APIユーザー名とパスワードを入力します。
1. Adobeから受け取ったアカウントのSOAP APIエンドポイントを入力します。ドメインのみを含めます。  
例：サーバーパスが`&lt;http://example.com/nl/jsp/soaprouter.jsp&gt;`の場合、このフィールドに「example.com」とだけ入力します。
1. 実装に関する追加のメモを提供します。
1. **接続を確立**をクリックしてAPIの接続性を確認します。

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - カスタムSOAPリクエストの送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|SOAPアクションヘッダー値|  &lt;ul&gt;&lt;li&gt;このパラメータは必須です&lt;/li&gt;&lt;li&gt;例：`xtk:workflow#PostEvent`。&lt;/li&gt;&lt;/ul&gt; |
|SOAPリクエストボディテンプレート|  &lt;ul&gt;&lt;li&gt;(必須) 送信するSOAPリクエストボディテンプレートを提供します。詳細については、を参照してください。&lt;/li&gt;&lt;li&gt;テンプレートは名前で二重中括弧で囲まれたサポートされるフィールドに注入されます。例えば、`{{SomeTemplateName}}`。&lt;/li&gt;&lt;li&gt;Adobe Campaign APIコールにはセッショントークンが必要です。適切な場所にそれをテンプレートに含めてください。&lt;ul&gt;&lt;li&gt;このトークンをテンプレートに含めるために、予約済みのテンプレートキーワード`{{sessionToken}}`を使用します。&lt;/li&gt;&lt;/ul&gt;&lt;/li&gt;&lt;/ul&gt; |
|SOAPレスポンスエラー識別子|  &lt;ul&gt;&lt;li&gt;レスポンスに以下のいずれかのエラー文字列が含まれている場合（OR条件）、それは失敗としてマークされます。&lt;/li&gt;&lt;li&gt;デフォルトでは、200-299の範囲外のHTTPレスポンスステータスも失敗としてマークされます。&lt;/li&gt;&lt;/ul&gt; |
|任意のフォルトコードとフォルト文字列レスポンスに対してエラーを投げる|  &lt;ul&gt;&lt;li&gt;ボディレスポンスに含まれる任意のフォルトコードまたはフォルト文字列はキャプチャされ、エラーとして返されます。&lt;/li&gt;&lt;/ul&gt; |

追加のヘルプについては、[Adobe Campaign v6.1構成ガイド](https://docs.campaign.adobe.com/doc/AC6.1/en/PDF/configuration-v6.1-en.pdf)を参照してください。

### 追加のメモ

* SOAPリクエストボディテンプレートが必要です。
  * テンプレートをサポートされるフィールドに注入するには、その名前を二重中括弧で囲みます。例えば、`{{SomeTemplateName}}`。
  * 一般的な構文と拡張についての詳細は、を参照してください。

* Adobe Campaign APIコールにはセッショントークンが必要です
  * 適切な場所にそれをテンプレートに含めてください。
  * このトークンをテンプレートに含めるために、予約済みのテンプレートキーワード`{{sessionToken}}`を使用します。
  * 予約済みキーワードはあらかじめ定義され、自動的に入力されます。

* テンプレート変数はオプションです。
  * ネストされたテンプレート変数に名前を付けるには、ドット表記を使用します。例えば、`items.name`。
  * ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。
  * 詳細については、を参照してください。


## 使用例

PostEvent SOAPリクエストを送信するためのサンプル構成です。

|**パラメータ - オプション**| **説明**|
|---| ---|
|SOAPアクションヘッダー値|  &lt;ul&gt;&lt;li&gt;`xtk:workflow#PostEvent`のカスタム値を構成&lt;/li&gt;&lt;/ul&gt; |
|SOAPリクエストボディテンプレート変数|  &lt;ul&gt;&lt;li&gt;**Map** カスタム値の `workflow1000 `**To** `strWorkflowId`&lt;/li&gt;&lt;li&gt;**Map** カスタム値の `importTask2000` **To** `strActivity`&lt;/li&gt;&lt;/ul&gt; |
|SOAPリクエストボディテンプレート|  ``` &lt;SOAP-ENV:Envelope xmlns:SOAP-ENV=&#34;http://schemas.xmlsoap.org/soap/envelope/&#34;  xmlns:ns0=&#34;urn:xtk:workflow&#34;&gt;   &lt;SOAP-ENV:Header /&gt;   &lt;SOAP-ENV:Body&gt;     &lt;ns0:PostEvent&gt;       &lt;ns0:sessiontoken&gt;{{sessionToken}}&lt;/ns0:sessiontoken&gt;       &lt;ns0:strWorkflowId&gt;{{strWorkflowId}}&lt;/ns0:strWorkflowId&gt;       &lt;ns0:strActivity&gt;{{strActivity}}&lt;/ns0:strActivity&gt;     &lt;/ns0:PostEvent&gt;   &lt;/SOAP-ENV:Body&gt; &lt;/SOAP-ENV:Envelope&gt; ``` |
|SOAPレスポンスエラー識別子|  &lt;ul&gt;&lt;li&gt;`SOAP-ENV:Fault`のカスタム値を構成&lt;/li&gt;&lt;/ul&gt; |

### 例のリクエスト

```xml
&lt;SOAP-ENV:Envelope xmlns:SOAP-ENV=&#34;http://schemas.xmlsoap.org/soap/envelope/&#34;
	xmlns:ns0=&#34;urn:xtk:workflow&#34;&gt;
	&lt;SOAP-ENV:Header /&gt;
	&lt;SOAP-ENV:Body&gt;
		&lt;ns0:PostEvent&gt;
			&lt;ns0:sessiontoken&gt;EXAMPLE_TEALIUM_POPULATED_TOKEN&lt;/ns0:sessiontoken&gt;
            &lt;ns0:strWorkflowId&gt;workflow1000&lt;/ns0:strWorkflowId&gt;
            &lt;ns0:strActivity&gt;importTask2000&lt;/ns0:strActivity&gt;
		&lt;/ns0:PostEvent&gt;
	&lt;/SOAP-ENV:Body&gt;
&lt;/SOAP-ENV:Envelope&gt;

```

### 例のレスポンス

```xml
&lt;?xml version=&#39;1.0&#39;?&gt;
	&lt;SOAP-ENV:Envelope xmlns:xsd=&#39;http://www.w3.org/2001/XMLSchema&#39;
		xmlns:xsi=&#39;http://www.w3.org/2001/XMLSchema-instance&#39; xmlns:ns=&#39;urn:xtk:workflow&#39;
		xmlns:SOAP-ENV=&#39;http://schemas.xmlsoap.org/soap/envelope/&#39;&gt;
		&lt;SOAP-ENV:Body&gt;
			&lt;PostEventResponse xmlns=&#39;urn:xtk:workflow&#39;
				SOAP-ENV:encodingStyle=&#39;http://schemas.xmlsoap.org/soap/encoding/&#39;&gt;&lt;/PostEventResponse&gt;
		&lt;/SOAP-ENV:Body&gt;
	&lt;/SOAP-ENV:Envelope&gt;

```
### 例外エラーレスポンス

SOAPコールレスポンスのHTTPステータスが200-299である場合、または「SOAPレスポンスエラー識別子」のいずれかを含む場合、アクションは失敗と見なされます。この例では、レスポンスに識別子「SOAP-ENV:Server」が含まれているため、アクションは失敗とマークされます。

```xml
&lt;?xml version=&#39;1.0&#39;?&gt;
	&lt;SOAP-ENV:Envelope xmlns:xsd=&#39;http://www.w3.org/2001/XMLSchema&#39;
		xmlns:xsi=&#39;http://www.w3.org/2001/XMLSchema-instance&#39; xmlns:SOAP-ENV=&#39;http://schemas.xmlsoap.org/soap/envelope/&#39;&gt;
		&lt;SOAP-ENV:Body&gt;
			&lt;SOAP-ENV:Fault&gt;
				&lt;faultcode&gt;SOAP-ENV:Server&lt;/faultcode&gt;
				&lt;faultstring xsi:type=&#39;xsd:string&#39;&gt;SOP-330011 Error while executing
					the method &#39;PostEvent&#39; of service &#39;xtk:workflow&#39;.&lt;/faultstring&gt;
			&lt;/SOAP-ENV:Fault&gt;
		&lt;/SOAP-ENV:Body&gt;
	&lt;/SOAP-ENV:Envelope&gt;

```

**フォルトコードとフォルト文字列レスポンスのエラーを投げる** パラメータを有効にすると、コネクタはボディレスポンスに含まれるフォルトコードまたはフォルト文字列をエラーとして返します：

```xml
&lt;/soapenv:Body&gt;
&lt;/soapenv:Envelope&gt;; error_identifier = SOP-330011; Action Result Response: Http Response 200 &lt;?xml version=&#39;1.0&#39;?&gt;&lt;SOAP-ENV:Envelope xmlns:xsd=&#39;&lt;http://www.w3.org/2001/XMLSchema&gt;&#39; xmlns:xsi=&#39;&lt;http://www.w3.org/2001/XMLSchema-instance&gt;&#39; xmlns:SOAP-ENV=&#39;&lt;http://schemas.xmlsoap.org/soap/envelope/&gt;&#39;&gt;&lt;SOAP-ENV:Body&gt;&lt;SOAP-ENV:Fault&gt;&lt;faultcode&gt;SOAP-ENV:Server&lt;/faultcode&gt;&lt;faultstring xsi:type=&#39;xsd:string&#39;&gt;SOP-330011 Error while executing the method &#39;addAbandonedCart&#39; of service &#39;va:abandoned_cart_event&#39;.&lt;/faultstring&gt;&lt;detail xsi:type=&#39;xsd:string&#39;&gt;ODB-240000 ODBC error: [Microsoft][SQL Server Native Client 11.0][SQL Server]Transaction (Process ID 108) was deadlocked on lock | communication buffer resources with another process and has been chosen as the deadlock victim. Rerun the transaction. SQLState: 40001
XSV-350023 Unable to save document of type &#39;abandoned_cart_events (va:abandoned_cart_event)&#39;.
SOP-330011 Error while executing the method &#39;Write&#39; of service &#39;xtk:persist|xtk:session&#39;.&lt;/detail&gt;
&lt;/SOAP-ENV:Fault&gt;
&lt;/SOAP-ENV:Body&gt;
&lt;/SOAP-ENV:Envelope&gt;
```

```xml
 &lt;soapenv:Body&gt;
&lt;urn:addAbandonedCart&gt;
         &lt;urn:sessiontoken&gt; {{ sessionToken }} &lt;/urn:sessiontoken&gt;
         &lt;urn:days_to_departure&gt; {{ days_to_departure }} &lt;/urn:days_to_departure&gt;
         &lt;urn:recipient_id&gt; {{ recipient_id }} &lt;/urn:recipient_id&gt;
         &lt;urn:abandoned_type&gt; {{ abandoned_type }} &lt;/urn:abandoned_type&gt;
         &lt;urn:msg_id&gt; {{ msg_id }} &lt;/urn:msg_id&gt;
         &lt;urn:origin_code&gt; {{ origin_code }} &lt;/urn:origin_code&gt;
         &lt;urn:triggerType&gt; {{ triggerType }} &lt;/urn:triggerType&gt;
         &lt;urn:velocity_id&gt; {{ velocity_id }} &lt;/urn:velocity_id&gt;
         &lt;urn:timeGMT&gt; {{ timeGMT }} &lt;/urn:timeGMT&gt;
         &lt;urn:experianId&gt; {{ experianId }} &lt;/urn:experianId&gt;
         &lt;urn:main_dest_code&gt; {{ main_dest_code }} &lt;/urn:main_dest_code&gt;
&lt;/urn:addAbandonedCart&gt;
&lt;/soapenv:Body&gt;
&lt;/soapenv:Envelope&gt;; error_identifier = SOP-330011; Action Time: 5088 ms
```

## ベンダー文書

* [Adobe Campaign Classic v7: Webサービスコール](https://experienceleague.adobe.com/docs/campaign-classic/using/configuring-campaign-classic/api/web-service-calls.html?lang=en)