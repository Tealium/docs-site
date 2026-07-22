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

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **API Username**
* **API Password**
* **Server Host**  
Contact your Oracle Responsys representative to get the appropriate server host.  

<blockquote>
When entering the server host, do not include the protocol or the path.
</blockquote>


## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Merge Visitor into Profile Extension Table

|**Parameter**| **Description**|
|---| ---|
|Table Folder Name| Required|
|Table Object Name| Required|
|Update Strategy|  <ul><li>(Required) Controls how the existing record should be updated.</li><li>NO_UPDATE — When selected, if an existing record is matched, no update will happen. Therefore, to enforce an INSERT only, use this option.</li><li>REPLACE_ALL – When selected, if an existing record is matched, all the properties configured will be updated.</li></ul> |
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
|Update Strategy|  <ul><li>Required, controls how the existing record should be updated.</li><li>NO_UPDATE – When selected, if an existing record is matched, no update will happen. Therefore, to enforce an INSERT only, use this option and check the **Insert on No Match** checkbox.</li><li>REPLACE_ALL — When selected, if an existing record is matched, all the properties configured will be updated.</li></ul> |
|Insert on No Match| Optional|
|Pass Empty Values for Data Columns(s) to Set| Optional|
|Data Column(s) to Set|  <ul><li>(Required) Ensure you have included primary key columns.</li><li>To pass a List, use a List Attribute and ensure all the lists have the same index length.</li></ul> |

### Action - Merge Visitor into List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List Folder Name|
|List Object Name|
|Update Strategy|  <ul><li>(Required) Controls how the existing record should be updated.</li><li>NO_UPDATE — When selected, if an existing record is matched, no update will happen. Therefore, to enforce an INSERT only, use this option and check the **Insert on No Match** checkbox.</li><li>REPLACE_ALL — When selected, if an existing record is matched, all the properties configured will be updated.</li></ul> |
|Insert on No Match|
|RIID|
|CUSTOMER_ID|
|EMAIL_ADDRESS|
|Pass Empty Values for Data Columns(s) to Set|
|Data Column(s) to Set|  <ul><li>(Required) Please specify the record data to merge.</li></ul> |
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
|Optional Data Map|  <ul><li>(Optional) Custom Event data that the user can set to any value</li></ul> |

## Vendor Documentation

* [Oracle Marketing Cloud - Oracle Responsys API](https://docs.oracle.com/cloud/latest/marketingcs_gs/responsys.html)
