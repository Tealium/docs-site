---
title: Data sources for iQ Tag Management
description: This article explains how to use data sources with existing iQ Tag Management accounts.
url: https://docs.tealium.com/server-side/data-sources/data-sources-for-iq-tag-management/
---
## How data sources work with iQ Tag Management

A data source requires an installation of Tealium Collect. For iQ Tag Management accounts, where you have already installed Tealium on your website or mobile app, you will install either the Tealium Collect tag or the Tealium Collect module for mobile.

To connect a data source to one of these Tealium Collect installations the **data source key** must be set--either in the Tealium Collect tag configuration or in the mobile code.

If you haven&#39;t already, [create a data source]() for your iQ Tag Management account, copy the unique data source key-value, then proceed with one of the following methods:

* [Single-site profiles](#single-site-profiles)
* [Multi-site profiles](#multi-site-profiles) 
* [Mobile profile with the Tag Management module and Tealium Collect tag](#tag-management-module-with-the-tealium-collect-tag)
* [Mobile profile with Tealium Collect module](#tealium-collect-module)

## Single-site profiles

A single-site profile has been deployed to one web property. To connect a profile to a data source you must have an active Tealium Collect tag.

To add the data source key to the Tealium Collect tag:

1. In iQ Tag Management, add the Tealium Collect tag.  
      If you already have the Tealium Collect tag [check that you have the most recent version]()
1. Paste the data source key into the **Data Source Key** field in the tag configuration, as seen here:  
      ![](/images/server-side/iq-data-source-key.jpg)
1. Save and publish your changes.

## Multi-site profiles

A multi-site profile has been deployed to more than one web property (for instance, more than one domain) and is configured to set values dynamically based on the site.

To get started you will need to create an iQ Tag Management data source for each web property that is serviced by the client-side profile. To connect those data sources to each site serviced by the client-side profile use a **Lookup Table** extension to  set the data layer variable `tealium_datasource` based on the site name or domain. This will ensure that the Tealium Collect tag uses the correct data source key.

A data mapping is not needed because the Tealium Collect tag uses the `tealium_datasource` variable automatically.

To add multiple data source keys to the Tealium Collect tag:

1. Add a Lookup Table extension.
1. Set the **Lookup Value In** to `domain` (or another variable that distinguishes your sites from one another).
1. Set the **Destination** to `tealium_datasource` (click the **&#43;** button to add it if it doesn&#39;t already exist).
1. Enter an expected value for each site in the **Lookup Match** field.
1. Enter the matching data source key in the **Output** field.
1. Save and publish your changes.

The Tealium Collect tag will automatically include the `tealium_datasource` attribute in its tracking call. The value will be dynamically set based on the output of the Lookup Table.

![](/images/server-side/datasourcekey-lookup-table.jpg)

## Mobile profiles

A mobile profile is used for an installation of Tealium for iOS or Tealium for Android. To connect a mobile client-side profile to a server-side data source for Android or iOS you must enable either the Tealium Collect module or the Tag Management module with an active Tealium Collect tag.

### Tag Management module with the Tealium Collect tag

A client-side profile for mobile that uses the native Tag Management module with the Tealium Collect tag will follow the same process for [single-site profiles](#single-site-profiles).

### Tealium Collect module

A client-side profile for mobile that uses the native Tealium Collect module must update the mobile library code to include the data source key in the initialization. Follow the installation instructions for your chosen mobile data Source platform to make this change.

As an alternative, you can disable the Tealium Collect module, enable the Tag Management module, add the Tealium Collect tag, then follow the same process for [single-site profiles](#single-site-profiles).
