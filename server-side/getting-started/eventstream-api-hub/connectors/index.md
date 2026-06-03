---
title: Connectors
description: A connector is an integration between Tealium and another vendor that is used to transmit data. A connector contains actions that represent the vendor's supported APIs.
url: https://docs.tealium.com/server-side/getting-started/eventstream-api-hub/connectors/
---![](/images/server-side/as-getting-started-connectors.jpg)

Here&#39;s how it works:

* **Connectors**  
A connector contains the credentials needed to connect to your vendor and trigger the API actions they support, such as an account ID, username/password, or API key.
* **Actions**  
An action is a vendor operation or API method, such as triggering an email, building a custom audience, or tracking purchase events. The configuration of an action determines which events and attributes the vendor will receive.
* **Event feeds**  
Each action is triggered by an event feed. Every time the event feed receives an event, it will trigger the connector action that it&#39;s used for.
* **Data mappings**  
Data mappings are configured in the action to translate event attributes into the data parameters expected by the vendor.

Let&#39;s give it a try! Go to the next step to set up and configure a connector. You will soon see all of your work for this lesson in action.
