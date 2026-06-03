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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

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
|IP Address| The user&#39;s IP address. |
|Override Event Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |
|Event Name| (Required) The name of the event. |
|Event Data|  &lt;ul&gt;&lt;li&gt;Custom properties to add to your event.&lt;/li&gt;&lt;li&gt;Date type properties are converted to Mixpanel date format `YYYY-MM-DDThh:mm:ss`.&lt;/li&gt;&lt;li&gt;Properties with empty values are skipped and not included.&lt;/li&gt;&lt;/ul&gt; |

### Action - Update Profile - Set

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Ignore Last Seen Update| (Optional) If set to `true`, Mixpanel will not automatically update the &#34;Last Seen&#34; time property for the user profile. |
|User ID| (Required) A unique identifier for the user associated with the event. |
|IP Address| The user&#39;s IP address. |
|Override Update Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |
|Created| When the profile was updated. Date type properties are converted to Mixpanel date format `YYYY-MM-DDThh:mm:ss`. |
|Phone Number| The user&#39;s phone number.|
|Last Name| The user&#39;s last name.|
|Email| The user&#39;s email address. |
|First Name| The user&#39;s first name.|
|Full Name| The user&#39;s full name.|
|Do Not Overwrite Existing Property Values (Set Once)| Select this checkbox to prevent the connector from overwriting existing values. |

### Action - Update Profile - Add

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Ignore Last Seen Update|(Optional) If set to `true`, Mixpanel will not automatically update the &#34;Last Seen&#34; time property for the user profile. |
|User ID| (Required) A unique identifier for the user associated with the event. |
|IP Address| The user&#39;s IP address. |
|Override Update Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |
|Add Data|  &lt;ul&gt;&lt;li&gt;Specify a number to add a numerical amount to their existing value.&lt;/li&gt;&lt;li&gt;Decrement values by providing a negative amount.&lt;/li&gt;&lt;li&gt;Properties with empty values are skipped and not included.&lt;/li&gt;&lt;/ul&gt; |

### Action - Update Profile - Append

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Ignore Last Seen Update| (Optional) If set to `true`, Mixpanel will not automatically update the &#34;Last Seen&#34; time property for the user profile.|
|User ID| (Required) A unique identifier for the user associated with the event. |
|IP Address| The user&#39;s IP address. |
|Override Update Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |
|Append Data|  &lt;ul&gt;&lt;li&gt;Specify properties to append a value to their existing list of values.&lt;/li&gt;&lt;li&gt;Appending to a property that doesn&#39;t exist produces a new list with one element.&lt;/li&gt;&lt;li&gt;Properties with empty values are skipped and not included.&lt;/li&gt;&lt;/ul&gt; |

### Action - Update Profile - Union

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Ignore Last Seen Update| (Optional) If set to `true`, Mixpanel will not automatically update the &#34;Last Seen&#34; time property for the user profile.|
|User ID| (Required) A unique identifier for the user associated with the event. |
|IP Address| The user&#39;s IP address. |
|Override Update Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |
|Union Data|  &lt;ul&gt;&lt;li&gt;Specify properties to merge their values with the existing list on the user profile.&lt;/li&gt;&lt;li&gt;Properties must be of Array type in Data Layer.&lt;/li&gt;&lt;li&gt;Properties with empty values are skipped and not included.&lt;/li&gt;&lt;li&gt;Duplicate values are ignored.&lt;/li&gt;&lt;/ul&gt; |

### Action - Update Profile - Unset

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Ignore Last Seen Update|(Optional) If set to `true`, Mixpanel will not automatically update the &#34;Last Seen&#34; time property for the user profile.|
|User ID| (Required) A unique identifier for the user associated with the event. |
|IP Address| The user&#39;s IP address. |
|Override Update Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |
|Unset Data|  &lt;ul&gt;&lt;li&gt;Specify properties to permanently remove them and their values from a user profile.&lt;/li&gt;&lt;li&gt;Supports Array type in Data Layer.&lt;/li&gt;&lt;/ul&gt; |

### Action - Update Profile - Delete

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Ignore Last Seen Update| (Optional) If set to `true`, Mixpanel will not automatically update the &#34;Last Seen&#34; time property for the user profile.|
|User ID| (Required) A unique identifier for the user associated with the event. |
|IP Address| The user&#39;s IP address. |
|Override Update Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |

### Action - Update Profile - Track Revenue

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Ignore Last Seen Update|(Optional) If set to `true`, Mixpanel will not automatically update the &#34;Last Seen&#34; time property for the user profile.|
|User ID| (Required) A unique identifier for the user associated with the event. |
|IP Address| The user&#39;s IP address. |
|Override Update Time| Not Recommended. Override automatic event timestamp with custom value (epoch time format, UTC). |
|Transaction Amount| (Required) The amount of the transaction.|
|Transaction Time| (Required) The time of the transaction. Date type properties are converted to Mixpanel date format &#39;YYYY-MM-DDThh:mm:ss&#39;|

### Action - Create Alias

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Original User ID|  &lt;ul&gt;&lt;li&gt;Previously set identifier for a user.&lt;/li&gt;&lt;li&gt;Typically a temporary generated ID before a better user ID becomes available (example: user&#39;s email after sign up)&lt;/li&gt;&lt;/ul&gt; |
|New Alias User ID|  &lt;ul&gt;&lt;li&gt;New ID to map to original ID.&lt;/li&gt;&lt;li&gt;Typically an alias is set immediately after user signs up and all subsequent events and updates utilize the new alias ID.&lt;/li&gt;&lt;li&gt;For more information, see [Mixpanel: Using Mixpanel Alias](https://mixpanel.com/docs/integration-libraries/using-mixpanel-alias)&lt;/li&gt;&lt;/ul&gt;. |
