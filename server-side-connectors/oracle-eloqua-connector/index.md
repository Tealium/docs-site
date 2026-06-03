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
* If the allow list is enabled for Oracle Eloqua, add the [AudienceStream server IP addresses]() to the Oracle Eloqua allow list.
If the IP addresses are not added to the allow list at Oracle Eloqua or the Oracle Eloqua allow list is not disabled, the Import Definition action will fail with a `DD: ELOQUA UNABLE TO RETRIEVE VENDOR ENDPOINT` error.

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
  
This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 60 minutes
* Max size of requests: 32 MB

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

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
| Optional - Update Rule | Select the action to update values in the Oracle Eloqua database from values imported with this import definition:&lt;ul&gt;&lt;li&gt;`always`: Always update the value.&lt;/li&gt;&lt;li&gt;`ifNewIsNotNull`: Update the value if the new value is not blank.&lt;/li&gt;&lt;li&gt;`ifExistingIsNull`: Update the value if the existing value is blank.&lt;/li&gt;&lt;li&gt;`useFieldRule`: Use the field level-defined rule.&lt;/li&gt;&lt;/ul&gt; |
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

Only the first 1,000 Shared Lists are retrieved from your account. If you cannot find a specific Shared List, use the &#34;Custom Text&#34; option, providing only the numeric ID of the Shared List. Entering the text name may result in errors. 

If &#34;API Contact ID&#34; is not specified, an extra API call will be made to search the Target Contact according to **Contact Fields** specified in the **Contact Lookup** parameter. 

#### Parameters

|**Parameter**| **Description**|
| --- | --- |
|Target Shared List| (Required) Target Shared List for the Target Contact. |
|Contact Lookup|  &lt;ul&gt;&lt;li&gt;API Contact ID – Target Contact ID&lt;/li&gt;&lt;li&gt;Contact Fields – If &#34;API Contact ID&#34; is not specified, the **Contact Fields** will be used to search for the Target Contact.&lt;/li&gt;&lt;li&gt;Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`&lt;/li&gt;&lt;/ul&gt;|

### Action - Remove Contact from Shared List

If &#34;API Contact ID&#34; is not specified, an extra API call will be made to search the Target Contact according to **Contact Fields** specified in the **Contact Lookup** parameter.

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Shared List| (Required) Target Shared List for the Target Contact. |
|Contact Lookup|  &lt;ul&gt;&lt;li&gt;API Contact ID – Target Contact ID&lt;/li&gt;&lt;li&gt;Contact Fields – if &#34;API Contact ID&#34; is not specified, the **Contact Fields** will be used to search for the Target Contact.  &lt;/li&gt;&lt;li&gt;Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`&lt;/li&gt;&lt;/ul&gt; |

### Action - Insert or Update Contact

If &#34;API Contact ID&#34; is not specified, an extra API call will be made to search the Target Contact according to **Contact Fields** specified in the **Contact Lookup** parameter.

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Update Strategy|  &lt;ul&gt;&lt;li&gt;(Required) Select applicable update strategy.  &lt;ul&gt;&lt;li&gt;Create Only – Create new contact without lookup.&lt;/li&gt;&lt;li&gt;Update Only – Look up an existing contact and update it.&lt;/li&gt;&lt;li&gt;Create or Update – Look up an existing contact and if found, update it, otherwise create a new contact.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Contact Lookup|  &lt;ul&gt;&lt;li&gt;Required if Update Strategy is **Update Only**, **Create**, or **Update**.&lt;/li&gt;&lt;li&gt;Contact Fields – if &#34;API Contact ID&#34; is not specified, these fields will be used to search for the Target Contact.  &lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`&lt;/li&gt;&lt;/ul&gt; |
|Create Contact Data|  &lt;ul&gt;&lt;li&gt;Required if Update Strategy is **Create Only**, **Create**, or **Update**.&lt;/li&gt;&lt;li&gt;Map values to create a new contact.&lt;/li&gt;&lt;li&gt;Date attributes are converted to Unix timestamp in seconds.&lt;/li&gt;&lt;/ul&gt; |
|Update Contact Data|  &lt;ul&gt;&lt;li&gt;Required if Update Strategy is **Update Only**, **Create**, or **Update**.&lt;/li&gt;&lt;li&gt;Map values to update an existing contact.&lt;/li&gt;&lt;li&gt;Date attributes are converted to Unix timestamp in seconds.&lt;/li&gt;&lt;/ul&gt; |

### Action - Insert Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Data To Set|  &lt;ul&gt;&lt;li&gt;(Required) Map values to contact fields.&lt;/li&gt;&lt;li&gt;Date attributes are converted to Unix timestamp in seconds.&lt;/li&gt;&lt;/ul&gt; |

