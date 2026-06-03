---
title: Oracle Responsys Connector Setup Guide for AudienceStream (SOAP API)
description: This article describes how to set up the Oracle Responsys connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/oracle-responsys-connector-soap-api/
---## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Merge Visitor into Profile Extension Table| ✓| ✗|
|Merge Visitor into Supplemental Table| ✓| ✗|
|Merge Visitor into List| ✓| ✗|
|Send Transactional Campaign Email| ✓| ✗|
|Trigger Custom Event| ✓| ✗|

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

After adding the connector, configure the following settings:

* **API Username**
* **API Password**
* **Server Host**  
Contact your Oracle Responsys representative to get the appropriate server host.  
When entering the server host, do not include the protocol or the path.

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Merge Visitor into Profile Extension Table

|**Parameter**| **Description**|
|---| ---|
|Table Folder Name| Required|
|Table Object Name| Required|
|Update Strategy|  &lt;ul&gt;&lt;li&gt;(Required) Controls how the existing record should be updated.&lt;/li&gt;&lt;li&gt;NO_UPDATE — When selected, if an existing record is matched, no update will happen. Therefore, to enforce an INSERT only, use this option.&lt;/li&gt;&lt;li&gt;REPLACE_ALL – When selected, if an existing record is matched, all the properties configured will be updated.&lt;/li&gt;&lt;/ul&gt; |
|RIID|
|CUSTOMER_ID|
|EMAIL_ADDRESS|
|Pass Empty Values for Data Columns(s) to Set| Optional|
|Data Column(s) to Set| Required, please specify the record data to merge.|

### Action - Merge Visitor into Supplemental Table

|**Parameter**| **Description**|
|---| ---|
|Table Folder Name| Required|
|Table Object Name| Required|
|Update Strategy|  &lt;ul&gt;&lt;li&gt;Required, controls how the existing record should be updated.&lt;/li&gt;&lt;li&gt;NO_UPDATE – When selected, if an existing record is matched, no update will happen. Therefore, to enforce an INSERT only, use this option and check the **Insert on No Match** checkbox.&lt;/li&gt;&lt;li&gt;REPLACE_ALL — When selected, if an existing record is matched, all the properties configured will be updated.&lt;/li&gt;&lt;/ul&gt; |
|Insert on No Match| Optional|
|Pass Empty Values for Data Columns(s) to Set| Optional|
|Data Column(s) to Set|  &lt;ul&gt;&lt;li&gt;(Required) Ensure you have included primary key columns.&lt;/li&gt;&lt;li&gt;To pass a List, use a List Attribute and ensure all the lists have the same index length.&lt;/li&gt;&lt;/ul&gt; |

### Action - Merge Visitor into List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List Folder Name|
|List Object Name|
|Update Strategy|  &lt;ul&gt;&lt;li&gt;(Required) Controls how the existing record should be updated.&lt;/li&gt;&lt;li&gt;NO_UPDATE — When selected, if an existing record is matched, no update will happen. Therefore, to enforce an INSERT only, use this option and check the **Insert on No Match** checkbox.&lt;/li&gt;&lt;li&gt;REPLACE_ALL — When selected, if an existing record is matched, all the properties configured will be updated.&lt;/li&gt;&lt;/ul&gt; |
|Insert on No Match|
|RIID|
|CUSTOMER_ID|
|EMAIL_ADDRESS|
|Pass Empty Values for Data Columns(s) to Set|
|Data Column(s) to Set|  &lt;ul&gt;&lt;li&gt;(Required) Please specify the record data to merge.&lt;/li&gt;&lt;/ul&gt; |
|optinValue|
|optoutValue|

### Action - Send Transactional Campaign Email

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Campaign Folder Name|
|Campaign Object Name|
|RIID|
|CUSTOMER_ID|
|EMAIL_ADDRESS|

### Action - Trigger Custom Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Recipient List Folder Name|
|Recipient List Object Name|
|RIID|
|CUSTOMER_ID|
|EMAIL_ADDRESS|
|Custom Event ID|
|Custom Event Name|
|Optional Data Map|  &lt;ul&gt;&lt;li&gt;(Optional) Custom Event data that the user can set to any value&lt;/li&gt;&lt;/ul&gt; |

## Vendor Documentation

* [Oracle Marketing Cloud - Oracle Responsys API](https://docs.oracle.com/cloud/latest/marketingcs_gs/responsys.html)
