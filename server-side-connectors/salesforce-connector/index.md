---
title: Salesforce (Customer-Provided Credentials) Connector Setup Guide
description: This article describes how to set up the Salesforce (Customer-Provided Credentials) connector.
url: https://docs.tealium.com/server-side-connectors/salesforce-connector/
---

<blockquote>
If your existing Salesforce connector shows **Tealium-Provided Credentials (Deprecated)** as its authentication type, migrate it to the [Salesforce (Tealium-Provided Credentials)](https://docs.tealium.com/salesforce-tealium-provided-credentials-connector/) connector or change the authentication type to Client Credentials. The connector continues to send data until you migrate.
</blockquote>


## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

To use Tealium-managed OAuth credentials instead of your own connected app, see [Salesforce (Tealium-Provided Credentials)](https://docs.tealium.com/salesforce-tealium-provided-credentials-connector/).

### Set up a Salesforce connected app

Before you configure this connector, set up a Salesforce connected app with Client Credentials Flow enabled:

1. In Salesforce Setup, go to **App Manager** and create a new Connected App.
1. Enable **OAuth Settings** and add the following callback URL: `https://my.tealiumiq.com/oauth/salesforce/callback.html`
1. Select the required OAuth scopes. The minimum required scopes are `api` and `refresh_token`.
1. Enable **Client Credentials Flow** under OAuth Settings.
1. Under Client Credentials Flow, nominate a **Run As** user. The Run As user's permissions determine what data the connector can access.
1. Save and wait a few minutes for the app to activate.
1. Copy the Consumer Key and Consumer Secret to use in the fields below.

### Connect the connector

After adding the connector, configure the following settings:

* **Login URL (My Domain)**: (Required) Enter your Salesforce My Domain URL (for example, `https://mycompany.my.salesforce.com`). Client Credentials Flow requires your org-specific My Domain URL. Do not use `login.salesforce.com` or `test.salesforce.com`.
* **Consumer Key (Client ID)**: (Required) Enter the Consumer Key from your Salesforce Connected App or External Client App.
* **Consumer Secret (Client Secret)**: (Required) Enter the Consumer Secret from your Salesforce Connected App or External Client App. The app may take a few minutes to activate after creation.

Click **Test Connection** to verify the connection.

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
| Append Data Map | <ul><li>(Optional) Use this section to append multiple AudienceStream attributes to the same Salesforce text area field.</li><li>Map multiple values to the same Salesforce field key as needed.</li><li>For update and upsert actions, existing field content is preserved and new values are appended in formatted text.</li><li>Only Salesforce fields of type TextArea are supported.</li><li>Ensure the selected field has sufficient length to prevent API errors.</li><li>Appended values are represented in Salesforce according to their AudienceStream data type (for example, Boolean, String, JSON).</li><li>The appended text includes the optional entry label (if provided), current ISO UTC date, and the mapped key-value pairs on separate lines.</li></ul> |
|Append Data Map - Entry Label|  <ul><li>(Optional) If provided, this text is appended to the start of the appended columns values.</li><li>Leave empty if not used.</li><li>See "Append Data Map" section for the exact format.</li></ul> |
|Select Target Assignment Rule|  <ul><li>(Optional) A list that displays available assignment rules for your account that can be used to apply on your target lead.</li><li>Selecting the **Use Default Assignment Rule** enforces Salesforce to use the default rule for rule-based assignment.</li><li>Do not select any values or select **None** to avoid inclusion of assignment rule options in the API call.</li></ul> |

### Update Lead

#### Parameters

|Parameter| Description|
|---| ---|
| Lead ID | (Required) Select the Salesforce field used to identify the lead to update.|
|Update Data to Set| Select and map Tealium attributes to Salesforce lead fields for record update.|
| Append Data Map | <ul><li>(Optional) Use this section to append multiple AudienceStream attributes to the same Salesforce text area field.</li><li>Map multiple values to the same Salesforce field key as needed.</li><li>For update and upsert actions, existing field content is preserved and new values are appended in formatted text.</li><li>Only Salesforce fields of type TextArea are supported.</li><li>Ensure the selected field has sufficient length to prevent API errors.</li><li>Appended values are represented in Salesforce according to their AudienceStream data type (for example, Boolean, String, JSON).</li><li>The appended text includes the optional entry label (if provided), current ISO UTC date, and the mapped key-value pairs on separate lines.</li></ul> |
|Append Data Map - Entry Label|  <ul><li>(Optional) If provided, this text is appended to the start of the appended columns values.</li><li>Leave empty if not used.</li><li>See "Append Data Map" section for the exact format.</li></ul> |
|Select Target Assignment Rule|  <ul><li>(Optional) The list displays available assignment rules for your account that can be used to apply on your target lead.</li><li>Selecting **Use Default Assignment Rule** enforces Salesforce to use the default rule for rule-based assignment.</li><li>Do not select any values or select **None** to avoid inclusion of assignment rule options in the API call.</li></ul> |

### Upsert Lead

#### Parameters

|Parameter| Description|
|---| ---|
| Update Lookup ID | <ul><li>(Required) Select the Salesforce field used to identify an existing lead.</li><li>The value of this field determines whether the action updates an existing record or inserts a new one.</li></ul> |
| Update Data to Set | <ul><li>(Required) Map Tealium attributes to Salesforce lead fields to update when existing records are found.</li><li>To append multiple AudienceStream attributes to the same Salesforce field, use the Append Data Map section instead.</li><li>Values mapped here overwrite the existing field values in Salesforce.</li><li>Avoid configuring the same field in both sections. Use either Update Data to Set or Append Data Map, not both.</li></ul>  |
| Insert Data to Set | <ul><li>(Required) Map Tealium attributes to Salesforce lead fields for creating new records.</li><li>To append multiple AudienceStream attributes to the same Salesforce field, use the Append Data Map section instead.</li><li>Values mapped here populate the specified fields in the newly created lead record.</li><li>Avoid configuring the same field in both sections. Use either Insert Data to Set or Append Data Map, not both.</li></ul>  |
| Append Data Map | <ul><li>(Optional) Use this section to append multiple AudienceStream attributes to the same Salesforce text area field.</li><li>Map multiple values to the same Salesforce field key as needed.</li><li>For update and upsert actions, existing field content is preserved and new values are appended in formatted text.</li><li>Only Salesforce fields of type TextArea are supported.</li><li>Ensure the selected field has sufficient length to prevent API errors.</li><li>Appended values are represented in Salesforce according to their AudienceStream data type (for example, Boolean, String, JSON).</li><li>The appended text includes the optional entry label (if provided), current ISO UTC date, and the mapped key-value pairs on separate lines.</li></ul> |
|Append Data Map - Entry Label|  <ul><li>(Optional) If provided, this text is appended to the start of the appended columns values.</li><li>Leave empty if not used.</li><li>See "Append Data Map" section for the exact format.</li></ul> |
|Select Target Assignment Rule|  <ul><li>(Optional) The list displays available assignment rules for your account that can be used to apply on your target lead.</li><li>Selecting **Use Default Assignment Rule** enforces Salesforce to use the default rule for rule-based assignment.</li><li>Do not select any values or select **None** to avoid inclusion of assignment rule options in the API call.</li></ul> |

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
| Insert Contact |  <ul><li>(Required) Map Tealium attributes to Salesforce contact identity fields.</li><li>These fields are used to define the contact record that are created in Salesforce.</li></ul> |
|Append Data Map - Entry Label|  <ul><li>(Optional) If provided, this text is appended to the start of the appended columns values.</li><li>Leave empty if not used.</li><li>See "Append Data Map" section for the exact format.</li></ul> |

### Update Contact

#### Parameters

|Parameter| Description|
|---| ---|
| Contact ID | (Required) Select the Salesforce field used to identify the contact to update.|
|Update Data to Set| Select and map Tealium attributes to Salesforce contact fields for record update.|
| Append Data Map | <ul><li>(Optional) Use this section to append multiple AudienceStream attributes to the same Salesforce text area field.</li><li>Map multiple values to the same Salesforce field key as needed.</li><li>For update and upsert actions, existing field content is preserved and new values are appended in formatted text.</li><li>Only Salesforce fields of type TextArea are supported.</li><li>Ensure the selected field has sufficient length to prevent API errors.</li><li>Appended values are represented in Salesforce according to their AudienceStream data type (for example, Boolean, String, JSON).</li><li>The appended text includes the optional entry label (if provided), current ISO UTC date, and the mapped key-value pairs on separate lines.</li></ul> |
|Append Data Map - Entry Label|  <ul><li>(Optional) If provided, this text is appended to the start of the appended columns values.</li><li>Leave empty if not used.</li><li>See "Append Data Map" section for the exact format.</li></ul> |

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

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

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
