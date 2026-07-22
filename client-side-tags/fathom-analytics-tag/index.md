---
title: Fathom Analytics Tag Setup Guide
description: This article describes how to set up the Fathom Analytics tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/fathom-analytics-tag/
---
This tag adds the Fathom Analytics script to your site. The script tracks page views, sessions, bounce rate, and other metrics without using cookies or collecting personal data. The script can be customized with various options, such as changing the site ID, ignoring canonical URLs, honoring do-not-track requests, and more.

## Tag tips

* Use mapping to override the standard configuration values dynamically.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Site ID**: The Site ID generated when creating a new site. Displayed in the data-site attribute.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Configuration

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `site_id`  | String | Site ID |

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `url`  | String | URL |
|  `referrer`  | String | Referrer |
|  `event_id`  | String | Event ID |
|  `event_value`  | Number | Event Value |

### HTML attributes

For more information

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `load_option`  | String | Load option. <ul><li>`defer`: Defer loading of the script until after the site loads.</li><li>`async`: Load the script asynchronously.</li></ul> | 
|  `data_auto`  | String | Disable automatic tracking. Available values are `true` and `false`. |
|  `data_canonical`  | String | Ignore canonical URLs. Available values are `true` and `false`. | 
|  `data_excluded_domains`  | String | A comma-separated list of domains to exclude from data collection. |
|  `data_spa`  | String | Set single page application mode. <ul><li>`auto`: Automatically check if the HTML5 History API is available, otherwise use hash-based routing.</li><li>`history`: Use the HTML5 History API.</li><li>`hash`: Use hash-based routing.</li></ul> |

### Events

For more information on mapping events, see [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Variable | Description |
|:---------|:------------|
|  `trackPageview` | Track Pageview |
|  `trackGoal` | Track Goal |

### Event-specific Parameters
For more information on mapping events, see [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping).

| Variable | Description |
|:---------|:------------|
|  `trackPageview` | Track Pageview |
|  `trackGoal` | Track Goal |
