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

Previously, Fraud and Ad blocking triggers were available as configuration settings in the Contentsquare tag. These settings are now built-in to the tag and enabled by default.

### Fraud

* **Excessive Pasting**
Triggers when thresholds are met that identify abnormal and potentially fraudulent pasting behavior within the same visitor session. There are three (3) levels of Fraud likelihood: **low**, **medium**, and **high**.
* **Excessive Reload**
Triggers when thresholds are met that identify abnormal and potentially fraudulent reload behavior within the same visitor session. There are three (3) levels of Fraud likelihood: **low**, **medium**, and **high**

### Ad blocking

* **Ad Blocker Signal**
Identifies when or if certain files are blocked, which signifies that an ad blocker is present.
You can optionally use signals from your EventStream event specifications and your AudienceStream visitor attributes.

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

First, go to the Tealium tag marketplace and add the Contentsquare UX User Analytics tag (Learn more about [how to add a tag]()).

See: [Contentsquare UX User Analytics Tag Setup Guide]()

After adding the tag, go to the **Data Mappings** section to configure any additional mappings.

## Load rules

[Load Rules]() determine when and where to load an instance of this tag. The &#39;Load on All Pages&#39; rule is the default load rule.

To load this tag on a specific page, create a new load rule with the relevant conditions and load the Contentsquare tag on the page where you want to track the visitor&#39;s mouse movements.

## Extensions

You must set `tealium_datasource` in your data layer to allow Contentsquare to send data server-side.

1. Go to **Server-Side &amp;gt; Data Sources.**
1. Add the HTTP API data source
1. Set the name to &#34;Contentsquare Server-Side Events&#34;.

When you finish, note the data source key. In iQ Tag Management, use an extension to assign this value to the variable `tealium_datasource`.

If you are running the Tealium Universal Tag (utag.js) version 4.41 or older, you must also set the following variables:

* `tealium_account`
* `tealium_profile`
* `tealium_visitor_id`

These variables are set automatically in version 4.42&#43;.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
| `title` |  &lt;ul&gt;&lt;li&gt;(Required) Identifies the tag instance.&lt;/li&gt;&lt;li&gt;Contentsquare UX Analytics is the default name.&lt;/li&gt;&lt;li&gt;When using multiple tags by the same vendor, assign a unique name.&lt;/li&gt;&lt;/ul&gt; |
| `id_project` |  &lt;ul&gt;&lt;li&gt;The Project Tag ID specific to your project.&lt;/li&gt;&lt;li&gt;Map to this variable to set the project guide field.&lt;/li&gt;&lt;/ul&gt; |
| `base_url` |  &lt;ul&gt;&lt;li&gt;Base URL&lt;/li&gt;&lt;/ul&gt; |
| `send_replay_link` |  &lt;ul&gt;&lt;li&gt;Send Contentsquare Replay Link&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;li&gt;Also known as `contensquare_replay_link`. Note: This variable and session replay capability is currently in development for Contentsquare tag and is expected to be released in H1 2020. &lt;/li&gt;&lt;/ul&gt; |
| `send_udh_audiences` |  &lt;ul&gt;&lt;li&gt;Send Customer Data Hub (CDH) audiences.&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
| `tealium_account` |  &lt;ul&gt;&lt;li&gt;Tealium account.&lt;/li&gt;&lt;/ul&gt; |
| `tealium_profile` |  &lt;ul&gt;&lt;li&gt;Tealium profile.&lt;/li&gt;&lt;/ul&gt; |

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
|---| ---|
| `title` |  &lt;ul&gt;&lt;li&gt;Badge Identifier.&lt;/li&gt;&lt;li&gt;To send the mapped badge to Contentsquare, enter the name by which the badge will be identified in Contentsquare.&lt;/li&gt;&lt;li&gt;Tealium automatically includes the badge title as a child property of a new object `send_udh_data`&lt;/li&gt;&lt;li&gt;Your badge name will appear as mapped to `send_udh_data`.&lt;/li&gt;&lt;/ul&gt; |
