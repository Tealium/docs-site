---
title: Integrate with Tag Management
description: This article describes the process of publishing on the server side of the Tealium platform.
url: https://docs.tealium.com/server-side/save-publish/with-tealium-iq/
---
## Import data layer variables

Customer Data Hub can make use of the variables from Tag Management. To do so the Tag Management profile must be published to the Prod environment to make these variables appear as attributes within Customer Data Hub.

## Data layer enrichment

Tag Management can make use of Customer Data Platform (CDP) attributes through a feature called [data layer enrichment](https://docs.tealium.com/about-data-layer-enrichment/). To make your visitor attributes available in Tag Management, your server-side configuration must be published. These attributes can then be used like any other data layer variable.

By default, a Tag Management profile will attempt to import visitor attributes from the corresponding server-side profile. For example, the Tag Management profile `tealium/main` will read from the server-side profile `tealium/main`.

However, it's possible to import visitor attributes from a different server-side profile.

To import visitor attributes from a different server-side profile: 

1. In the admin menu, click **Configure Publish Settings**. The **Publish Configuration** dialog appears.
* In the **Implementation** section, select a server-side profile from the **Data Layer Enrichment Profile** list.

![](https://docs.tealium.com/images/server-side/no-title-1711i6d0b9fae5a4e3679.png)
