---
title: SiteCatalyst Tag Setup Guide
description: SiteCatalyst is Adobe’s software as a service application offering Web Analytics to tracking how visitors interact with your site.
url: https://docs.tealium.com/client-side-tags/sitecatalyst-tag/
---
## Tag Specifications and Requirements

### Specifications

**Name**: SiteCatalyst

**Vendor**: Adobe

**Type**: Analytics

### Required

**Services**: SiteCatalyst Account

**Configurations**:

* S-Code Version
* Report Suite
* Server
* Server Secure
* Namespace
* Internal Link Filters

## Tag Configuration in Tealium iQ

### 1. Add the Tag

Tealium iQ&#39;s Tag marketplace offers a wide variety of Tags. To learn more, see [here]().

### 2. Configure the Tag

Here&#39;s a list of configurations for the SiteCatalyst Tag. You can find the values for the configurations in the `s_code` file provided to you by SiteCatalyst.

![](/images/client-side-tags/no-title-1081i487822e9a007e208.png)

![](/images/client-side-tags/no-title-1080if5f98fdd321f2089.png)

1. **Title**: (Required) Enter a descriptive title to identify the Tag.
1. **S-Code Version**: (Required) Select the version of SiteCatalyst you want to use. Versions H20 through H27 are supported.
1. **Report Suite**: (Required) Enter the name of your SiteCatalyst report suite. You can find this value as `s.account` in your `s_code.js` file.
1. **Server**: (Required) Enter the data collection server information. You can find this value as `s.trackingServer` in your `s_code.js`. file.
1. **Server Secure**: (Required) Enter the secure (`https`) data collection server information. You can find this values as `s.trackingServerSecure` in your `s_code.js` file.
1. **Namespace**: (Required) You can find this value as `s.namespace` in your `s_code.js` file.
1. **Auto Link Tracking**: (Optional) The default selection is `Yes` and is the recommended selection. If you set this to `No`, you will have to duplicate all the automatic link tracking with Tealium&#39;s [link tracking extensions]().
You may still use Tealium&#39;s link tracking extensions for custom tracking even if you select `Yes`.

1. **Download Types**: (Optional) In this field list the types of file extensions that, when downloaded, you want to track as download links. For example, you could enter `zip`,`exe`,`wav`,`mp3`,`mov`,`mpg`,`avi`,`wmv`,`pdf`,`doc`,`docx`,`xls`,`xlsx`,`ppt`,`pptx`
1. **Internal Link Filters**: (Optional) You must enter a value here, otherwise all link clicks will be reported as exit links in your SiteCatalyst report. To properly track link clicks that trigger a JavaScript activity such as a modal popping up you need to make certain you include `javascript` in the field. You can find these values as `s.linkInternalFilters` in your `s_code.js` file.
1. **Currency Code**: (Optional) Enter the three-letter currency code of the currency you want your revenue data in. The default value is `USD`. This is the default currency that SiteCatalyst will understand revenue data in your report suite. If a transaction occurs in another currency on your site, SiteCatalyst can do the currency conversion for you. You can find this value in the `s.currencyCode` in your `s_code.js` file.
1. **Use Dynamic Account**: (Optional) Set to `Yes` when you want to send data to different report suites based on the domain.
1. **Dynamic Acct List**: (Optional) Enter the list of report suites and their corresponding domains to dynamically set the report suite based on domain. For example: `testreportsuite=testing.example.com,qa.example.com;prodreportsuite=www.example.com`
1. **S-Object Name**: (Required) Keep this set at the default `s` unless you plan to run this tag alongside a completely separate implementation.
1. **Clear Vars**: (Optional) Set this to `Yes` to clears props, eVars, and events set in the global `s` object after each tracking request.
1. **Partner**: (Optional) Enter your partner ID here. This is only required to use Adobe AudienceManager, so leave it blank if you do not use Adobe AudienceManager. You can find the partner ID value in the `DIL.create` call.

**Tip**: Place this Tag near the top of the list in the Tags tab to ensure that it loads as soon as possible. The sooner the Tag loads, the sooner it captures visitors&#39; activity.

### 3. Apply Load Rules

[Load Rules]() determine when and where to load an instance of this Tag. The **Display on All Pages** rule is the default load rule. To load this Tag on a specific page, create a new load rule with the relevant conditions.

**Note**: Since SiteCatalyst is an analytics Tag you will want it to load across your entire site, so we recommend leaving the default **Load on all Pages** selection as is.

### 4. Set up Mappings

[Mapping](/iq-tag-management/data-mappings/manage/) is the process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor Tag.

To properly format the Products String and send revenue data to your SiteCatalyst report suite, you must add and configure the [E-Commerce Extension]() in your Tealium iQ profile.

 As of the latest template update, linkTrackVars and linkTrackEvents are set automatically. You may have to update your template to the latest and greatest to take advantage of this. 

### Standard Mappings

* **pageName**
* **channel**
* **server**
* **hier1 through hier3**
* **VisitorID**
* **s\_account**: Map to this destination to dynamically set the account configuration.

### Events

You can use mapping to trigger the following events events:

* **prodView**
* **scOpen**
* **scAdd**
* **scRemove**
* **scView**
* **scCheckout**
* **purchase**
* **event1 through event100**

For more information on Event tracking in SiteCatalyst through Tealium iQ, click [here]().

#### Product-level Events

Mapping here will add these events to the Products String.

* `PRODUCTS_event1` through `PRODUCTS_event100`

#### Props

Map data sources to these destinations to send them to SiteCatalyst as props.

* `prop1` through `prop75`

#### eVars

Map data sources to these destinations to send them to SiteCatalyst as eVars.

* `eVar1` through `eVar75`

#### Merchandising eVars

Map data sources to these destination to send them to SiteCatalyst as merchandising eVars.

* `PRODUCTS_eVar1` through `PRODUCTS_eVAr75`

#### Commerce

Map data sources to these destinations to send commerce data to SiteCatalyst. Much of this data is sent automatically by the E-Commerce Extension.

* **purchaseID**
* **transactionID**
* **state**
* **zip**
* **Product IDs (`PRDOCUTS_id`) \{Array\}**
* **Product Categories (`PRODUCTS_category`) \{Array\}**
* **Product Quantities (`PRODUCTS_quantity`) \{Array\}**
* **Product Prices (`PRODUCTS_price`) \{Array\}**

#### Other

Map data sources to the destinations below to send list data and the doneAction parameter.

* Link Tracking - doneAction param (H25 only)
* list1 through list3


## Vendor Documentation

* [General website](http://www.adobe.com/products/sitecatalyst.html)
* [Support site](http://helpx.adobe.com/sitecatalyst.html)
