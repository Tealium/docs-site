---
title: Salesforce Connector Setup Guide
description: This article describes how to set up the Salesforce Connector.
url: https://docs.tealium.com/server-side-connectors/salesforce-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings to establish a connection to Salesforce:

* **Account Type**: Select an account type to connect to: **Developer**, **Production**, or **Sandbox**.
    * Click **Establish Connection** to initiate the OAuth process and follow the prompts to completion.
    * For more information on sandboxes, see [Salesforce: Create a Sandbox for Account Engagement](https://help.salesforce.com/s/articleView?id=mktg.pardot_sf_connector_sandbox.htm&amp;type=5).

## Actions

| Action Name | AudienceStream | EventStream|
|---| ---| ---|
|Insert into Custom Object| ✓| ✗|
|Update Custom Object| ✓| ✗|
|Insert Lead| ✓| ✗|
|Update Lead| ✓| ✗|
|Upsert Lead| ✓| ✗|
|Convert Lead to Contact| ✓| ✗|
|Add Lead to Campaign| ✓| ✗|
|Insert Contact| ✓| ✗|
|Update Contact| ✓| ✗|
|Add Contact to Campaign| ✓| ✗|
| Send Entire Visitor to Custom Apex | ✓ | ✗ |
| Send Entire Event to Custom Apex | ✗ | ✓ |
| Upsert into Custom Object (non-batched) | ✓ | ✓ |
| Upsert into Custom Object (batched) | ✓ | ✓ |

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Insert into Custom Object

#### Parameters

|Parameter| Description|
|---| ---|
|Custom Object Name| Name of Salesforce custom object.|
| Insert Data Map | Select and map Tealium attributes to the Salesforce fields of your custom object. Each mapped field is sent as part of the record insert. |

### Update Custom Object

#### Parameters

|Parameter| Description|
|---| ---|
|Custom Object Name| Name of Salesforce custom object.|
|Custom Object ID | ID of Salesforce custom object.|
| Update Fields | Map Tealium attributes to the Salesforce fields to update in the record. |

### Insert Lead

#### Parameters

|Parameter| Description|
|---| ---|
|Insert Data to Set| Select and map Tealium attributes to Salesforce lead fields for record creation.|
| Append Data Map | &lt;ul&gt;&lt;li&gt;(Optional) Use this section to append multiple AudienceStream attributes to the same Salesforce text area field.&lt;/li&gt;&lt;li&gt;Map multiple values to the same Salesforce field key as needed.&lt;/li&gt;&lt;li&gt;For update and upsert actions, existing field content is preserved and new values are appended in formatted text.&lt;/li&gt;&lt;li&gt;Only Salesforce fields of type TextArea are supported.&lt;/li&gt;&lt;li&gt;Ensure the selected field has sufficient length to prevent API errors.&lt;/li&gt;&lt;li&gt;Appended values are represented in Salesforce according to their AudienceStream data type (for example, Boolean, String, JSON).&lt;/li&gt;&lt;li&gt;The appended text includes the optional entry label (if provided), current ISO UTC date, and the mapped key-value pairs on separate lines.&lt;/li&gt;&lt;/ul&gt; |
|Append Data Map - Entry Label|  &lt;ul&gt;&lt;li&gt;(Optional) If provided, this text is appended to the start of the appended columns values.&lt;/li&gt;&lt;li&gt;Leave empty if not used.&lt;/li&gt;&lt;li&gt;See &#34;Append Data Map&#34; section for the exact format.&lt;/li&gt;&lt;/ul&gt; |
|Select Target Assignment Rule|  &lt;ul&gt;&lt;li&gt;(Optional) A list that displays available assignment rules for your account that can be used to apply on your target lead.&lt;/li&gt;&lt;li&gt;Selecting the **Use Default Assignment Rule** enforces Salesforce to use the default rule for rule-based assignment.&lt;/li&gt;&lt;li&gt;Do not select any values or select **None** to avoid inclusion of assignment rule options in the API call.&lt;/li&gt;&lt;/ul&gt; |

### Update Lead

#### Parameters

|Parameter| Description|
|---| ---|
| Lead ID | (Required) Select the Salesforce field used to identify the lead to update.|
|Update Data to Set| Select and map Tealium attributes to Salesforce lead fields for record update.|
| Append Data Map | &lt;ul&gt;&lt;li&gt;(Optional) Use this section to append multiple AudienceStream attributes to the same Salesforce text area field.&lt;/li&gt;&lt;li&gt;Map multiple values to the same Salesforce field key as needed.&lt;/li&gt;&lt;li&gt;For update and upsert actions, existing field content is preserved and new values are appended in formatted text.&lt;/li&gt;&lt;li&gt;Only Salesforce fields of type TextArea are supported.&lt;/li&gt;&lt;li&gt;Ensure the selected field has sufficient length to prevent API errors.&lt;/li&gt;&lt;li&gt;Appended values are represented in Salesforce according to their AudienceStream data type (for example, Boolean, String, JSON).&lt;/li&gt;&lt;li&gt;The appended text includes the optional entry label (if provided), current ISO UTC date, and the mapped key-value pairs on separate lines.&lt;/li&gt;&lt;/ul&gt; |
|Append Data Map - Entry Label|  &lt;ul&gt;&lt;li&gt;(Optional) If provided, this text is appended to the start of the appended columns values.&lt;/li&gt;&lt;li&gt;Leave empty if not used.&lt;/li&gt;&lt;li&gt;See &#34;Append Data Map&#34; section for the exact format.&lt;/li&gt;&lt;/ul&gt; |
|Select Target Assignment Rule|  &lt;ul&gt;&lt;li&gt;(Optional) The list displays available assignment rules for your account that can be used to apply on your target lead.&lt;/li&gt;&lt;li&gt;Selecting **Use Default Assignment Rule** enforces Salesforce to use the default rule for rule-based assignment.&lt;/li&gt;&lt;li&gt;Do not select any values or select **None** to avoid inclusion of assignment rule options in the API call.&lt;/li&gt;&lt;/ul&gt; |

### Upsert Lead

#### Parameters

|Parameter| Description|
|---| ---|
| Update Lookup ID | &lt;ul&gt;&lt;li&gt;(Required) Select the Salesforce field used to identify an existing lead.&lt;/li&gt;&lt;li&gt;The value of this field determines whether the action updates an existing record or inserts a new one.&lt;/li&gt;&lt;/ul&gt; |
| Update Data to Set | &lt;ul&gt;&lt;li&gt;(Required) Map Tealium attributes to Salesforce lead fields to update when existing records are found.&lt;/li&gt;&lt;li&gt;To append multiple AudienceStream attributes to the same Salesforce field, use the Append Data Map section instead.&lt;/li&gt;&lt;li&gt;Values mapped here overwrite the existing field values in Salesforce.&lt;/li&gt;&lt;li&gt;Avoid configuring the same field in both sections. Use either Update Data to Set or Append Data Map, not both.&lt;/li&gt;&lt;/ul&gt;  |
| Insert Data to Set | &lt;ul&gt;&lt;li&gt;(Required) Map Tealium attributes to Salesforce lead fields for creating new records.&lt;/li&gt;&lt;li&gt;To append multiple AudienceStream attributes to the same Salesforce field, use the Append Data Map section instead.&lt;/li&gt;&lt;li&gt;Values mapped here populate the specified fields in the newly created lead record.&lt;/li&gt;&lt;li&gt;Avoid configuring the same field in both sections. Use either Insert Data to Set or Append Data Map, not both.&lt;/li&gt;&lt;/ul&gt;  |
| Append Data Map | &lt;ul&gt;&lt;li&gt;(Optional) Use this section to append multiple AudienceStream attributes to the same Salesforce text area field.&lt;/li&gt;&lt;li&gt;Map multiple values to the same Salesforce field key as needed.&lt;/li&gt;&lt;li&gt;For update and upsert actions, existing field content is preserved and new values are appended in formatted text.&lt;/li&gt;&lt;li&gt;Only Salesforce fields of type TextArea are supported.&lt;/li&gt;&lt;li&gt;Ensure the selected field has sufficient length to prevent API errors.&lt;/li&gt;&lt;li&gt;Appended values are represented in Salesforce according to their AudienceStream data type (for example, Boolean, String, JSON).&lt;/li&gt;&lt;li&gt;The appended text includes the optional entry label (if provided), current ISO UTC date, and the mapped key-value pairs on separate lines.&lt;/li&gt;&lt;/ul&gt; |
|Append Data Map - Entry Label|  &lt;ul&gt;&lt;li&gt;(Optional) If provided, this text is appended to the start of the appended columns values.&lt;/li&gt;&lt;li&gt;Leave empty if not used.&lt;/li&gt;&lt;li&gt;See &#34;Append Data Map&#34; section for the exact format.&lt;/li&gt;&lt;/ul&gt; |
|Select Target Assignment Rule|  &lt;ul&gt;&lt;li&gt;(Optional) The list displays available assignment rules for your account that can be used to apply on your target lead.&lt;/li&gt;&lt;li&gt;Selecting **Use Default Assignment Rule** enforces Salesforce to use the default rule for rule-based assignment.&lt;/li&gt;&lt;li&gt;Do not select any values or select **None** to avoid inclusion of assignment rule options in the API call.&lt;/li&gt;&lt;/ul&gt; |

### Convert Lead to Contact

#### Parameters

|Parameter| Description|
|---| ---|
| Lead ID | (Required) Select the Salesforce field used to identify the lead to update.|
|Send Email to the Owner| Send email to the owner.|

### Add Lead to Campaign

#### Parameters

|Parameter| Description|
|---| ---|
| Lead ID | (Required) Select the Salesforce field used to identify the lead to update.|
|Campaign| Select the target campaign for the lead.|

### Insert Contact

#### Parameters

|Parameter| Description|
|---| ---|
| Insert Contact |  &lt;ul&gt;&lt;li&gt;(Required) Map Tealium attributes to Salesforce contact identity fields.&lt;/li&gt;&lt;li&gt;These fields are used to define the contact record that are created in Salesforce.&lt;/li&gt;&lt;/ul&gt; |
|Append Data Map - Entry Label|  &lt;ul&gt;&lt;li&gt;(Optional) If provided, this text is appended to the start of the appended columns values.&lt;/li&gt;&lt;li&gt;Leave empty if not used.&lt;/li&gt;&lt;li&gt;See &#34;Append Data Map&#34; section for the exact format.&lt;/li&gt;&lt;/ul&gt; |

### Update Contact

#### Parameters

|Parameter| Description|
|---| ---|
| Contact ID | (Required) Select the Salesforce field used to identify the contact to update.|
|Update Data to Set| Select and map Tealium attributes to Salesforce contact fields for record update.|
| Append Data Map | &lt;ul&gt;&lt;li&gt;(Optional) Use this section to append multiple AudienceStream attributes to the same Salesforce text area field.&lt;/li&gt;&lt;li&gt;Map multiple values to the same Salesforce field key as needed.&lt;/li&gt;&lt;li&gt;For update and upsert actions, existing field content is preserved and new values are appended in formatted text.&lt;/li&gt;&lt;li&gt;Only Salesforce fields of type TextArea are supported.&lt;/li&gt;&lt;li&gt;Ensure the selected field has sufficient length to prevent API errors.&lt;/li&gt;&lt;li&gt;Appended values are represented in Salesforce according to their AudienceStream data type (for example, Boolean, String, JSON).&lt;/li&gt;&lt;li&gt;The appended text includes the optional entry label (if provided), current ISO UTC date, and the mapped key-value pairs on separate lines.&lt;/li&gt;&lt;/ul&gt; |
|Append Data Map - Entry Label|  &lt;ul&gt;&lt;li&gt;(Optional) If provided, this text is appended to the start of the appended columns values.&lt;/li&gt;&lt;li&gt;Leave empty if not used.&lt;/li&gt;&lt;li&gt;See &#34;Append Data Map&#34; section for the exact format.&lt;/li&gt;&lt;/ul&gt; |

### Add Contact to Campaign

#### Parameters

|Parameter| Description|
|---| ---|
| Contact ID | (Required) Select the Salesforce field used to identify the contact to update.|
|Campaign| Select the target campaign for the contact.|

### Send Entire Visitor to Custom Apex

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Apex Endpoint URL | (Required) The Custom Apex REST endpoint. Enter either a full URL (for example, `https://myorg.my.salesforce.com/services/apexrest/TealiumVisitor`) or a relative path (for example, `/services/apexrest/TealiumVisitor`). The path must contain `/services/apexrest/`. |
| Include Current Visit Data | Include current visit data with visitor data. |
| Print Attribute Names | By default, the attribute keys are used. Enable to use attribute names as keys instead. |

### Send Entire Event to Custom Apex

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Apex Endpoint URL | (Required) The Custom Apex REST endpoint. Enter either a full URL (for example, `https://myorg.my.salesforce.com/services/apexrest/TealiumEvent`) or a relative path (for example, `/services/apexrest/TealiumEvent`). The path must contain `/services/apexrest/`. |
| Print Attribute Names | By default, the attribute keys are used. Enable to use attribute names as keys instead. |

### Upsert into Custom Object (non-batched)

#### Parameters

| Parameter | Description |
| --- | --- |
| Custom Object | Select the custom object to perform an upsert. |

#### Lookup

| Parameter | Description |
| --- | --- |
| Lookup | Data to lookup external ID.|

#### Data Mapping

| Parameter | Description |
| --- | --- |
| Data mapping | Data to modify when upserting records. |

### Upsert into Custom Object (batched)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 5 minutes
* Max size of requests: 10 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Custom Object | Select the custom object to perform an upsert. |

#### Lookup

| Parameter | Description |
| --- | --- |
| Lookup | Data to lookup external ID.|

#### Data Mapping

| Parameter | Description |
| --- | --- |
| Data mapping | Data to modify when upserting records. |
