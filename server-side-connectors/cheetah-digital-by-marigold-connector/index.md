---
title: Cheetah Digital by Marigold Connector Setup Guide
description: This article describes how to set up the Cheetah Digital by Marigold connector.
url: https://docs.tealium.com/server-side-connectors/cheetah-digital-by-marigold-connector/
---
## Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
|:------|:-------------------|:----------------|
| Send Email to Subscriber (Advanced API Call - ebmtrigger1) | ✓                  | ✗               |

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Username**
  * The username for the Cheetah Digital by Marigold API. 
  * For more information, see [Cheetah Digital by Marigold API](https://help.cheetahces.com/hc/en-us/articles/360007860897-API-Category-Authentication-Service).

* **API Password**
  * The password for the Cheetah Digital by Marigold API.
  * For more information, see [Cheetah Digital by Marigold API](https://help.cheetahces.com/hc/en-us/articles/360007860897-API-Category-Authentication-Service).

* **API URL**
  * Supports private IP networks, for example `https://trig.{client-domain}.com/`.
  * Define your client domain if needed.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Email to Subscriber (Advanced API Call - ebmtrigger1)

#### Parameters

| **Parameter** | **Description** |
|:--------------|:----------------|
| `email`| <ul><li>(Required) Target email address.</li></ul>|
| `eid`| <ul><li>(Required) Event ID tied to target mailing template.</li></ul>|
| `aid`| <ul><li>Affiliate ID for target mailing.</li></ul>|
| `from_address`| <ul><li>Sender/From email address.</li></ul>|
| `from_text`| <ul><li>Text part of from header.</li></ul>|
| `replyto`| <ul><li>Reply-To header.</li></ul>|
| `b `| <ul><li>Engage Global Suppression Tool (GST).</li></ul> |
| `certify`| <ul><li>Send with a third party certification stamp.</li></ul> |
| `mtype`| <ul><li>Certified message type.</li></ul> |
| `test `| <ul><li>Test flag to trigger non-deployed event.</li></ul> |
| `part`| <ul><li>Mailing part to use for the test.</li></ul> |
| Preferred Content Type                                                              | <ul><li>(Optional) `HTML=Optional` - A specialized instance of a PARAM value that indicates the preferred content type:  <ul><li>– Text only</li><li>`1` – HTML/Text multipart</li><li>`2` – Rich Text/Text multipart</li></ul> </li></ul> |
| Email CB Data Fields to Set                                                         | <ul><li>(Optional) Add one line item per field (line items provided are pipe delimited).</li><li>`cb=Optional` - A list of client-defined suppression bit indexes for the Global Suppression Tool (GST) to change, ranging from 1 to 25.</li><li>If the `cb` parameter is passed, the `b` parameter must also be specified with a value of 0 or 1.</li><li>Indicates whether the standard stoplist should be included when evaluating suppression for an address.</li></ul> |
| Email REQ Data Fields to Set                                                        | <ul><li>(Optional) Add one line item per field (line items provided are pipe delimited).</li><li>`req=Optional` - Specify required personalization fields that must be non-empty for success.</li><li>Looping dynamic content fields may only be required explicitly, replacing `*` with appropriate values (`ITEMS.*`).</li><li>Alternatively, setting `req` to a value of `1` specifies that all personalization fields present must be non-empty.</li></ul> |
| Set Dynamic Content Tags/Parameters                                                 | <ul><li>(Optional) Add one line item per field (line items provided are pipe delimited).</li><li>`PARAM=` - The value of any upper case parameter is made available for substitution into the email in place of a tag consisting of two percentage signs, the parameter name, and two percentage signs.  <ul><li>For example: For PARAM, the tag would be "`%%PARAM%%`.</li></ul> </li><li>Uppercase parameters start with `A` - `Z` or `_`, followed by any number of characters `A`- `Z`, - `9`, or underscore ( `_`).</li><li>Values are URL-decoded before substitution.</li><li>Tags referring to parameters not supplied in the API call are replaced with an empty string.</li><li>There is no size limit to values (entire order tables can be supplied).</li><li>There is no versioning of the parameters for the three different types of email creative (text, html, rich text/aol).</li><li>If variable content needs to be formatted differently depending on creative, the API call should supply the different versions with different parameter names.</li><li>Mailing should be set up to use version-appropriate tags.</li><li>The parameters `T`, `TRACK`, and `EMAIL` are reserved for internal use.</li><li>The API is error-tolerant for PARAM names.</li><li>If a PARAM is supplied that does not exist in the template, it will be silently ignored.</li><li>Ensure that through proofread all names so that they are not lost due to a spelling error.</li></ul> |
| Enable Subscriber Lookup through the `getuser1` API Call | <ul><li>Enabling this option triggers an extra API call where the target subscriber is looked-up up using the `getuser1` API call.</li><li>The result is matched against the Subscriber List ID configured in the next section, and if satisfied an email is sent through the `ebmtrigger1` API call. </li></ul> 
<blockquote>
The AID returned from this API call will be used regardless and will override the configuration in the "Email General Data Fields to Set" section unless the "Exclude using AID returned from Subscriber Lookup" is checked.
</blockquote>
 |
| Exclude using AID returned from "Subscriber Lookup" | <ul><li>This option is only used when "Subscriber Lookup" is also enabled.</li><li>If checked the AID returned for the "Subscriber Lookup" API call will not be included in the subsequent `ebmtrigger1` API call, otherwise the AID from "Subscriber Lookup" will be included and override the configurations in the "Email General Data Fields to Set" section.</li></ul> |
| Target Subscriber List ID to match against Subscriber Lookup (`getuser1` API Call) | <ul><li>This option is only used when "Subscriber Lookup" is also enabled.</li><li>email</li><li>See the "Email General Data Fields to Set" row in this table.  <ul><li>(Required) The email address provided in "Email General Data Fields to Set" section will be used to look up the subscriber.</li></ul> </li><li>Target Subscriber List ID  <ul><li>(Required) The subscriber list ID that is used to match against `getuser1` API call response.</li></ul> </li></ul> |
