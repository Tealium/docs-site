---
title: Mixpanel Connector Setup Guide
description: This article describes how to set up the Mixpanel connector.
url: https://docs.tealium.com/server-side-connectors/mixpanel-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Track Event| ✓| ✓|
|Update Profile - Set| ✓| ✓|
|Update Profile - Add| ✓| ✓|
|Update Profile - Append| ✓| ✓|
|Update Profile - Union| ✓| ✓|
|Update Profile - Unset| ✓| ✓|
|Update Profile - Delete| ✓| ✓|
|Update Profile - Track Revenue| ✓| ✓|
|Create Alias| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Project Token**: A project token is required to send profile and events data to Mixpanel. For more information, see [Where can I find my project token?](https://mixpanel.com/help/questions/articles/where-can-i-find-my-project-token).
* **Mixpanel API Base URL**: (Required) Select your Mixpanel API Base URL. For more information, see [Mixpanel : Privacy Program](https://mixpanel.com/legal/eu-data-residency/).
  * Standard Server: `api.mixpanel.com`
  * EU Residency Server: `api-eu.mixpanel.com`
  * India Residency Server: `api-in.mixpanel.com`

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Track Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|User ID| A unique identifier for the user associated with the event.|
|IP Address| The user's IP address. |
|Override Event Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |
|Event Name| (Required) The name of the event. |
|Event Data|  <ul><li>Custom properties to add to your event.</li><li>Date type properties are converted to Mixpanel date format `YYYY-MM-DDThh:mm:ss`.</li><li>Properties with empty values are skipped and not included.</li></ul> |

### Action - Update Profile - Set

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Ignore Last Seen Update| (Optional) If set to `true`, Mixpanel will not automatically update the "Last Seen" time property for the user profile. |
|User ID| (Required) A unique identifier for the user associated with the event. |
|IP Address| The user's IP address. |
|Override Update Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |
|Created| When the profile was updated. Date type properties are converted to Mixpanel date format `YYYY-MM-DDThh:mm:ss`. |
|Phone Number| The user's phone number.|
|Last Name| The user's last name.|
|Email| The user's email address. |
|First Name| The user's first name.|
|Full Name| The user's full name.|
|Do Not Overwrite Existing Property Values (Set Once)| Select this checkbox to prevent the connector from overwriting existing values. |

### Action - Update Profile - Add

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Ignore Last Seen Update|(Optional) If set to `true`, Mixpanel will not automatically update the "Last Seen" time property for the user profile. |
|User ID| (Required) A unique identifier for the user associated with the event. |
|IP Address| The user's IP address. |
|Override Update Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |
|Add Data|  <ul><li>Specify a number to add a numerical amount to their existing value.</li><li>Decrement values by providing a negative amount.</li><li>Properties with empty values are skipped and not included.</li></ul> |

### Action - Update Profile - Append

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Ignore Last Seen Update| (Optional) If set to `true`, Mixpanel will not automatically update the "Last Seen" time property for the user profile.|
|User ID| (Required) A unique identifier for the user associated with the event. |
|IP Address| The user's IP address. |
|Override Update Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |
|Append Data|  <ul><li>Specify properties to append a value to their existing list of values.</li><li>Appending to a property that doesn't exist produces a new list with one element.</li><li>Properties with empty values are skipped and not included.</li></ul> |

### Action - Update Profile - Union

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Ignore Last Seen Update| (Optional) If set to `true`, Mixpanel will not automatically update the "Last Seen" time property for the user profile.|
|User ID| (Required) A unique identifier for the user associated with the event. |
|IP Address| The user's IP address. |
|Override Update Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |
|Union Data|  <ul><li>Specify properties to merge their values with the existing list on the user profile.</li><li>Properties must be of Array type in Data Layer.</li><li>Properties with empty values are skipped and not included.</li><li>Duplicate values are ignored.</li></ul> |

### Action - Update Profile - Unset

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Ignore Last Seen Update|(Optional) If set to `true`, Mixpanel will not automatically update the "Last Seen" time property for the user profile.|
|User ID| (Required) A unique identifier for the user associated with the event. |
|IP Address| The user's IP address. |
|Override Update Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |
|Unset Data|  <ul><li>Specify properties to permanently remove them and their values from a user profile.</li><li>Supports Array type in Data Layer.</li></ul> |

### Action - Update Profile - Delete

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Ignore Last Seen Update| (Optional) If set to `true`, Mixpanel will not automatically update the "Last Seen" time property for the user profile.|
|User ID| (Required) A unique identifier for the user associated with the event. |
|IP Address| The user's IP address. |
|Override Update Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |

### Action - Update Profile - Track Revenue

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Ignore Last Seen Update|(Optional) If set to `true`, Mixpanel will not automatically update the "Last Seen" time property for the user profile.|
|User ID| (Required) A unique identifier for the user associated with the event. |
|IP Address| The user's IP address. |
|Override Update Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |
|Transaction Amount| (Required) The amount of the transaction.|
|Transaction Time| (Required) The time of the transaction. Date type properties are converted to Mixpanel date format 'YYYY-MM-DDThh:mm:ss'|

### Action - Create Alias

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Original User ID|  <ul><li>Previously set identifier for a user.</li><li>Typically a temporary generated ID before a better user ID becomes available (example: user's email after sign up)</li></ul> |
|New Alias User ID|  <ul><li>New ID to map to original ID.</li><li>Typically an alias is set immediately after user signs up and all subsequent events and updates utilize the new alias ID.</li><li>For more information, see [Mixpanel: Using Mixpanel Alias](https://mixpanel.com/docs/integration-libraries/using-mixpanel-alias)</li></ul>. |
