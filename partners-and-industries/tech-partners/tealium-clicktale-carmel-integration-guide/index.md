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
You can optionally use signals from your EventStream event specifications and your AudienceStream visitor attributes.

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

First, go to Tealium&#39;s tag marketplace and add the Clicktale Carmel tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings in the Data Mappings section.

## Load rules

[Load Rules]() determine when and where to load an instance of this tag. The &#39;Load on All Pages&#39; rule is the default load rule. To load this tag on a specific page, create a new load rule with the relevant conditions.

* Load this tag on the page where you want to track the visitor&#39;s mouse movements.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
| `title` |  &lt;ul&gt;&lt;li&gt;(Required) Identifies the tag instance.&lt;/li&gt;&lt;li&gt;Clicktale Carmel is the default name.&lt;/li&gt;&lt;li&gt;When using multiple tags by the same vendor, assign a unique name.&lt;/li&gt;&lt;/ul&gt; |
|`partition`|  &lt;ul&gt;&lt;li&gt;Partition.&lt;/li&gt;&lt;li&gt;The partition where data is sent.&lt;/li&gt;&lt;li&gt;Map to this variable to dynamically configure the server partition value.&lt;/li&gt;&lt;/ul&gt; |
|`project_guid`|  &lt;ul&gt;&lt;li&gt;Project GUID.&lt;/li&gt;&lt;li&gt;Map to this variable to set the project guide field.&lt;/li&gt;&lt;/ul&gt; |
|`send_replay_link`|  &lt;ul&gt;&lt;li&gt;Send Clicktale Replay Link&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`send_udh_audiences`|  &lt;ul&gt;&lt;li&gt;Send UDH Audiences.&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;Tealium Account.&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;Tealium Profile.&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;Order ID.&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;li&gt;Required for transactions.&lt;/li&gt;&lt;/ul&gt; |
|`order_total`|  &lt;ul&gt;&lt;li&gt;Order total.&lt;/li&gt;&lt;li&gt;Overrides `_ctotal`.&lt;/li&gt;&lt;li&gt;Required for transactions.&lt;/li&gt;&lt;/ul&gt; |
|`order_shipping`|  &lt;ul&gt;&lt;li&gt;Shipping amount.&lt;/li&gt;&lt;li&gt;Overrides `_cship`.&lt;/li&gt;&lt;/ul&gt; |
|`order_tax`|  &lt;ul&gt;&lt;li&gt;Tax amount.&lt;/li&gt;&lt;li&gt;Overrides `_ctax`.&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product IDs.&lt;/li&gt;&lt;li&gt;Overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Names.&lt;/li&gt;&lt;li&gt;Overrides `_cprodname`.&lt;/li&gt;&lt;li&gt;Required for transactions.&lt;/li&gt;&lt;/ul&gt; |
|`product_sku`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of SKUs.&lt;/li&gt;&lt;li&gt;Overrides `_csku`.&lt;/li&gt;&lt;li&gt;Required for transactions.&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Categories.&lt;/li&gt;&lt;li&gt;Overrides `_ccat`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities.&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;li&gt;Required for transactions.&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Prices.&lt;/li&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;li&gt;Required for transactions.&lt;/li&gt;&lt;/ul&gt; |

### Badges

|Variable| Description|
| --- | --- |
| `title` |  &lt;ul&gt;&lt;li&gt;Badge Identifier.&lt;/li&gt;&lt;li&gt;To send the mapped badge to Clicktale, enter the name by which the badge will be identified in Clicktale.&lt;/li&gt;&lt;li&gt;Tealium automatically includes the badge title as a child property of a new object `send_udh_data`&lt;/li&gt;&lt;li&gt;Your badge name will appear as mapped to `send_udh_data`.&lt;/li&gt;&lt;/ul&gt; |
