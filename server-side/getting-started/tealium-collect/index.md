---
title: Install Tealium Collect
description: Learn how to install Tealium Collect.
url: https://docs.tealium.com/server-side/getting-started/tealium-collect/
---
Tealium Collect is the primary method for server-side data collection  for websites, mobile apps, and server applications. Tealium Collect can be installed in many ways, depending on the platform.

## Web and mobile

![](/images/server-side/tag-management-01.png)

For customers with an iQ Tag Management account, use the Tealium Collect tag. Adding this tag to your client-side profile turns your installation of the Tealium Universal Tag into a data source for your server-side profile.

The Tealium Collect tag sends each event tracking call to your server-side profile where the data will be processed into visitor profiles, audiences, cloud-based connectors, and data storage solutions.

Learn [how to set up the Tealium Collect tag in your client-side profile]().


Even if you are not already using a tag manager, we recommend using a basic setup of Tealium iQ Tag Management and the Tealium Collect tag.

For mobile profiles, we recommend using the Tealium Collect module in your app.

Learn more about [installing Tealium Collect directly in your mobile app](/platforms/getting-started-mobile/server-side/).

## Server applications

For other platforms that are not managed through iQ Tag Management, we offer installation libraries for sending data to your server-side profile. 

Popular server app platforms include:

* [Python](/platforms/python/)
* [Node](/platforms/node/)
* [C#](/platforms/csharp/)
* [Java](/platforms/java/)
* [HTTP API](/platforms/http-api/)

## Google Tag Manager

### With Tealium Collect

If you are using Google Tag Manager and are satisfied with your data layer and event tracking, we recommend deploying the Tealium Collect tag for Google Tag Manager. The Tealium Collect tag sends all data processed by Google Tag Manager, including the complete `dataLayer` object, directly to AudienceStream.

Installation components:

* [Tealium Collect for Google Tag Manager](/platforms/google-tag-manager/)

### With Tealium Universal tag

If you prefer to deploy vendors using Google Tag Manager, we recommend deploying the Tealium Universal Tag as a Custom HTML Tag in Google Tag Manager. This approach is also recommended if your Google Tag Manager implementation is not tracking behaviors and data points that are critical to your business, such as conversion funnel activity or ecommerce checkout steps. By deploying the Tealium Universal Tag you can take advantage of the full benefits of iQ Tag Management to fully implement advanced event tracking and supplemental data layer variables.

This approach provides the advantages of deploying iQ Tag Management, as well as the ability to utilize existing event tracking in Google Tag Manager to expedite the installation.

Installation components:

* [Tealium iQ Tag Management](/iq-tag-management/)
* [Custom HTML Tag in Google Tag Manager](https://support.google.com/tagmanager/answer/6107167?hl=en)

