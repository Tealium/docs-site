---
title: Adobe Campaign Connector Setup Guide for AudienceStream
description: This article describes how to set up the Adobe Campaign connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/adobe-campaign-connector/
---## Requirements

* Adobe Campaign Account
* SOAP API Credentials  
Contact your Adobe representative for your credentials.
* Whitelist the [IP addresses]() of the AudienceStream servers  
If the IP addresses are not whitelisted by Adobe, the trace feature displays the following error: `Action Failure: Error: received non-successful http response status = 403`

## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Custom SOAP Request| ✓| ✗|

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

This Connector uses Adobe Campaign&#39;s SOAP log on method to connect to the SOAP API. Refer to Adobe Campaign&#39;s Connectivity documentation for more information.

To configure your vendor, follow these steps:

1. In the Configure tab, provide a title for the Connector instance.
1. Enter the SOAP API username and password that you received from Adobe for your account.
1. Enter the SOAP API endpoint that you received from Adobe for your account. Only include the domain.  
Example: If the server path is `&lt;http://example.com/nl/jsp/soaprouter.jsp&gt;`, only enter &#34;example.com&#34; in this field.
1. Provide additional notes about your implementation.
1. Click **Establish Connection** to verify the API connectivity.

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Custom SOAP Request

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|SOAP Action Header Value|  &lt;ul&gt;&lt;li&gt;This parameter is required&lt;/li&gt;&lt;li&gt;Example: `xtk:workflow#PostEvent`.&lt;/li&gt;&lt;/ul&gt; |
|SOAP Request Body Template|  &lt;ul&gt;&lt;li&gt;(Required) Provide SOAP Request Body Template to be sent. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;li&gt;A session token is required for Adobe Campaign API calls, ensure to include it in the template where appropriate.  &lt;ul&gt;&lt;li&gt;Use the reserved (predefined and populated automatically for you) template keyword `{{sessionToken}}` to have this token included in the template.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|SOAP Response Error Identifier|  &lt;ul&gt;&lt;li&gt;If the response contains any of the error strings (OR condition) specified below, it is marked as a failure.&lt;/li&gt;&lt;li&gt;By default, an HTTP response status outside 200-299 range is also marked as a failure.&lt;/li&gt;&lt;/ul&gt; |
|Throw errors for any Fault Codes and Fault String Responses|  &lt;ul&gt;&lt;li&gt;Any fault codes or fault strings included in the body response will be captured and returned as errors.&lt;/li&gt;&lt;/ul&gt; |

Refer to [Adobe Campaign v6.1 Configuration Guide](https://docs.campaign.adobe.com/doc/AC6.1/en/PDF/configuration-v6.1-en.pdf) for additional help.

### Additional notes

* A SOAP Request Body template is required.
  * To inject a template into the supported fields, simply wrap its name in double curly braces. For example, `{{SomeTemplateName}}`.
  * For more information about common syntax and extensions, see .

* A session token is required for Adobe Campaign API calls
  * Ensure that you include it in the template where appropriate.
  * Use the reserved template keyword `{{sessionToken}}` to have this token included in the template.
  * A reserved keyword is predefined and populated automatically for you.

* Template variables are optional.
  * To name nested template variables, use the dot notation, for example `items.name`.
  * Nested template variables are typically built from data layer list Attributes.
  * For more information, see .


## Usage example

Here&#39;s a sample configuration for sending a PostEvent SOAP request.

|**Parameter - Option**| **Description**|
|---| ---|
|SOAPAction Header Value|  &lt;ul&gt;&lt;li&gt;Configure Custom Value of `xtk:workflow#PostEvent`&lt;/li&gt;&lt;/ul&gt; |
|SOAP Request Body Template Variables|  &lt;ul&gt;&lt;li&gt;**Map** Custom Value of `workflow1000 `**To** `strWorkflowId`&lt;/li&gt;&lt;li&gt;**Map** Custom Value of `importTask2000` **To** `strActivity`&lt;/li&gt;&lt;/ul&gt; |
|SOAP Request Body Template|  ``` &lt;SOAP-ENV:Envelope xmlns:SOAP-ENV=&#34;http://schemas.xmlsoap.org/soap/envelope/&#34;  xmlns:ns0=&#34;urn:xtk:workflow&#34;&gt;   &lt;SOAP-ENV:Header /&gt;   &lt;SOAP-ENV:Body&gt;     &lt;ns0:PostEvent&gt;       &lt;ns0:sessiontoken&gt;{{sessionToken}}&lt;/ns0:sessiontoken&gt;       &lt;ns0:strWorkflowId&gt;{{strWorkflowId}}&lt;/ns0:strWorkflowId&gt;       &lt;ns0:strActivity&gt;{{strActivity}}&lt;/ns0:strActivity&gt;     &lt;/ns0:PostEvent&gt;   &lt;/SOAP-ENV:Body&gt; &lt;/SOAP-ENV:Envelope&gt; ``` |
|SOAP Response Error Identifier|  &lt;ul&gt;&lt;li&gt;Configure Custom Value of `SOAP-ENV:Fault`&lt;/li&gt;&lt;/ul&gt; |

### Example request

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

### Example response

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

### Example error response

If the SOAP Call Response&#39;s HTTP status is 200-299 or otherwise includes any of the &#34;SOAP Response Error Identifier&#34; values, the Action is deemed as a failure. In this example, the Action will be marked as failure because the response contains the identifier &#34;SOAP-ENV:Server&#34;.

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

If you enable the **Throw errors for any Fault Codes and Fault String Responses** parameter, the connector will return fault codes or fault strings included in the body response as errors:

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

## Vendor documentation

* [Adobe Campaign Classic v7: Web service calls](https://experienceleague.adobe.com/docs/campaign-classic/using/configuring-campaign-classic/api/web-service-calls.html?lang=en)