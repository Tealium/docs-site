---
title: Install options for web
description: This article describes the installation options for Tealium AudienceStream CDP.
url: https://docs.tealium.com/server-side/getting-started/audiencestream-cdp/install/
---
This article is for customers that want to install Tealium AudienceStream, but do not already use Tealium iQ Tag Management or Tealium EventStream API Hub.

## Option 1: Tealium Universal Tag &#43; Tealium Collect

If you are not already using a tag manager, we recommend using a basic setup of Tealium iQ Tag Management and the Tealium Collect tag to send data to AudienceStream.

Tealium iQ requires an installation of the Universal Tag (`utag.js`) on all pages of your site and the Tealium Collect tag, which is easily added with a few clicks from the tag marketplace. Additional benefits of this option include access to the [extension marketplace](), for preparing and transforming your data before it&#39;s sent to AudienceStream, and the use of [Web Companion]() and [Tealium Tools]() to validate and extend your installation.

Installation components:

* [Tealium iQ Tag Management]()
* [Tealium Universal Tag (`utag.js`)](/platforms/javascript/install/)
* [Tealium Collect Tag]()

## Option 2: Google Tag Manager &#43; Tealium Collect

If you are using Google Tag Manager and are satisfied with your data layer and event tracking, we recommend deploying the Tealium Collect tag for Google Tag Manager. The Tealium Collect tag sends all data processed by Google Tag Manager, including the complete `dataLayer` object, directly to AudienceStream.

Installation components:

* [Tealium Collect for Google Tag Manager](/platforms/google-tag-manager/)

## Option 3: Google Tag Manager &#43; Tealium Universal Tag

If you prefer (or are required) to deploy vendors using Google Tag Manager, we recommend deploying the Tealium Universal Tag as a Custom HTML Tag in Google Tag Manager. This approach is also recommended if your Google Tag Manager implementation is not tracking behaviors and data points that are critical to your business, such as conversion funnel activity or ecommerce checkout steps. By deploying the Tealium Universal Tag you can take advantage of the full benefits of iQ Tag Management to fully implement advanced event tracking and supplemental data layer variables.

This approach provides the advantages of deploying iQ Tag Management, as well as the ability to utilize existing event tracking in Google Tag Manager to expedite the installation.

Installation components:

* [Tealium iQ Tag Management]()
* [Custom HTML Tag in Google Tag Manager](https://support.google.com/tagmanager/answer/6107167?hl=en)

## Learn more

The following resources are available to help continue your implementation experience:

### Live Events

Regardless of the installation option, you will validate the data flowing into AudienceStream using Tealium [Live Events](). **Live Events** shows incoming data in real-time so that you can evaluate your tracked events and collected data attributes.

### Tealium Education

Explore Tealium’s robust on-demand learning at [education.tealium.com](https://education.tealium.com/) to take advantage of courses to increase your Tealium knowledge and skills, including the [AudienceStream Basic eLearning course](https://education.tealium.com/learn/course/en-as-bsc-elrn).
