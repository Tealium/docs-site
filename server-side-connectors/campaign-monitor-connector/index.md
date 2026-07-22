---
title: Campaign Monitor Connector Setup Guide
description: This article describes how to set up the Campaign Monitor connector.
url: https://docs.tealium.com/server-side-connectors/campaign-monitor-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Smart Email | ✓ | ✗ |
| Add or Update Subscriber | ✓ | ✗ |
| Delete Subscriber | ✓ | ✗ |
| Unsubscribe Subscriber | ✓ | ✗ |
| Update a Subscriber | ✓ | ✗ |

## Configure Settings

Navigate to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **API Key**  
 <br>An API key is required to interact with Campaign Monitor accounts. For more information, see <a href="http://help.campaignmonitor.com/topic.aspx?t=206" target="_blank">Where can I find my API key?</a>
* **Client Name**  
 <br>A name is required to manage the client account.

## Actions

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Smart Email

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Smart Email | Select smart transactional email to send. |

### Add or Update Subscriber

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Subscriber List | Select list to add subscriber to |
| Subscriber Email Address | (Required)  |
| Subscriber Name | (Required)  |
| Resubscribe Subscriber |  |
| Restart Subscriber Auto Responders |  |

### Delete Subscriber

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Subscriber List | Select list to delete subscriber from. |
| Subscriber Email | Provide email to delete from selected list (see: <a href="http://help.campaignmonitor.com/topic.aspx?t=140#remove-options" target="_blank">Delete vs Unsubscribe</a>). Deleted email is not added to the suppression list<br>Recommended: use unsubscribe action if someone has asked to be removed, and delete action if you have chosen to remove them for any reason. |

### Unsubscribe Subscriber

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Subscriber List | Select list to unsubscribe subscriber from. |
| Subscriber Email | Provide email to unsubscribe from selected list and add to the suppression list. Email will also be unsubscribed from any other lists for your client, except for lists where the unsubscribe setting has been changed. |

### Update a Subscriber

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Subscriber List | Select list to update subscriber |
| Subscriber Email Address | (Required)  |
| Subscriber Name | (Required)  |
| Subscriber Mobile Number |  |
| Subscriber Custom Fields | When clear is selected, you can remove an attribute value by selecting **Clear** and inputting the value into the value field, or selecting **Clear** and inputting `Clear` into the value field and inputting the Attribute Name you want to clear its value. To clear the value of a custom field, pass a parameter of Clear with a value of true along with the custom field name/value. To remove a specific Multi-Valued Select Many option, pass the option name in the Value field along with the Clear: true parameter. To clear all values of a Multi-Valued Select Many field, pass an empty Value along with the Clear: true parameter. Alternatively, Date type custom fields may be still cleared by passing in a value of “0000-00-00”. Available fields are determined by selected Subscriber List (see: <a href="http://help.campaignmonitor.com/topic.aspx?t=154" target="_blank">How do I create and use custom fields?</a>)<br>Date attributes are automatically converted to YYYY-MM-DD format |
| Consent To Track | Whether the subscriber has given permission to have their email opens and clicks tracked. This value applies to all subscribers with the same email address, within the same client. If you pass a value of unchanged for an email address, and that address doesn't currently exist in the client, or has no existing value for ConsentToTrack, it is assumed the subscriber has given consent. |
| Consent To Send SMS | An optional parameter to indicate if consent has been granted by the subscriber to receive SMS. Consent to send SMS for a subscriber is only recorded when a mobile number is supplied. It can also be used to indicate consent is not granted. If this parameter is omitted it will leave any existing consent preference unchanged. |
| Resubscribe | If the subscriber is in an inactive state or has previously been unsubscribed or added to the suppression list and you specify the Resubscribe input value as true, they will be re-added to the list. Therefore, this method should be used with caution and only where suitable. If Resubscribe is specified as false, the subscriber will not be re-added to the active list. |
| Restart Subscription Based Autoresponders | If you specify the RestartSubscriptionBasedAutoresponders input value as true, any sequences will be restarted. RestartSubscriptionBasedAutoresponders only affects resubscribing subscribers, and will default to false if omitted. |