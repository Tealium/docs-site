---
title: Tealium + Clicktale Integration Guide
description: This article describes how to set up the Clicktale tag in your iQ Tag Management account.
url: https://docs.tealium.com/partners-and-industries/tech-partners/tealium-clicktale-carmel-integration-guide/
---
A working integration of iQ Tag Management with the Clicktale tag from the Tealium tag marketplace enables customers to seamlessly execute session replays associated with clickstream data to detect and minimize end customer friction associated with tagged web pages.

## Prerequisites

* **Tealium**
    * iQ Tag Management
    * AudienceStream
    * EventStream (Optional)
* **Clicktale**
    * Clicktale real-time signals are available to all customers with access to the Data Export

## How it works

Clicktale empowers brands to act on unique behavioral insights to turn user experiences into measurable advantages. For more information about Clicktale, a Contentsquare company, visit[ contentsquare.com](https://contentsquare.com/).


### Fraud

* **Excessive Pasting**  
Triggers when thresholds are met that identify abnormal and potentially fraudulent pasting behavior within the same visitor session. There are three (3) levels of Fraud likelihood: **low**, **medium**, and **high**.
* **Excessive Reload**  
Triggers when thresholds are met that identify abnormal and potentially fraudulent reload behavior within the same visitor session. There are three (3) levels of Fraud likelihood: **low**, **medium**, and **high**

### Ad blocking

* **Ad Blocker Signal**  
Identifies when or if certain files are blocked, which identifies that an ad-blocker is present.   

<blockquote>
You can optionally use signals from your EventStream event specifications and your AudienceStream visitor attributes.
</blockquote>


## Tag tips

* Conversion fires when Order ID is set.
* To send your Clicktale Replay Link to Tealium, you must:
    1. Contact your Clicktale representative to enable the generation of the replay link.
    1. Set the Send Replay Link configuration to **True**.
* The Contentsquare tag automatically detects the Tealium account and profile loading on the page and sends the replay link there. To send the replay link to a different account or profile, override the default values by mapping the account and profile you want to the `tealium_account` and `tealium_profile` destinations, respectively
* To pass Tealium Audiences and Badges to Clicktale:
    1. Contact your Clicktale representative to enable the receiving of this data.
    1. To send a badge to Clicktale, navigate to the Badges tab in the mapping toolbox and enter the name by which the badge will be identified in the Clicktale system.
    1. To send all Audiences to Clicktale, toggle the Send UDH Audiences toggle to **True**.

## Tag configuration

First, go to Tealium's tag marketplace and add the Clicktale Carmel tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings in the Data Mappings section.

## Load rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag. The 'Load on All Pages' rule is the default load rule. To load this tag on a specific page, create a new load rule with the relevant conditions.

* Load this tag on the page where you want to track the visitor's mouse movements.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
| `title` |  <ul><li>(Required) Identifies the tag instance.</li><li>Clicktale Carmel is the default name.</li><li>When using multiple tags by the same vendor, assign a unique name.</li></ul> |
|`partition`|  <ul><li>Partition.</li><li>The partition where data is sent.</li><li>Map to this variable to dynamically configure the server partition value.</li></ul> |
|`project_guid`|  <ul><li>Project GUID.</li><li>Map to this variable to set the project guide field.</li></ul> |
|`send_replay_link`|  <ul><li>Send Clicktale Replay Link</li><li>Values are **true** or **false**.</li></ul> |
|`send_udh_audiences`|  <ul><li>Send UDH Audiences.</li><li>Values are **true** or **false**.</li></ul> |
|`tealium_account`|  <ul><li>Tealium Account.</li></ul> |
|`tealium_profile`|  <ul><li>Tealium Profile.</li></ul> |

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
| --- | --- |
| `title` |  <ul><li>Badge Identifier.</li><li>To send the mapped badge to Clicktale, enter the name by which the badge will be identified in Clicktale.</li><li>Tealium automatically includes the badge title as a child property of a new object `send_udh_data`</li><li>Your badge name will appear as mapped to `send_udh_data`.</li></ul> |
