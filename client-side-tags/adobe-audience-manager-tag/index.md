---
title: Adobe Audience Manager Tag Setup Guide
description: This article describes how to set up the Adobe Audience Manager tag in your iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/adobe-audience-manager-tag/
---
## Tag Tips

* Select **On** under **Use E-Commerce Variables** to add the Order and Customer E-Commerce data to the `c_` data
* Use the "Custom c_ Object" mapping to send your own object or additional objects with `c_` data
* Current Library Version: 9.5

## Tag Configuration

First, go to Tealium's tag marketplace and add the Adobe Audience Manager tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Visitor Service Namespace**: This is the same as your Adobe Org ID/Experience Cloud ID
* **Partner Name**: Provided by Audience Management
* **Use E-Commerce Variables**:

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable                                                                   | Description         |
|:---------------------------------------------------------------------------|:--------------------|
| Visitor Service Namespace                                                  | (`namespace`)         |
| Partner Name                                                               | (`partner`)           |
| Use E-Commerce Variables                                                   | (`use_ecommerce`)     |
| Container ID                                                               | (`containerNSID`)     |
| Data Partner ID                                                            | (`declaredId.dpid`)   |
| Unique User ID                                                             | (`declaredId.dpuuid`) |
| Defer Requests Until Page Load (`delayAllUntilWindowLoad`)                   | [Boolean]           |
| Disable UUID Cookie (`disableDeclaredUUIDCookie`)                            | [Boolean]           |
| Prevent Destination Publishing IFRAME (`disableDestinationPublishingIframe`) | [Boolean]           |
| Disable ID Synchronization (`disableIDSyncs`)                                | [Boolean]           |
| Enable Error Reporting (`enableErrorReporting`)                              | [Boolean]           |
| Enable Logging (`enableLogging`)                                             | [Boolean]           |
| Enable URL Destinations (`enableUrlDestinations`)                            | [Boolean]           |
| Enable Cookie Destinations (`enableCookieDestinations`)                      | [Boolean]           |
| Enable Akamai for HTTPS (`iframeAkamaiHTTPS`)                                | [Boolean]           |
| Remove Finished Scripts and Callbacks (`removeFinishedScriptsAndCallbacks`)   | [Boolean]           |
| Key Mappings Object (`mappings`)                                             | [Object]            |
| Cookie Name                                                                | (`uuidCookie.name`)   |
| Cookie Lifetime in Days                                                    | (`uuidCookie.days`)   |
| Cookie Path                                                                | (`uuidCookie.path`)   |
| Cookie Domain                                                              | (`uuidCookie.domain`) |
| Send Over HTTPS (`uuidCookie.secure`)                                        | [Boolean]           |

### Basic `c_` Variables

| Variable             | Description              |
|:---------------------|:-------------------------|
| Ad ID                | (`c.ad_id`)                |
| Content Author       | (`c.content_author`)       |
| Content Title        | (`c.content_title`)        |
| Content Publish Date | (`c.content_publish_date`) |
| Category ID          | (`c.category_id`)          |
| Category Name        | (`c.category_name`)        |
| Page Name            | (`c.page_name`)            |
| Page Number          | (`c.page_number`)          |
| Previous Page Name   | (`c.previous_page_name`)   |
| Search Category      | (`c.search_category`)      |
| Search Keyword       | (`c.search_keyword`)       |
| Search Results       | (`c.search_results`)       |
| Site Section         | (`c.site_section`)         |
| Sort By              | (`c.sort_by`)              |
| Sort Order           | (`c.sort_order`)           |
| Custom `c_` Variable   | (`c.custom`)               |
| Custom `c_` Object     | (`cobject.custom`)         |

### Basic `d_` Variables

| Variable                               | Description  |
|:---------------------------------------|:-------------|
| Caller                                 | (`d.caller`)   |
| Javascript Callback Function           | (`d.cb`)       |
| Data Provider ID                       | (`s`) (`d.cid`)  |
| Integration Code and User ID           | (`d.cid_ic`)   |
| Trait and Segment Return Type          | (`d.cts`)      |
| Return URL Destination                 | (`d.dst`)      |
| JSON Return Version                    | (`d.jsonv`)    |
| Name Space ID                          | (`d.nsid`)     |
| Return JSON                            | (`d.rtbd`)     |
| Score ID                               | (`d.sid`)      |
| Trait Data Source                      | (`d.tdpid`)    |
| Trait Data Source via Integration Code | (`d.tdpid_ic`) |
| Unique User ID                         | (`d.uuid`)     |
| Custom `_d` Variable                     | (`d.custom`)   |

### Custom `h_` and `p_` Variables

| Variable           | Description |
|:-------------------|:------------|
| Custom `_h` Variable | (`h.custom`)  |
| Custom `_p` Variable | (`p.custom`)  |

### E-Commerce

| Variable           | Description                             |
|:-------------------|:----------------------------------------|
| Order ID           | (`order_id`) (Overrides `_corder`)          |
| Order Total        | (`order_total`) (Overrides `_ctotal`)       |
| Sub Total          | (`order_subtotal`) (Overrides `_csubtotal`) |
| Shipping Amount    | (`order_shipping`) (Overrides `_cship`)     |
| Tax Amount         | (`order_tax`) (Overrides `_ctax`)           |
| Store              | (`order_store`) (Overrides `_cstore`)       |
| Currency           | (`order_currency`) (Overrides `_ccurrency`) |
| Promo Code         | (`order_coupon_code`) (Overrides `_cpromo`) |
| Cart or Order Type | (`order_type`) (Overrides `_ctype`)         |