### Action - Update Contact

If &#34;API Contact ID&#34; is not specified, an extra API call will be made to search the Target Contact according to **Contact Fields** specified in the **Contact Lookup** parameter.

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact Lookup|  &lt;ul&gt;&lt;li&gt;API Contact ID – Target Contact ID&lt;/li&gt;&lt;li&gt;Contact Fields – if &#34;API Contact ID&#34; is not specified, these fields will be used to search for the Target Contact.  &lt;/li&gt;&lt;li&gt;Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`&lt;/li&gt;&lt;/ul&gt; |
|Data To Set|  &lt;ul&gt;&lt;li&gt;(Required) Map values to contact fields&lt;/li&gt;&lt;li&gt;Date attributes are converted to Unix timestamp in seconds&lt;/li&gt;&lt;/ul&gt; |

### Action - Subscribe Contact to Email Group

If &#34;API Contact ID&#34; is not specified, an extra API call will be made to search the Target Contact according to **Contact Fields** specified in the **Contact Lookup** parameter.

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Email Group|  &lt;ul&gt;&lt;li&gt;(Required) Target Email Group for the Target Contact&lt;/li&gt;&lt;/ul&gt; |
|Contact Lookup|  &lt;ul&gt;&lt;li&gt;API Contact ID – Target Contact ID&lt;/li&gt;&lt;li&gt;Contact Fields – if &#34;API Contact ID&#34; is not specified, the **Contact Fields** will be used to search for the Target Contact.  &lt;/li&gt;&lt;li&gt;Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`&lt;/li&gt;&lt;/ul&gt; |

### Action - Unsubscribe Contact from Email Group

If &#34;API Contact ID&#34; is not specified, an extra API call will be made to search the Target Contact according to **Contact Fields** specified in the **Contact Lookup** parameter. 

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Target Email Group|  &lt;ul&gt;&lt;li&gt;(Required) Target Email Group for the Target Contact&lt;/li&gt;&lt;/ul&gt; |
|Contact Lookup|  &lt;ul&gt;&lt;li&gt;API Contact ID – Target Contact ID&lt;/li&gt;&lt;li&gt;Contact Fields – if &#34;API Contact ID&#34; is not specified, the **Contact Fields** will be used to search for the Target Contact. &lt;/li&gt;&lt;li&gt;Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`&lt;/li&gt;&lt;/ul&gt; |

### Action - Insert Custom Object Data for Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact Lookup|  &lt;ul&gt;&lt;li&gt;(Required) Contact is used to map the contact to the Target Custom Object.&lt;/li&gt;&lt;li&gt;Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`&lt;/li&gt;&lt;/ul&gt; |
|Target Custom Object|  &lt;ul&gt;&lt;li&gt;(Required)&lt;/li&gt;&lt;/ul&gt; |
|Custom Object Data to Set|  &lt;ul&gt;&lt;li&gt;(Required) Map values to contact custom object fields.&lt;/li&gt;&lt;li&gt;Date attributes are converted to Unix timestamp in seconds.&lt;/li&gt;&lt;/ul&gt; |

### Action - Insert or Update Custom Object Data for Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact Lookup|  &lt;ul&gt;&lt;li&gt;(Required) Contact is used to map the contact to the Target Custom Object.&lt;/li&gt;&lt;li&gt;Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`&lt;/li&gt;&lt;/ul&gt; |
|Target Custom Object|  &lt;ul&gt;&lt;li&gt;(Required) The [Custom Object](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/#Help/CustomObjects/CustomObjects.htm) to create or update a record in.&lt;/li&gt;&lt;/ul&gt; |
|Record Lookup|  &lt;ul&gt;&lt;li&gt;(Required) If a record is found with these fields and values; an update will be performed with the **Update Parameters** below.&lt;/li&gt;&lt;li&gt;If no record is found, an insert will be performed with the **Insert Parameters** below.&lt;/li&gt;&lt;li&gt;The fields and values must all exist and match for an update to be performed. Only 50 records (related to the Contact Lookup) are searched. &lt;/li&gt;&lt;li&gt;Date attributes are converted to the following format: `yyyy-MM-dd HH:mm:ss`&lt;/li&gt;&lt;/ul&gt; |
|Record create data to set|  &lt;ul&gt;&lt;li&gt;(Required) If the record cannot be found, these values will be used for creating the record. Date attributes are converted to Unix timestamp in seconds.&lt;/li&gt;&lt;/ul&gt; |
|Record update data to set|  &lt;ul&gt;&lt;li&gt;(Required) If the record is found, these values will be used for updating the record. Date attributes are converted to Unix timestamp in seconds.&lt;/li&gt;&lt;/ul&gt; |
