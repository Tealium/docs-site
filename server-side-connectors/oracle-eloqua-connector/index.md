---
title: Oracle Eloqua Connector Setup Guide
description: This article describes how to set up the Oracle Eloqua connector service in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/oracle-eloqua-connector/
---
## Requirements

* Oracle Eloqua account
* Company name for your Oracle Eloqua account
* Username for your Oracle Eloqua account
* Password for your Oracle Eloqua account
* If the allow list is enabled for Oracle Eloqua, add the [AudienceStream server IP addresses](https://docs.tealium.com/ip-allow-list/) to the Oracle Eloqua allow list.

<blockquote>
If the IP addresses are not added to the allow list at Oracle Eloqua or the Oracle Eloqua allow list is not disabled, the Import Definition action will fail with a `DD: ELOQUA UNABLE TO RETRIEVE VENDOR ENDPOINT` error.
</blockquote>


## Supported actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Update Contact via Bulk API| ✓| ✗|
|Add Contact to Shared List| ✓| ✗|
|Remove Contact from Shared List| ✓| ✗|
|Insert or Update Contact| ✓| ✗|
|Insert Contact| ✓| ✗|
|Update Contact| ✓| ✗|
|Subscribe Contact to Email Group| ✓| ✗|
|Unsubscribe Contact from Email Group| ✓| ✗|
|Insert Custom Object Data for Contact| ✓| ✗|
|Insert or Update Custom Object Data for Contact| ✓| ✗|

## Batch Limits
  
This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 32 MB

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following required settings:

* Company
* Username
* Password

### Configure New Import Definition

The import definition creates a structure for your uploaded data. In the definition, you configure the fields you will be uploading to Tealium. You can also configure data syncs to a contact list or an email list.

After you create the import definition, Tealium will automatically synchronize the data when you import it.

|**Parameter**| **Description** |
| --- | --- |
| Import Definition Name | (Required) The name of your contact import definition. |
| Contact Fields |  (Required) Select contact fields to use during upload. |
| Identifier Field Name | (Required) Select the field to check the imported data against existing records within Oracle Eloqua. It should match one of the **Contact Fields** and contain unique data for each record. |
| Optional - Update Rule | Select the action to update values in the Oracle Eloqua database from values imported with this import definition:<ul><li>`always`: Always update the value.</li><li>`ifNewIsNotNull`: Update the value if the new value is not blank.</li><li>`ifExistingIsNull`: Update the value if the existing value is blank.</li><li>`useFieldRule`: Use the field level-defined rule.</li></ul> |
| Optional - Sync to Contact List | Select a contact list to sync this contact to. |
| Optional - Sync to Contact List Action | Select the sync action of the contact list for this import definition: `add` or `remove`. |
| Optional - Sync to Email Group | Select an email group to sync this contact to. |
| Optional - Sync to Email Group Action | Select the sync action of the email group for this import definition: `subscribed` or `unsubscribed`. |

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Update Contact via Bulk API

The Bulk API queues requests until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 32 MB

For more information, see [Oracle Eloqua Bulk API](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-develop/Developers/BulkAPI/bulk-API.htm).

#### Parameters

|**Parameter**| **Description**|
| --- | --- |
|Contact Import Definition| (Required) Select the import definition for this batch upload. |
|Contact Data |  Map attributes to the import definition fields. |

### Action - Add Contact to Shared List


<blockquote>
Only the first 1,000 Shared Lists are retrieved from your account. If you cannot find a specific Shared List, use the "Custom Text" option, providing only the numeric ID of the Shared List. Entering the text name may result in errors.
</blockquote>
 


<blockquote>
If "API Contact ID" is not specified, an extra API call will be made to search the Target Contact according to **Contact Fields** specified in the **Contact Lookup** parameter.
</blockquote>


#### Parameters

|**Parameter**| **Description**|
| --- | --- |
|Target Shared List| (Required) Target Shared List for the Target Contact. |
|Contact Lookup|  <ul><li>API Contact ID – Target Contact ID</li><li>Contact Fields – If "API Contact ID" is not specified, the **Contact Fields** will be used to search for the Target Contact.</li><li>Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`</li></ul>|

### Action - Remove Contact from Shared List


<blockquote>
If "API Contact ID" is not specified, an extra API call will be made to search the Target Contact according to **Contact Fields** specified in the **Contact Lookup** parameter.
</blockquote>


#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Shared List| (Required) Target Shared List for the Target Contact. |
|Contact Lookup|  <ul><li>API Contact ID – Target Contact ID</li><li>Contact Fields – if "API Contact ID" is not specified, the **Contact Fields** will be used to search for the Target Contact.  </li><li>Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`</li></ul> |

### Action - Insert or Update Contact


<blockquote>
If "API Contact ID" is not specified, an extra API call will be made to search the Target Contact according to **Contact Fields** specified in the **Contact Lookup** parameter.
</blockquote>


#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Update Strategy|  <ul><li>(Required) Select applicable update strategy.  <ul><li>Create Only – Create new contact without lookup.</li><li>Update Only – Look up an existing contact and update it.</li><li>Create or Update – Look up an existing contact and if found, update it, otherwise create a new contact.</li></ul> </li></ul> |
|Contact Lookup|  <ul><li>Required if Update Strategy is **Update Only**, **Create**, or **Update**.</li><li>Contact Fields – if "API Contact ID" is not specified, these fields will be used to search for the Target Contact.  </li></ul> <ul><li>Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`</li></ul> |
|Create Contact Data|  <ul><li>Required if Update Strategy is **Create Only**, **Create**, or **Update**.</li><li>Map values to create a new contact.</li><li>Date attributes are converted to Unix timestamp in seconds.</li></ul> |
|Update Contact Data|  <ul><li>Required if Update Strategy is **Update Only**, **Create**, or **Update**.</li><li>Map values to update an existing contact.</li><li>Date attributes are converted to Unix timestamp in seconds.</li></ul> |

### Action - Insert Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Data To Set|  <ul><li>(Required) Map values to contact fields.</li><li>Date attributes are converted to Unix timestamp in seconds.</li></ul> |

### Action - Update Contact


<blockquote>
If "API Contact ID" is not specified, an extra API call will be made to search the Target Contact according to **Contact Fields** specified in the **Contact Lookup** parameter.
</blockquote>


#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact Lookup|  <ul><li>API Contact ID – Target Contact ID</li><li>Contact Fields – if "API Contact ID" is not specified, these fields will be used to search for the Target Contact.  </li><li>Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`</li></ul> |
|Data To Set|  <ul><li>(Required) Map values to contact fields</li><li>Date attributes are converted to Unix timestamp in seconds</li></ul> |

### Action - Subscribe Contact to Email Group


<blockquote>
If "API Contact ID" is not specified, an extra API call will be made to search the Target Contact according to **Contact Fields** specified in the **Contact Lookup** parameter.
</blockquote>


#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Email Group|  <ul><li>(Required) Target Email Group for the Target Contact</li></ul> |
|Contact Lookup|  <ul><li>API Contact ID – Target Contact ID</li><li>Contact Fields – if "API Contact ID" is not specified, the **Contact Fields** will be used to search for the Target Contact.  </li><li>Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`</li></ul> |

### Action - Unsubscribe Contact from Email Group


<blockquote>
If "API Contact ID" is not specified, an extra API call will be made to search the Target Contact according to **Contact Fields** specified in the **Contact Lookup** parameter.
</blockquote>
 

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Email Group|  <ul><li>(Required) Target Email Group for the Target Contact</li></ul> |
|Contact Lookup|  <ul><li>API Contact ID – Target Contact ID</li><li>Contact Fields – if "API Contact ID" is not specified, the **Contact Fields** will be used to search for the Target Contact. </li><li>Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`</li></ul> |

### Action - Insert Custom Object Data for Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact Lookup|  <ul><li>(Required) Contact is used to map the contact to the Target Custom Object.</li><li>Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`</li></ul> |
|Target Custom Object|  <ul><li>(Required)</li></ul> |
|Custom Object Data to Set|  <ul><li>(Required) Map values to contact custom object fields.</li><li>Date attributes are converted to Unix timestamp in seconds.</li></ul> |

### Action - Insert or Update Custom Object Data for Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact Lookup|  <ul><li>(Required) Contact is used to map the contact to the Target Custom Object.</li><li>Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`</li></ul> |
|Target Custom Object|  <ul><li>(Required) The [Custom Object](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/#Help/CustomObjects/CustomObjects.htm) to create or update a record in.</li></ul> |
|Record Lookup|  <ul><li>(Required) If a record is found with these fields and values; an update will be performed with the **Update Parameters** below.</li><li>If no record is found, an insert will be performed with the **Insert Parameters** below.</li><li>The fields and values must all exist and match for an update to be performed. Only 50 records (related to the Contact Lookup) are searched. </li><li>Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`</li></ul> |
|Record create data to set|  <ul><li>(Required) If the record cannot be found, these values will be used for creating the record. Date attributes are converted to Unix timestamp in seconds.</li></ul> |
|Record update data to set|  <ul><li>(Required) If the record is found, these values will be used for updating the record. Date attributes are converted to Unix timestamp in seconds.</li></ul> |
