---
title: Data Connect events
description: This article describes the Data Connect events format.
url: https://docs.tealium.com/server-side/data-connect/events/
---
Data Connect captures real-time updates from your Workato integrations. Use Workato recipes to configure event triggers and use the Tealium Events app to map your integration data to Tealium event attributes. 

Data Connect sends events in a JSON format to Tealium using the data mapping you configure in your recipe. For example, you can configure a Salesforce integration to capture the customer field `customerStatusTypeID` whenever a contact object is updated and send the value as a visitor attribute to AudienceStream. Using the Tealium Event integration, you can map the  Salesforce fields `customerID` and `customerStatusTypeID` to the Tealium event attributes `customer_id` and `customer_status`, respectively. 

When Salesforce captures the customer field `customerStatusTypeID`, your Workato recipe will trigger an event and send the following event data to Tealium:

```json
{
  tealium_event   : &#34;offline_account_update&#34;,
  customer_id     : &#34;123456&#34;,
  customer_status : &#34;Active&#34;
}
```

The tealium_event name `offline_account_update` can be customized for each integration.

To capture this event in Tealium AudienceStream, create a visitor attribute and enrichment to store `customer_status` whenever this event occurs.

