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

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100
* Max time since oldest request: 60 minutes
* Max size of requests: 1 MB

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

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
|List Name|  &lt;ul&gt;&lt;li&gt;Required&lt;/li&gt;&lt;/ul&gt; |
|Default Permission Status|  &lt;ul&gt;&lt;li&gt;(Optional) Values are **Opt In** or **Opt Out**.&lt;/li&gt;&lt;/ul&gt; |
|Match Columns|  &lt;ul&gt;&lt;li&gt;(Optional) The column name to be used to match the recipient record to the Profile Extension records.&lt;/li&gt;&lt;/ul&gt; |
|Match Operator|  &lt;ul&gt;&lt;li&gt;(Optional) Operator to join match column names.&lt;/li&gt;&lt;/ul&gt; |
|Update Strategy|  &lt;ul&gt;&lt;li&gt;(Optional) Controls how the existing record should be updated.  &lt;ul&gt;&lt;li&gt;**No Update** — When selected, if an existing record is matched, no update will happen (Insert only).&lt;/li&gt;&lt;li&gt;**Replace All** — When selected, if an existing record is matched, all the properties configured will be updated.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|HTML Value|  &lt;ul&gt;&lt;li&gt;(Optional) Value of incoming preferred email format data.&lt;/li&gt;&lt;li&gt;Example: `H` may represent a preference for HTML-formatted email.&lt;/li&gt;&lt;/ul&gt; |
|Opt In Value|  &lt;ul&gt;&lt;li&gt;(Optional) Value of incoming opt-in status data that represents an opt-in status.&lt;/li&gt;&lt;li&gt;Example: `I` may represent an opt-in status.&lt;/li&gt;&lt;/ul&gt; |
|Opt Out Value|  &lt;ul&gt;&lt;li&gt;(Optional) Value of incoming opt-out status data that represents an opt-out status.&lt;/li&gt;&lt;li&gt;Example: `O` may represent an opt-out status.&lt;/li&gt;&lt;/ul&gt; |
|Reject Record if Channel Empty|  &lt;ul&gt;&lt;li&gt;(Optional) String containing a comma-separated channel codes that will result in record rejection when the channel address filed is null.&lt;/li&gt;&lt;li&gt;Channel codes are:  &lt;ul&gt;&lt;li&gt;**E** – Email&lt;/li&gt;&lt;li&gt;**M** – Mobile&lt;/li&gt;&lt;li&gt;**P** – Postal Code&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;Example&#34; `&#34;E,M&#34;` indicates that a record that has a null value for the email or mobile number value should be rejected.&lt;/li&gt;&lt;/ul&gt; |
|Text Value|  &lt;ul&gt;&lt;li&gt;(Optional) Value of incoming preferred email format data.&lt;/li&gt;&lt;li&gt;Example: `T` may represent a preference for text-formatted email.&lt;/li&gt;&lt;/ul&gt; |

### Action - Merge Profile Extension Recipients

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List Name|  &lt;ul&gt;&lt;li&gt;Required&lt;/li&gt;&lt;/ul&gt; |
|Profile Extension Table (PET) Name|  &lt;ul&gt;&lt;li&gt;Profile extension table name.&lt;/li&gt;&lt;/ul&gt; |
|Update Strategy|  &lt;ul&gt;&lt;li&gt;(Required) Controls how the existing record should be updated.  &lt;ul&gt;&lt;li&gt;**No Update** — When selected, if an existing record is matched, no update will happen (Insert only).&lt;/li&gt;&lt;li&gt;**Replace All** — When selected, if an existing record is matched, all the properties configured will be updated.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Match Columns|  &lt;ul&gt;&lt;li&gt;The column name to be used to match the recipient record to the profile extension records.&lt;/li&gt;&lt;li&gt;Options are:  &lt;ul&gt;&lt;li&gt;Recipient ID (RIID)&lt;/li&gt;&lt;li&gt;Customer ID&lt;/li&gt;&lt;li&gt;Email Address&lt;/li&gt;&lt;li&gt;Mobile Number&lt;/li&gt;&lt;li&gt;Email (MD5 hashed)&lt;/li&gt;&lt;li&gt;Email (SHA 256 hashed)&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Map Template Name|  &lt;ul&gt;&lt;li&gt;(Optional) Specify a mapping template configured in Oracle Responsys.&lt;/li&gt;&lt;/ul&gt; |

### Action - Merge Table Records

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Folder Name|  &lt;ul&gt;&lt;li&gt;Required&lt;/li&gt;&lt;/ul&gt; |
|Table Name|  &lt;ul&gt;&lt;li&gt;Required&lt;/li&gt;&lt;/ul&gt; |
|Update Strategy|  &lt;ul&gt;&lt;li&gt;(Required) Controls how the existing record should be updated.  &lt;ul&gt;&lt;li&gt;**No Update** — When selected, if an existing record is matched, no update will happen (Insert only).&lt;/li&gt;&lt;li&gt;**Replace All** — When selected, if an existing record is matched, all the properties configured will be updated.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Match Columns|  &lt;ul&gt;&lt;li&gt;The column name to be used to match the recipient record to the Supplemental Table records.&lt;/li&gt;&lt;/ul&gt; |
|Map Template Name|  &lt;ul&gt;&lt;li&gt;(Optional) Specify a mapping template configured in Oracle Responsys.&lt;/li&gt;&lt;/ul&gt; |

### Action - Trigger Custom Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event Name|  &lt;ul&gt;&lt;li&gt;(Required) Custom Event Name&lt;/li&gt;&lt;/ul&gt; |
|Folder Name|  &lt;ul&gt;&lt;li&gt;Required&lt;/li&gt;&lt;/ul&gt; |
|Object Name|  &lt;ul&gt;&lt;li&gt;(Required) Profile List Name&lt;/li&gt;&lt;/ul&gt; |
|Email Format|  &lt;ul&gt;&lt;li&gt;(Required) Values are **Text** or **HTML**.&lt;/li&gt;&lt;/ul&gt; |
|Customer ID|  &lt;ul&gt;&lt;li&gt;Customer ID&lt;/li&gt;&lt;/ul&gt; |
|Email Address|  &lt;ul&gt;&lt;li&gt;Email Address&lt;/li&gt;&lt;/ul&gt; |
|Mobile Number|  &lt;ul&gt;&lt;li&gt;Mobile Number&lt;/li&gt;&lt;/ul&gt; |
|Mobile Number|  &lt;ul&gt;&lt;li&gt;Mobile Number&lt;/li&gt;&lt;/ul&gt; |
|Number Data Mapping|  &lt;ul&gt;&lt;li&gt;Optional&lt;/li&gt;&lt;/ul&gt; |
|Date Data Mapping|  &lt;ul&gt;&lt;li&gt;Optional&lt;/li&gt;&lt;/ul&gt; |
|String Data Mapping|  &lt;ul&gt;&lt;li&gt;Optional&lt;/li&gt;&lt;/ul&gt; |
|Optional Data|  &lt;ul&gt;&lt;li&gt;Optional&lt;/li&gt;&lt;/ul&gt; |

## Vendor documentation

* [Oracle Marketing Cloud - Oracle Responsys API](https://docs.oracle.com/cloud/latest/marketingcs_gs/responsys.html)
