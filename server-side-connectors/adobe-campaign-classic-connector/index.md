---
title: Adobe Campaign Classic Connector Setup Guide
description: This article describes how to set up the Adobe Campaign Classic connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/adobe-campaign-classic-connector/
---
## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Custom SOAP Request (Batched) | ✓ | ✓ |
|Send Custom SOAP Request| ✓| ✓ |

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **Server Host**
  * Either Server Host or Server Address is required.
  * Example: For the domain, &#34;serverURL&#34; copy and paste `serverURL` from the following example URL: `&lt;https://serverURL/nl/jsp/soaprouter.jsp&gt;`
  * For authentication, provide username and password as part of SOAP Request Body Prefix.
  * For additional information, see [Access Management](https://experienceleague.adobe.com/docs/campaign-classic/using/configuring-campaign-classic/api/web-service-calls.html?lang=en#connectivity) in the Adobe Campaign Classic access management help documentation.

* **Server Address**
  * Specify full URL to Adobe Campaign server.
  * Either Server Host or Server Address is required.
  * If the address is provided, host is ignored.

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Send Custom SOAP Request (Batched)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 200
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| SOAP Action | SOAP Action, for example: `xtk:session#Logon`.&lt;br&gt;This value will be assigned to SOAPAction HTTP header. |
|SOAP Request Template Variables|  &lt;ul&gt;&lt;li&gt;Provide template variables as data input for SOAP Request Body Prefix, SOAP Request Body Data and SOAP Request Body Suffix. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation.&lt;/li&gt;&lt;li&gt;For example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|SOAP Request Body Prefix|  &lt;ul&gt;&lt;li&gt;Provide a template of the opening portion of SOAP Request.&lt;/li&gt;&lt;li&gt;For example: ``` &lt;soapenv:Envelope xmlns:soapenv=&#34;http://schemas.xmlsoap.org/soap/envelope/&#34; xmlns:urn=&#34;urn:xtk:session&#34;&gt;&lt;soapenv:Header/&gt;&lt;soapenv:Body&gt;&lt;urn:Logon&gt;&lt;urn:strLogin&gt;USERNAME&lt;/urn:strLogin&gt;&lt;urn:strPassword&gt;PASSWORD&lt;/urn:strPassword&gt;&lt;urn:elemParameters&gt; ``` &lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;Use your Adobe username and password in place of `USERNAME` and `PASSWORD`.&lt;/li&gt;&lt;li&gt;Use template variables in the **SOAP Request Body Prefix**.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;/ul&gt; |
|SOAP Request Body Data|  &lt;ul&gt;&lt;li&gt;Provide a template for the SOAP Request batch item to be sent.&lt;/li&gt;&lt;li&gt;Use template variables in the SOAP Request Body Data.&lt;/li&gt;&lt;/ul&gt; |
|SOAP Request Body Joiner|  &lt;ul&gt;&lt;li&gt;A character or string to use between body items when batching.&lt;/li&gt;&lt;li&gt;If not specified, empty string will be used.&lt;/li&gt;&lt;/ul&gt; |
|SOAP Request Body Suffix|  &lt;ul&gt;&lt;li&gt;Provide a template for the closing portion of SOAP Request.&lt;/li&gt;&lt;li&gt;For example: ``` &lt;/urn:elemParameters&gt;&lt;/urn:Logon&gt;&lt;/soapenv:Body&gt;&lt;/soapenv:Envelope&gt; ``` &lt;/li&gt;&lt;li&gt;Use template variables in the SOAP Request Body Suffix.&lt;/li&gt;&lt;/ul&gt; |
|SOAP Response Error Identifier|  &lt;ul&gt;&lt;li&gt;If the response contains any of the error strings (OR condition) specified below, it is marked as a failure.&lt;/li&gt;&lt;li&gt;By default, an HTTP response status outside the 200-299 range is also marked as a failure.&lt;/li&gt;&lt;/ul&gt; |
| Throw errors for any Fault Codes and Fault String Responses | Select this checkbox to throw errors for any fault codes and fault string responses.|

### Action - Send Custom SOAP Request

#### Parameters

|**Parameter**| **Description**|
|---| ---|
| SOAP Action Header Value | This parameter is required&lt;br&gt;For example: `xtk:workflow#PostEvent`. |
| SOAP Request Template Variables|  &lt;ul&gt;&lt;li&gt;Provide template variables as data input for SOAP Request Body Prefix, SOAP Request Body Data and SOAP Request Body Suffix. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation.&lt;/li&gt;&lt;li&gt;For example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
| SOAP Request Body Template | This parameter is required&lt;br&gt;Provide SOAP Request Body Template to be sent. For more information, see .&lt;br&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.&lt;br&gt;Note: a session token is required for Adobe Campaign API calls, ensure to include it in the template where appropriate. Use the reserved template keyword `{{sessionToken}}`, which is predefined and populated automatically for you, to have this token included in the template. |
|SOAP Response Error Identifier|  &lt;ul&gt;&lt;li&gt;If the response contains any of the error strings (OR condition) specified below, it is marked as a failure.&lt;/li&gt;&lt;li&gt;By default, an HTTP response status outside the 200-299 range is also marked as a failure.&lt;/li&gt;&lt;/ul&gt; |
