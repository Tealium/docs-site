---
title: Matomo Tag Setup Guide
description: This article describes how to set up the Matomo tag.
url: https://docs.tealium.com/client-side-tags/matomo-tag/
---
Matomo, formerly known as Piwik, is a downloadable, free (GPL licensed) web analytics software platform that provides detailed reports on your website and its visitors.

## Tag tips

Use mappings to do the following: 

* Set up event triggers
* Map event-specific parameters to event names
* Dynamically override standard config values
* Dynamically override e-commerce extension values

If `eventCategory` and `eventAction` are populated, `trackEvent` is called automatically.

Configure your `Goal Index` and `Custom Dimension` values in the **Event-specific Parameters** tab.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Tracker URL**: Found in the Matomo account and is typically the domain name.
* **Site ID**: A Site ID found in Matomo.
* **Track Subdomains**: To record users across the main domain and any of its subdomains, Matomo shares the cookies across all subdomains. If one user visits `x.mydomain.com` and `y.mydomain.com`, they will be counted as one unique visitor.
* **Send Page View**: By default, Page View events are automatically recorded for each page on your site. If you don’t want the snippet to send a Page View event to Matomo, set this option to `false`.
* **Prepend Site Domain**: When set to `True`, the site domain is prepended to the page name to provide an overview of traffic by subdomain. For example, the `About` page on `blog.mydomain.com` is recorded as `blog / About`.
* **Set Alias URLs**: Found in the Matomo account and is typically the domain name.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard Parameters

| Variable | Description |
|:---------|:------------|
| Tracker URL (`tracker_url`) | String |
| Site ID (`site_id`)  | String |
| Track Subdomains (`track_subdomains`)  | Boolean |
| Send Page View (`send_page_view`)  | Boolean |
| Prepend Site Domain (`prepend_site_domain`)  | Boolean |
| Set Alias Urls (`set_alias_urls`)  | Boolean |
| Alias URLs (`alias_urls`)  | String |
| User ID (`user_id`)  | String |
| User entered search words (`searchKeyword`)  | String |
| Category name of return search page (`searchCategory`)  | String |
| Number of return search results (`searchResultsCount`)  | String |
| The link URL that a user clicked on (`linkURL`)  | String |
| Description of clicked on link (`linkType`)  | String |

### Goal Index

| Variable | Description |
|:---------|:------------|
| Goal Index (`goal_index`)  | Number |

### Standard Events Parameters

| Variable | Description |
|:---------|:------------|
| Event Category (`eventCategory`)  | String |
| Event Action (`eventAction`)  | String |
| Event Name (`eventName`)  | String |
| Event Value (`eventValue`)  | Number |

### E-Commerce Parameters

| Variable | Description |
|:---------|:------------|
| List of SKUs (`product_sku`)&lt;br&gt;(Overrides `_csku`) | Array of Strings |
| List of Names (`product_name`)&lt;br&gt;(Overrides `_cprodname`)  | Array of Strings |
| List of Categories (`item_category`)&lt;br&gt;(Overrides `_ccat`)  | Array of Strings/Arrays |
| List of Prices (`product_unit_price`)&lt;br&gt;(Overrides `_cprice`)  | Array of Numbers |
| List of Quantities (`product_quantity`)&lt;br&gt;(Overrides `_cquan`)  | Array of Numbers |
| Order Discounts (`product_discount`)  | Number or Boolean |
| Order ID (`order_id`)&lt;br&gt;(Overrides `_corder`)  | String |
| Order Subtotal (`grand_total`)&lt;br&gt;(Overrides `_csubtotal`)  | Number |
| Order Total (`order_total`)&lt;br&gt;(Overrides `_ctotal`)  | Number |
| Tax Amount (`order_tax`)&lt;br&gt;(Overrides `_ctax`)  | Number |
| Shipping Amount (`order_shipping`)&lt;br&gt;(Overrides `_cship`)  | Number |

### Action Dimensions

| Variable | Description |
|:---------|:------------|
| Custom Dimension Index (`custom_dimension_index`)  | Number |
| Custom Dimension Value (`custom_dimension_value`)  | String |

### Events
For inforamtion on mapping events, see [Add an event mapping]().

| Variable | Description |
|:---------|:------------|
| Product View | `productView` |
| Category View | `ctegoryViews` |
| Add To Cart | `addToCart` |
| Remove From Cart | `removeFromCart` |
| Purchase | `purchase` |
| User Logged Out | `resetUserId` |&#34;
| Track Goal | `trackGoal` |
| Site Search | `trackSiteSearch` |
| Track Link | `trackLink` |
| Set Custom Dimension | `setCustomDimension` |
| Delete Custom Dimension | `deleteCustomDimension` |

### Event-specific Parameters
For information on mapping events, see [Add an event mapping]().

| Variable | Description |
|:---------|:------------|
| Product View | `productView` |
| Category View | `ctegoryViews` |
| Add To Cart | `addToCart` |
| Remove From Cart | `removeFromCart` |
| Purchase | `purchase` |
| User Logged Out | `resetUserId` |
| Track Goal | `trackGoal` |
| Site Search | `trackSiteSearch` |
| Track Link | `trackLink` |
| Set Custom Dimension | `setCustomDimension` |
| Delete Custom Dimension | `deleteCustomDimension` |
| Track Event | `trackEvent` |

    