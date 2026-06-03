---
title: Visitor Stitching Visitor ID
description: The visitor ID attribute is used to identify customers using a value that is guaranteed to be unique to each customer.
url: https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/visitor-stitching-visitor-id/
---
The value is usually set during a qualifying event, one that would only occur when a customer provides a reliable means of identification, such as registering or completing a purchase.

## How it works

![](/images/server-side/getting-started-audiencestream-visitor-id.png)

A simple example of a visitor ID attribute is email address (or email hash). This is typically a reliable way to uniquely identify a customer, especially when it&#39;s associated with a qualifying event. To accurately perform identity resolution with an email address the following is needed:

* **Event Attribute (String) - email_address**  
An email address must be part of the data collection as an event attribute.
* **Qualifying Event - user_register**  
Not all events that send an email address value should be used for identity resolution. Only specific events that have a high likelihood of accurately identifying the customer should be used.
* **Visitor Attribute (String) - Email Address**  
A visitor string attribute for the email address will associate it with the customer profile for any event that sends the corresponding event attribute.
* **Visitor ID - Email Address**  
Identity resolution only occurs when Email Address is set and a qualifying event has occurred.

Click **Next** to see how to configure this visitor ID attribute.