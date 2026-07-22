---
title: Tealium + Contentsquare Integration Guide
description: This article describes how to get the most out of Tealium and Contentsquare by setting up the Contentsquare UX Analytics tag in your Tealium iQ Tag Management account and enabling the transmission of Tealium audiences and Visitor badges to Contentsquare.
url: https://docs.tealium.com/partners-and-industries/tech-partners/tealium-contentsquare-integration-guide/
---
A working integration of iQ Tag Management with the Contentsquare tag from the Tealium tag marketplace enables customers to execute session replays associated with clickstream data to detect and minimize end customer friction associated with tagged web pages.

## Prerequisites

* **Tealium**
    * iQ Tag Management
    * AudienceStream
    * EventStream (Optional)
* **Contentsquare**
    * Contentsquare Business Edition or higher

## How it works

Contentsquare empowers brands to act on unique behavioral insights to turn user experiences into measurable advantages. Contentsquare daily transforms trillions of digital behaviors into intelligent visualizations and recommendations that can be used to grow revenue, increase loyalty, and fuel innovation. Users can access benchmarks and predictive scoring based on leading global data sets of digital behavior across geographies and industries.

For more information, visit [contentsquare.com](https://contentsquare.com/).


<blockquote>
Previously, Fraud and Ad blocking triggers were available as configuration settings in the Contentsquare tag. These settings are now built-in to the tag and enabled by default.
</blockquote>


### Fraud

* **Excessive Pasting**
Triggers when thresholds are met that identify abnormal and potentially fraudulent pasting behavior within the same visitor session. There are three (3) levels of Fraud likelihood: **low**, **medium**, and **high**.
* **Excessive Reload**
Triggers when thresholds are met that identify abnormal and potentially fraudulent reload behavior within the same visitor session. There are three (3) levels of Fraud likelihood: **low**, **medium**, and **high**

### Ad blocking

* **Ad Blocker Signal**
Identifies when or if certain files are blocked, which signifies that an ad blocker is present.

<blockquote>
You can optionally use signals from your EventStream event specifications and your AudienceStream visitor attributes.
</blockquote>


## Tag tips

* Conversion fires when Order ID is set.
* To make your Contentsquare Replay Link available as a server-side attribute:
    * Contact your Contentsquare representative to enable the generation of the replay link.
    * Set **Send Replay Link** to **True**.

* The Contentsquare tag automatically detects the Tealium account and profile loading on the page and sends the replay link there. To send the replay link to a different account or profile, override the default values by mapping the account and profile you want to the `tealium_account` and `tealium_profile` destinations, respectively.
* To pass Tealium Audiences and Badges to Contentsquare:
    * Contact your Contentsquare representative to enable the receiving of this data.
    * To send a badge to Contentsquare, navigate to the **Badges** tab in the mapping toolbox and enter the name by which the badge will be identified in the Contentsquare system.
    * To send all audiences to Contentsquare, set **Send All Audiences** to **True**.

## Tag configuration

First, go to the Tealium tag marketplace and add the Contentsquare UX User Analytics tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

See: [Contentsquare UX User Analytics Tag Setup Guide](https://docs.tealium.com/contentsquare-ux-analytics-tag/)

After adding the tag, go to the **Data Mappings** section to configure any additional mappings.

## Load rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag. The 'Load on All Pages' rule is the default load rule.

To load this tag on a specific page, create a new load rule with the relevant conditions and load the Contentsquare tag on the page where you want to track the visitor's mouse movements.

## Extensions

You must set `tealium_datasource` in your data layer to allow Contentsquare to send data server-side.

1. Go to **Server-Side &gt; Data Sources.**
1. Add the HTTP API data source
1. Set the name to "Contentsquare Server-Side Events".

When you finish, note the data source key. In iQ Tag Management, use an extension to assign this value to the variable `tealium_datasource`.

If you are running the Tealium Universal Tag (utag.js) version 4.41 or older, you must also set the following variables:

* `tealium_account`
* `tealium_profile`
* `tealium_visitor_id`

These variables are set automatically in version 4.42+.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
| `title` |  <ul><li>(Required) Identifies the tag instance.</li><li>Contentsquare UX Analytics is the default name.</li><li>When using multiple tags by the same vendor, assign a unique name.</li></ul> |
| `id_project` |  <ul><li>The Project Tag ID specific to your project.</li><li>Map to this variable to set the project guide field.</li></ul> |
| `base_url` |  <ul><li>Base URL</li></ul> |
| `send_replay_link` |  <ul><li>Send Contentsquare Replay Link</li><li>Values are **true** or **false**.</li><li>Also known as `contensquare_replay_link`. Note: This variable and session replay capability is currently in development for Contentsquare tag and is expected to be released in H1 2020. </li></ul> |
| `send_udh_audiences` |  <ul><li>Send Customer Data Hub (CDH) audiences.</li><li>Values are **true** or **false**.</li></ul> |
| `tealium_account` |  <ul><li>Tealium account.</li></ul> |
| `tealium_profile` |  <ul><li>Tealium profile.</li></ul> |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  <ul><li>Order ID.</li><li>Overrides `_corder`.</li><li>Required for transactions.</li></ul> |
|`order_total`|  <ul><li>Order total.</li><li>Overrides `_ctotal`.</li><li>Required for transactions.</li></ul> |
|`order_shipping`|  <ul><li>Shipping amount.</li><li>Overrides `_cship`.</li></ul> |
|`order_tax`|  <ul><li>Tax amount.</li><li>Overrides `_ctax`.</li></ul> |
|`product_id`|  <ul><li>Array</li><li>List of Product IDs.</li><li>Overrides `_cprod`.</li></ul> |
|`product_name`|  <ul><li>Array</li><li>List of Names.</li><li>Overrides `_cprodname`.</li><li>Required for transactions.</li></ul> |
|`product_sku`|  <ul><li>Array</li><li>List of SKUs.</li><li>Overrides `_csku`.</li><li>Required for transactions.</li></ul> |
|`product_category`|  <ul><li>Array</li><li>List of Categories.</li><li>Overrides `_ccat`.</li></ul> |
|`product_quantity`|  <ul><li>Array</li><li>List of Quantities.</li><li>Overrides `_cquan`.</li><li>Required for transactions.</li></ul> |
|`product_unit_price`|  <ul><li>Array</li><li>List of Prices.</li><li>Overrides `_cprice`.</li><li>Required for transactions.</li></ul> |

### Badges

|Variable| Description|
|---| ---|
| `title` |  <ul><li>Badge Identifier.</li><li>To send the mapped badge to Contentsquare, enter the name by which the badge will be identified in Contentsquare.</li><li>Tealium automatically includes the badge title as a child property of a new object `send_udh_data`</li><li>Your badge name will appear as mapped to `send_udh_data`.</li></ul> |
