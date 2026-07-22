---
title: Connectors
description: This document explains connectors in AudienceStream.
url: https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/connectors/
---
![](https://docs.tealium.com/images/server-side/getting-started-audiencestream-connectors-icon.png)

A connector is an integration between Tealium and another vendor that is used to transmit data. A connector contains actions that represent the vendor's supported APIs. In AudienceStream connectors, audiences (visitor profiles) are used as the source of data to transmit.

Here's how it works:

* **Connectors**  
A connector contains the credentials needed to connect to your vendor, such as an account ID, username/password, or API key, and trigger the API actions that they support.
* **Actions**  
An action is a vendor operation or API method, like triggering an email, building a custom audience, or tracking a conversion. The configuration of an action determines which audiences and attributes the vendor will receive.
* **Audiences**  
Each action is fueled by an audience. Every time a customer joins or leave an audience, it can trigger the connector action that it's configured for.
* **Data Mappings**  
Data mappings are configured in the action to translate visit/visitor attributes into the data parameters expected by the vendor.

Let's give it a try. Click **Next** to set up and configure a connector. You will soon see all of your work for this lesson in action.