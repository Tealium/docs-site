---
title: Oracle Responsys Marketing Cloud Connector Setup Guide
description: This article describes how to set up the Oracle Responsys Marketing Cloud connector.
url: https://docs.tealium.com/server-side-connectors/oracle-responsys-marketing-cloud-connector/
---

## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Merge List Recipients| ✓| ✓|
|Merge Profile Extension Recipients| ✓| ✓|
|Merge Table Records| ✓| ✓|
|Trigger Custom Event| ✓| ✓|

### Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100
* Max time since oldest request: 60 minutes
* Max size of requests: 1 MB

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **API Username**
* **API Password**
* **Login Endpoint**

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Merge List Recipients

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List Name|  <ul><li>Required</li></ul> |
|Default Permission Status|  <ul><li>(Optional) Values are **Opt In** or **Opt Out**.</li></ul> |
|Match Columns|  <ul><li>(Optional) The column name to be used to match the recipient record to the Profile Extension records.</li></ul> |
|Match Operator|  <ul><li>(Optional) Operator to join match column names.</li></ul> |
|Update Strategy|  <ul><li>(Optional) Controls how the existing record should be updated.  <ul><li>**No Update** — When selected, if an existing record is matched, no update will happen (Insert only).</li><li>**Replace All** — When selected, if an existing record is matched, all the properties configured will be updated.</li></ul> </li></ul> |
|HTML Value|  <ul><li>(Optional) Value of incoming preferred email format data.</li><li>Example: `H` may represent a preference for HTML-formatted email.</li></ul> |
|Opt In Value|  <ul><li>(Optional) Value of incoming opt-in status data that represents an opt-in status.</li><li>Example: `I` may represent an opt-in status.</li></ul> |
|Opt Out Value|  <ul><li>(Optional) Value of incoming opt-out status data that represents an opt-out status.</li><li>Example: `O` may represent an opt-out status.</li></ul> |
|Reject Record if Channel Empty|  <ul><li>(Optional) String containing a comma-separated channel codes that will result in record rejection when the channel address filed is null.</li><li>Channel codes are:  <ul><li>**E** – Email</li><li>**M** – Mobile</li><li>**P** – Postal Code</li></ul> </li></ul> <ul><li>Example" `"E,M"` indicates that a record that has a null value for the email or mobile number value should be rejected.</li></ul> |
|Text Value|  <ul><li>(Optional) Value of incoming preferred email format data.</li><li>Example: `T` may represent a preference for text-formatted email.</li></ul> |

### Action - Merge Profile Extension Recipients

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List Name|  <ul><li>Required</li></ul> |
|Profile Extension Table (PET) Name|  <ul><li>Profile extension table name.</li></ul> |
|Update Strategy|  <ul><li>(Required) Controls how the existing record should be updated.  <ul><li>**No Update** — When selected, if an existing record is matched, no update will happen (Insert only).</li><li>**Replace All** — When selected, if an existing record is matched, all the properties configured will be updated.</li></ul> </li></ul> |
|Match Columns|  <ul><li>The column name to be used to match the recipient record to the profile extension records.</li><li>Options are:  <ul><li>Recipient ID (RIID)</li><li>Customer ID</li><li>Email Address</li><li>Mobile Number</li><li>Email (MD5 hashed)</li><li>Email (SHA 256 hashed)</li></ul> </li></ul> |
|Map Template Name|  <ul><li>(Optional) Specify a mapping template configured in Oracle Responsys.</li></ul> |

### Action - Merge Table Records

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Folder Name|  <ul><li>Required</li></ul> |
|Table Name|  <ul><li>Required</li></ul> |
|Update Strategy|  <ul><li>(Required) Controls how the existing record should be updated.  <ul><li>**No Update** — When selected, if an existing record is matched, no update will happen (Insert only).</li><li>**Replace All** — When selected, if an existing record is matched, all the properties configured will be updated.</li></ul> </li></ul> |
|Match Columns|  <ul><li>The column name to be used to match the recipient record to the Supplemental Table records.</li></ul> |
|Map Template Name|  <ul><li>(Optional) Specify a mapping template configured in Oracle Responsys.</li></ul> |

### Action - Trigger Custom Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event Name|  <ul><li>(Required) Custom Event Name</li></ul> |
|Folder Name|  <ul><li>Required</li></ul> |
|Object Name|  <ul><li>(Required) Profile List Name</li></ul> |
|Email Format|  <ul><li>(Required) Values are **Text** or **HTML**.</li></ul> |
|Customer ID|  <ul><li>Customer ID</li></ul> |
|Email Address|  <ul><li>Email Address</li></ul> |
|Mobile Number|  <ul><li>Mobile Number</li></ul> |
|Mobile Number|  <ul><li>Mobile Number</li></ul> |
|Number Data Mapping|  <ul><li>Optional</li></ul> |
|Date Data Mapping|  <ul><li>Optional</li></ul> |
|String Data Mapping|  <ul><li>Optional</li></ul> |
|Optional Data|  <ul><li>Optional</li></ul> |

## Vendor documentation

* [Oracle Marketing Cloud - Oracle Responsys API](https://docs.oracle.com/cloud/latest/marketingcs_gs/responsys.html)
