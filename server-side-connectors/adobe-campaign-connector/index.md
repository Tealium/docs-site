---
title: Adobe Campaign Connector Setup Guide for AudienceStream
description: This article describes how to set up the Adobe Campaign connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/adobe-campaign-connector/
---## Requirements

* Adobe Campaign Account
* SOAP API Credentials  
Contact your Adobe representative for your credentials.
* Whitelist the [IP addresses](https://docs.tealium.com/ip-allow-list/) of the AudienceStream servers  

<blockquote>
If the IP addresses are not whitelisted by Adobe, the trace feature displays the following error: `Action Failure: Error: received non-successful http response status = 403`
</blockquote>


## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Custom SOAP Request| ✓| ✗|

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.


<blockquote>
This Connector uses Adobe Campaign's SOAP log on method to connect to the SOAP API. Refer to Adobe Campaign's Connectivity documentation for more information.
</blockquote>


To configure your vendor, follow these steps:

1. In the Configure tab, provide a title for the Connector instance.
1. Enter the SOAP API username and password that you received from Adobe for your account.
1. Enter the SOAP API endpoint that you received from Adobe for your account. Only include the domain.  
Example: If the server path is `<http://example.com/nl/jsp/soaprouter.jsp>`, only enter "example.com" in this field.
1. Provide additional notes about your implementation.
1. Click **Establish Connection** to verify the API connectivity.

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Custom SOAP Request

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|SOAP Action Header Value|  <ul><li>This parameter is required</li><li>Example: `xtk:workflow#PostEvent`.</li></ul> |
|SOAP Request Body Template|  <ul><li>(Required) Provide SOAP Request Body Template to be sent. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.</li><li>A session token is required for Adobe Campaign API calls, ensure to include it in the template where appropriate.  <ul><li>Use the reserved (predefined and populated automatically for you) template keyword `{{sessionToken}}` to have this token included in the template.</li></ul> </li></ul> |
|SOAP Response Error Identifier|  <ul><li>If the response contains any of the error strings (OR condition) specified below, it is marked as a failure.</li><li>By default, an HTTP response status outside 200-299 range is also marked as a failure.</li></ul> |
|Throw errors for any Fault Codes and Fault String Responses|  <ul><li>Any fault codes or fault strings included in the body response will be captured and returned as errors.</li></ul> |


<blockquote>
Refer to [Adobe Campaign v6.1 Configuration Guide](https://docs.campaign.adobe.com/doc/AC6.1/en/PDF/configuration-v6.1-en.pdf) for additional help.
</blockquote>


### Additional notes

* A SOAP Request Body template is required.
  * To inject a template into the supported fields, simply wrap its name in double curly braces. For example, `{{SomeTemplateName}}`.
  * For more information about common syntax and extensions, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).

* A session token is required for Adobe Campaign API calls
  * Ensure that you include it in the template where appropriate.
  * Use the reserved template keyword `{{sessionToken}}` to have this token included in the template.
  * A reserved keyword is predefined and populated automatically for you.

* Template variables are optional.
  * To name nested template variables, use the dot notation, for example `items.name`.
  * Nested template variables are typically built from data layer list Attributes.
  * For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).


## Usage example

Here's a sample configuration for sending a PostEvent SOAP request.

|**Parameter - Option**| **Description**|
|---| ---|
|SOAPAction Header Value|  <ul><li>Configure Custom Value of `xtk:workflow#PostEvent`</li></ul> |
|SOAP Request Body Template Variables|  <ul><li>**Map** Custom Value of `workflow1000 `**To** `strWorkflowId`</li><li>**Map** Custom Value of `importTask2000` **To** `strActivity`</li></ul> |
|SOAP Request Body Template|  ``` <SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  xmlns:ns0="urn:xtk:workflow">   <SOAP-ENV:Header />   <SOAP-ENV:Body>     <ns0:PostEvent>       <ns0:sessiontoken>{{sessionToken}}</ns0:sessiontoken>       <ns0:strWorkflowId>{{strWorkflowId}}</ns0:strWorkflowId>       <ns0:strActivity>{{strActivity}}</ns0:strActivity>     </ns0:PostEvent>   </SOAP-ENV:Body> </SOAP-ENV:Envelope> ``` |
|SOAP Response Error Identifier|  <ul><li>Configure Custom Value of `SOAP-ENV:Fault`</li></ul> |

### Example request

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

### Example response

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

### Example error response

If the SOAP Call Response's HTTP status is 200-299 or otherwise includes any of the "SOAP Response Error Identifier" values, the Action is deemed as a failure. In this example, the Action will be marked as failure because the response contains the identifier "SOAP-ENV:Server".

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

If you enable the **Throw errors for any Fault Codes and Fault String Responses** parameter, the connector will return fault codes or fault strings included in the body response as errors:

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

## Vendor documentation

* [Adobe Campaign Classic v7: Web service calls](https://experienceleague.adobe.com/docs/campaign-classic/using/configuring-campaign-classic/api/web-service-calls.html?lang=en)