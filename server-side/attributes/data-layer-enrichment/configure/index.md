---
title: Configure Data Layer Enrichment in Tag Management
description: Configure the Customer Data Platform (CDP) profile that provides attributes for Data Layer Enrichment in Tag Management.
url: https://docs.tealium.com/server-side/attributes/data-layer-enrichment/configure/
---
Use the publish configuration settings in Tag Management to select the Customer Data Platform (CDP) profile that provides visit and visitor attributes to your data layer. For more information about publish configuration, see [Publish configuration](https://docs.tealium.com/publish-configuration/).


<blockquote>
This configuration does not enable or disable server-side data layer enrichment. To control access to the Data Layer Enrichment API and Profile Definition API, see [Enable server-side Data Layer Enrichment](https://docs.tealium.com/enable-data-layer-enrichment/).
</blockquote>


## How it works

Data layer enrichment in Tag Management links your iQ profile to a CDP profile. The selected CDP profile provides the visit and visitor attributes that Tag Management imports into your data layer.

By default, Tag Management uses the CDP profile named `main`. You can select a different profile in the publish configuration settings.

## Select a CDP profile

1. In the admin menu, click **Configure Publish Settings**. The **Publish Configuration** dialog appears.
1. On the **General Publishing** tab, scroll to the bottom of the **Implementation** section.
1. Select a CDP profile from **Data Layer Enrichment Profile**.
1. Click **Apply**.
1. Save and publish your changes to the **Prod** environment.

![](https://docs.tealium.com/images/server-side/whiteui-datalayerenrichment-selectdatalayerenrichmentprofile.png)
