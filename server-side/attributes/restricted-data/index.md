---
title: About restricted data
description: Restricted data is a property to identify attributes that contain sensitive data.
url: https://docs.tealium.com/server-side/attributes/restricted-data/
---
## What is restricted data?

Restricted data refers to any attribute containing data that is:

* ✔ private or personal
* ✔ protected by privacy laws
* ✔ subject to controlled access

By default, attributes are not restricted and may flow through to a variety of destinations. Attributes have a setting called **Restricted Data** that prevents them from being included in some processes that send data out of the Customer Data Hub. Attribute enrichments are not affected.

## Identifying restricted attributes

You can use the filter in the left navigation panel to select the type of attributes you want to list. To identify attributes with restricted data, click the **Restricted Data** checkbox.

![](/images/server-side/restricted-attributes-filter.png)

When editing attribute details, the **Restricted Data** field displays in the properties section where applicable. Check this box if you want to mark the attribute as restricted data.

![](/images/server-side/restricted-attributes-checkbox-example.png)

## Restricted attributes

Restricted data settings apply to the following services:

* **EventStore and EventDB**  
By default, restricted attributes are omitted from event feeds. This behavior can be changed in the settings for each feed.  Connectors that use an event feed as a data source always receive restricted attributes, regardless of how the event feed is configured. 
* **Data Layer Enrichment**  
By default, restricted attributes are omitted from the visitor attributes returned to the on-page data layer with data layer enrichment with AudienceStream. When the Tealium Collect tag requests the latest visitor profile, AudienceStream returns attributes that are not restricted. This behavior cannot be changed.

Restricted data settings do not apply to the following services:

* **AudienceStore and AudienceDB**  
By default, restricted attributes are always included, whether they are sent to AudienceDB or exported using the AudienceStore connector. This behavior cannot be changed.
* **Connectors (including Webhook)**  
By default, restricted attributes are always included, whether you are sending them to the vendor through mappings or as part of the visitor profile. This behavior cannot be changed.
A warning message appears if your connector request contains one or more restricted attributes.

## Summary

* Marking an attribute as restricted protects it from being sent to select Tealium services.
* EventStore, EventDB, and Data Layer Enrichment services honor restricted data.
* AudienceStore, AudienceDB, and Connectors do not honor restricted data.
* Restricted attributes are available to all enrichments.
