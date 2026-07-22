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

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **Server Host**
  * Either Server Host or Server Address is required.
  * Example: For the domain, "serverURL" copy and paste `serverURL` from the following example URL: `<https://serverURL/nl/jsp/soaprouter.jsp>`
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

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 200
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| SOAP Action | SOAP Action, for example: `xtk:session#Logon`.<br>This value will be assigned to SOAPAction HTTP header. |
|SOAP Request Template Variables|  <ul><li>Provide template variables as data input for SOAP Request Body Prefix, SOAP Request Body Data and SOAP Request Body Suffix. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation.</li><li>For example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
|SOAP Request Body Prefix|  <ul><li>Provide a template of the opening portion of SOAP Request.</li><li>For example: ``` <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:urn="urn:xtk:session"><soapenv:Header/><soapenv:Body><urn:Logon><urn:strLogin>USERNAME</urn:strLogin><urn:strPassword>PASSWORD</urn:strPassword><urn:elemParameters> ``` </li></ul> <ul><li>Use your Adobe username and password in place of `USERNAME` and `PASSWORD`.</li><li>Use template variables in the **SOAP Request Body Prefix**.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li></ul> |
|SOAP Request Body Data|  <ul><li>Provide a template for the SOAP Request batch item to be sent.</li><li>Use template variables in the SOAP Request Body Data.</li></ul> |
|SOAP Request Body Joiner|  <ul><li>A character or string to use between body items when batching.</li><li>If not specified, empty string will be used.</li></ul> |
|SOAP Request Body Suffix|  <ul><li>Provide a template for the closing portion of SOAP Request.</li><li>For example: ``` </urn:elemParameters></urn:Logon></soapenv:Body></soapenv:Envelope> ``` </li><li>Use template variables in the SOAP Request Body Suffix.</li></ul> |
|SOAP Response Error Identifier|  <ul><li>If the response contains any of the error strings (OR condition) specified below, it is marked as a failure.</li><li>By default, an HTTP response status outside the 200-299 range is also marked as a failure.</li></ul> |
| Throw errors for any Fault Codes and Fault String Responses | Select this checkbox to throw errors for any fault codes and fault string responses.|

### Action - Send Custom SOAP Request

#### Parameters

|**Parameter**| **Description**|
|---| ---|
| SOAP Action Header Value | This parameter is required<br>For example: `xtk:workflow#PostEvent`. |
| SOAP Request Template Variables|  <ul><li>Provide template variables as data input for SOAP Request Body Prefix, SOAP Request Body Data and SOAP Request Body Suffix. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation.</li><li>For example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
| SOAP Request Body Template | This parameter is required<br>Provide SOAP Request Body Template to be sent. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).<br>Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.<br>Note: a session token is required for Adobe Campaign API calls, ensure to include it in the template where appropriate. Use the reserved template keyword `{{sessionToken}}`, which is predefined and populated automatically for you, to have this token included in the template. |
|SOAP Response Error Identifier|  <ul><li>If the response contains any of the error strings (OR condition) specified below, it is marked as a failure.</li><li>By default, an HTTP response status outside the 200-299 range is also marked as a failure.</li></ul> |
