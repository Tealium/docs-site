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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

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
| `email`| &lt;ul&gt;&lt;li&gt;(Required) Target email address.&lt;/li&gt;&lt;/ul&gt;|
| `eid`| &lt;ul&gt;&lt;li&gt;(Required) Event ID tied to target mailing template.&lt;/li&gt;&lt;/ul&gt;|
| `aid`| &lt;ul&gt;&lt;li&gt;Affiliate ID for target mailing.&lt;/li&gt;&lt;/ul&gt;|
| `from_address`| &lt;ul&gt;&lt;li&gt;Sender/From email address.&lt;/li&gt;&lt;/ul&gt;|
| `from_text`| &lt;ul&gt;&lt;li&gt;Text part of from header.&lt;/li&gt;&lt;/ul&gt;|
| `replyto`| &lt;ul&gt;&lt;li&gt;Reply-To header.&lt;/li&gt;&lt;/ul&gt;|
| `b `| &lt;ul&gt;&lt;li&gt;Engage Global Suppression Tool (GST).&lt;/li&gt;&lt;/ul&gt; |
| `certify`| &lt;ul&gt;&lt;li&gt;Send with a third party certification stamp.&lt;/li&gt;&lt;/ul&gt; |
| `mtype`| &lt;ul&gt;&lt;li&gt;Certified message type.&lt;/li&gt;&lt;/ul&gt; |
| `test `| &lt;ul&gt;&lt;li&gt;Test flag to trigger non-deployed event.&lt;/li&gt;&lt;/ul&gt; |
| `part`| &lt;ul&gt;&lt;li&gt;Mailing part to use for the test.&lt;/li&gt;&lt;/ul&gt; |
| Preferred Content Type                                                              | &lt;ul&gt;&lt;li&gt;(Optional) `HTML=Optional` - A specialized instance of a PARAM value that indicates the preferred content type:  &lt;ul&gt;&lt;li&gt;– Text only&lt;/li&gt;&lt;li&gt;`1` – HTML/Text multipart&lt;/li&gt;&lt;li&gt;`2` – Rich Text/Text multipart&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
| Email CB Data Fields to Set                                                         | &lt;ul&gt;&lt;li&gt;(Optional) Add one line item per field (line items provided are pipe delimited).&lt;/li&gt;&lt;li&gt;`cb=Optional` - A list of client-defined suppression bit indexes for the Global Suppression Tool (GST) to change, ranging from 1 to 25.&lt;/li&gt;&lt;li&gt;If the `cb` parameter is passed, the `b` parameter must also be specified with a value of 0 or 1.&lt;/li&gt;&lt;li&gt;Indicates whether the standard stoplist should be included when evaluating suppression for an address.&lt;/li&gt;&lt;/ul&gt; |
| Email REQ Data Fields to Set                                                        | &lt;ul&gt;&lt;li&gt;(Optional) Add one line item per field (line items provided are pipe delimited).&lt;/li&gt;&lt;li&gt;`req=Optional` - Specify required personalization fields that must be non-empty for success.&lt;/li&gt;&lt;li&gt;Looping dynamic content fields may only be required explicitly, replacing `*` with appropriate values (`ITEMS.*`).&lt;/li&gt;&lt;li&gt;Alternatively, setting `req` to a value of `1` specifies that all personalization fields present must be non-empty.&lt;/li&gt;&lt;/ul&gt; |
| Set Dynamic Content Tags/Parameters                                                 | &lt;ul&gt;&lt;li&gt;(Optional) Add one line item per field (line items provided are pipe delimited).&lt;/li&gt;&lt;li&gt;`PARAM=` - The value of any upper case parameter is made available for substitution into the email in place of a tag consisting of two percentage signs, the parameter name, and two percentage signs.  &lt;ul&gt;&lt;li&gt;For example: For PARAM, the tag would be &#34;`%%PARAM%%`.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Uppercase parameters start with `A` - `Z` or `_`, followed by any number of characters `A`- `Z`, - `9`, or underscore ( `_`).&lt;/li&gt;&lt;li&gt;Values are URL-decoded before substitution.&lt;/li&gt;&lt;li&gt;Tags referring to parameters not supplied in the API call are replaced with an empty string.&lt;/li&gt;&lt;li&gt;There is no size limit to values (entire order tables can be supplied).&lt;/li&gt;&lt;li&gt;There is no versioning of the parameters for the three different types of email creative (text, html, rich text/aol).&lt;/li&gt;&lt;li&gt;If variable content needs to be formatted differently depending on creative, the API call should supply the different versions with different parameter names.&lt;/li&gt;&lt;li&gt;Mailing should be set up to use version-appropriate tags.&lt;/li&gt;&lt;li&gt;The parameters `T`, `TRACK`, and `EMAIL` are reserved for internal use.&lt;/li&gt;&lt;li&gt;The API is error-tolerant for PARAM names.&lt;/li&gt;&lt;li&gt;If a PARAM is supplied that does not exist in the template, it will be silently ignored.&lt;/li&gt;&lt;li&gt;Ensure that through proofread all names so that they are not lost due to a spelling error.&lt;/li&gt;&lt;/ul&gt; |
| Enable Subscriber Lookup through the `getuser1` API Call | &lt;ul&gt;&lt;li&gt;Enabling this option triggers an extra API call where the target subscriber is looked-up up using the `getuser1` API call.&lt;/li&gt;&lt;li&gt;The result is matched against the Subscriber List ID configured in the next section, and if satisfied an email is sent through the `ebmtrigger1` API call. &lt;/li&gt;&lt;/ul&gt; The AID returned from this API call will be used regardless and will override the configuration in the &#34;Email General Data Fields to Set&#34; section unless the &#34;Exclude using AID returned from Subscriber Lookup&#34; is checked. |
| Exclude using AID returned from &#34;Subscriber Lookup&#34; | &lt;ul&gt;&lt;li&gt;This option is only used when &#34;Subscriber Lookup&#34; is also enabled.&lt;/li&gt;&lt;li&gt;If checked the AID returned for the &#34;Subscriber Lookup&#34; API call will not be included in the subsequent `ebmtrigger1` API call, otherwise the AID from &#34;Subscriber Lookup&#34; will be included and override the configurations in the &#34;Email General Data Fields to Set&#34; section.&lt;/li&gt;&lt;/ul&gt; |
| Target Subscriber List ID to match against Subscriber Lookup (`getuser1` API Call) | &lt;ul&gt;&lt;li&gt;This option is only used when &#34;Subscriber Lookup&#34; is also enabled.&lt;/li&gt;&lt;li&gt;email&lt;/li&gt;&lt;li&gt;See the &#34;Email General Data Fields to Set&#34; row in this table.  &lt;ul&gt;&lt;li&gt;(Required) The email address provided in &#34;Email General Data Fields to Set&#34; section will be used to look up the subscriber.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Target Subscriber List ID  &lt;ul&gt;&lt;li&gt;(Required) The subscriber list ID that is used to match against `getuser1` API call response.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
