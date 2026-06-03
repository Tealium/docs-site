---
title: Integrate with Tealium iQ
description: This article describes the process of publishing on the server side of the Tealium platform.
url: https://docs.tealium.com/server-side/save-publish/with-tealium-iq/
---
## Import data layer variables

Customer Data Hub can make use of the variables from Tealium iQ. To do so the Tealium iQ profile must be published to the Prod environment to make these variables appear as attributes within Customer Data Hub.

## Data layer enrichment

Tealium iQ can make use of AudienceStream attributes through a feature called [data layer enrichment](). To make your visitor attributes available in Tealium iQ, your server-side configuration must be published. These attributes can then be used like any other data layer variable.

By default, a Tealium iQ profile will attempt to import visitor attributes from the corresponding server-side profile. For example, the Tealium iQ profile `tealium/main` will read from the server-side profile `tealium/main`.

However, it&#39;s possible to import visitor attributes from a different server-side profile.

To import visitor attributes from a different server-side profile: 

1. In the admin menu, click **Configure Publish Settings**. The **Publish Configuration** dialog appears.
* In the **Implementation** section, select a server-side profile from the **Data Layer Enrichment Profile** list.

![](/images/server-side/no-title-1711i6d0b9fae5a4e3679.png)
