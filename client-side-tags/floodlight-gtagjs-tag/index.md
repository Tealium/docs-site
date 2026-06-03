---
title: Floodlight (gtag.js) Tag Setup Guide
description: This article describes how to configure Floodlight in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/floodlight-gtagjs-tag/
---
## Tag tips

* Activate the conversion API before beginning. For more information, see [Google: Create a Google tag for a new Floodlight conversion action](https://support.google.com/ds/answer/7562806).
* Supports the ecommerce extension for:
  * Order ID (`_corder`)  
  * Order Total (`_ctotal`)  
  * List of Product IDs (`_cprod`)  
  * List of Quantities (`_cquan`)  
  * List of Prices (`_cprice`)
* Use mappings to:
  * Set up event triggers
  * Dynamically override standard config values
  * Dynamically override ecommerce extension values
* Pass custom event parameters by mapping to &#34;DoubleClick Custom Parameters&#34; and replacing `myvar` with your custom variable name.
* If you do not need a Session ID while using a list, set SessionID to an empty space or empty string.
* For additional information, see the [Google: Floodlight documentation](https://support.google.com/dcm/partner/answer/7568534).

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Advertiser ID**
  * A single or comma separated list of advertiser identifiers that are the source of the Floodlight activity, or example, `DC-123456789`.
* **Group Tag String**
  * A single or comma-separated list of group tag strings.
  * Must match the number of Advertiser IDs.
* **Activity Tag String**
  * A single or comma-separated list of activity tag strings.
  * Must match the number of Advertiser IDs.
* **Counting Method**
  * A single or comma-separated list of counting methods.
  * Must match the number of Advertiser IDs.
* **Auto Fire Purchase Event**
  * Fires purchase event when an Order ID is present.
  * If counting method is not set it will be set to transactions.
* **Allow Custom Scripts**
  * Enables Dynamic tags to integrate third-party tools for tracking website activity.
* **Global Object**
  * This value is the name of the Global Object used for the event queue.
  * If not specified, `gtag` is used.
  * Not required for most implementations.
* **Data Layer Name**
  * By default, the data layer initiated and referenced by the global site tag is named `dataLayer`.
  * Rename the data layer only if your project requires a separate name.
* **Cross-Tracking Domains**
  * A comma-separated list of domains to use with Cross-Domain Tracking (`setAllowLinker`).
  * This value should be the top-level domain, for example, `tealiumiq.com`.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings]().

The available categories are:

### Standard

|Setting| Description|
|---| ---|
| Advertiser ID `advertiser_id` |  &lt;ul&gt;&lt;li&gt;(Required) String/Array&lt;/li&gt;&lt;li&gt;One or more Advertiser IDs separated by commas.&lt;/li&gt;&lt;li&gt;For example, `DC-12345678`&lt;/li&gt;&lt;li&gt;Data will be sent to all IDs.&lt;/li&gt;&lt;li&gt;Case-sensitive&lt;/li&gt;&lt;/ul&gt; |
| Group Tag String `activity_group` |  &lt;ul&gt;&lt;li&gt;(Required) String/Array&lt;/li&gt;&lt;li&gt;One or more group tag strings separated by commas.&lt;/li&gt;&lt;li&gt;Must match the length of Advertiser ID.&lt;/li&gt;&lt;li&gt;Case-sensitive&lt;/li&gt;&lt;/ul&gt; |
| Activity Tag String `activity` |  &lt;ul&gt;&lt;li&gt;(Required) String/Array&lt;/li&gt;&lt;li&gt;One or more activity tag strings separated by commas.&lt;/li&gt;&lt;li&gt;Must match the length of Advertiser ID.&lt;/li&gt;&lt;li&gt;Case-sensitive&lt;/li&gt;&lt;/ul&gt; |
| Counting Method `counting_method` |  &lt;ul&gt;&lt;li&gt;(Required) String/Array&lt;/li&gt;&lt;li&gt;One or more counting method names separated by commas.&lt;/li&gt;&lt;li&gt;Must match the length of Advertiser ID.&lt;/li&gt;&lt;li&gt;Converts to lowercase.&lt;/li&gt;&lt;/ul&gt; |
| Session ID `session_id` |  &lt;ul&gt;&lt;li&gt;String/Array&lt;/li&gt;&lt;li&gt;Map none, one, or a set of values matching the length of Advertiser ID.&lt;/li&gt;&lt;li&gt;Place blanks where not needed.&lt;/li&gt;&lt;/ul&gt; |
| Event Name `event_name` |  &lt;ul&gt;&lt;li&gt;The name of the current event.&lt;/li&gt;&lt;/ul&gt; |
| Auto Fire Purchase Event `fire_purchase` |  &lt;ul&gt;&lt;li&gt;Values are `True` or `False`.&lt;/li&gt;&lt;li&gt;Fires purchase event when an Order ID is present.&lt;/li&gt;&lt;li&gt;If counting method is not set, it will be set to transactions.&lt;/li&gt;&lt;/ul&gt; |
| Allow Custom Scripts `custom_scripts` |  &lt;ul&gt;&lt;li&gt;Values are `True` or `False`.&lt;/li&gt;&lt;li&gt;The default value is `True`.&lt;/li&gt;&lt;li&gt;Enables Dynamic tags to integrate third-party tools for tracking website activity.&lt;/li&gt;&lt;li&gt;Use to override the configuration value&lt;./li&gt;&lt;/ul&gt; |
| Cross-Tracking Domains `cross_track_domains` | &lt;ul&gt;&lt;li&gt;A comma-separated list of domains to use with Cross-Domain Tracking.&lt;/li&gt;&lt;/ul&gt; |
| Match ID `dc_custom_params.match_id` | &lt;ul&gt;&lt;li&gt;A unique advertiser-created identifier (passed through Floodlight) that you can sync with Google to attribute offline conversions.&lt;/li&gt;&lt;li&gt;This value is case sensitive, limited to 100 characters, and contains only letters (`a-z` or `A-Z`), numbers (`0-9`), underscores (`_`), hyphens (`-`), and periods (`.`).&lt;/li&gt;&lt;/ul&gt; |
| Ordinal `dc_custom_params.ord` | &lt;ul&gt;&lt;li&gt;A unique random number that acts as a cachebuster to prevent the browser from loading ad images and clickthrough URLs from cache.&lt;/li&gt;&lt;li&gt;When you use the [SA360 Enhanced Conversion connector]() in conjunction with the Floodlight tag, we recommend that you map `tealium_random` for non-purchase conversions.&lt;/li&gt;&lt;/ul&gt;  |

### Events

Map to these destinations for triggering specific events on a page.

Use the following steps to trigger an event:

1. Select the `tealium_event` variable.
1. Click **&#43; Add Mapping**.
1. In the left sidebar, click **Event**.
1. In the **Trigger** field, enter the value of the variable being mapped.
1. Select **Conversion** or **Purchase** from the drop-down list.
1. Click **&#43; Add**.
    * To map additional variables, repeat Steps 4, 5, and 6.
1. Click **Done**.  

The event triggers when the supplied value is found in the data layer.

|**Destination Name**| **Description**|
|---| ---|
| conversion `conversion` |  &lt;ul&gt;&lt;li&gt;Map to trigger sending a conversion type event.&lt;/li&gt;&lt;li&gt;Conversion events are not sent by default.&lt;/li&gt;&lt;li&gt;Use the `standard`, `unique` or `per_session` counting method for this event.&lt;/li&gt;&lt;/ul&gt; |
| purchase `purchase` |  &lt;ul&gt;&lt;li&gt;Map to trigger sending a purchase type event.&lt;/li&gt;&lt;li&gt;Purchase events are sent automatically when an order ID is present.&lt;/li&gt;&lt;li&gt;Use the `transactions` or `items_sold` counting method with this event.&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

As the Floodlight (`gtag.js`) tag is e-commerce enabled, it will automatically use the default E-Commerce extension mappings. Manually mapping in this category is generally not needed unless you want to override any extension mappings or an  e-commerce variable is not offered in the extension.

|**Destination Name**| **Description**|
|---| ---|
| Order ID `order_id` |  &lt;ul&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
| Order Total `order_total` |  &lt;ul&gt;&lt;li&gt;Overrides `_ctotal`.&lt;/li&gt;&lt;/ul&gt; |
| List of IDs `product_id` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
| List of Quantities `product_quantity` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;li&gt;Accepts a single number override or an array of values.&lt;/li&gt;&lt;/ul&gt; |
| List of Prices `product_unit_price` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;/ul&gt; |

### Custom

|**Destination Name**| **Description**|
|---| ---|
| DoubleClick Custom Parameters `dc_custom_params.myvar` |  &lt;ul&gt;&lt;li&gt;Use to send custom parameters as part of the `dc_custom_params` object.&lt;/li&gt;&lt;li&gt;Replace `myvar` with the name of your parameter.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 1 `custom.u1` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u1`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 2 `custom.u2` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u2`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 3 `custom.u3` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u3`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 4 `custom.u4` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u4`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 5 `custom.u5` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u5`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 6 `custom.u6` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u6`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 7 `custom.u7` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u7`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 8 `custom.u8` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u8`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 9 `custom.u9` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u9`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 10 `custom.u10` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u10`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 11 `custom.u11` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u11`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 12 `custom.u12` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u12`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 13 `custom.u13` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u13`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 14 `custom.u14` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u14`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 15 `custom.u15` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u15`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 16 `custom.u16` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u16`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 17 `custom.u17` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u17`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 18 `custom.u18` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u18`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 19 `custom.u19` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u19`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 20 `custom.u20` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions.&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u20`.&lt;/li&gt;&lt;li&gt;Defaults to dimension or metric name if not provided in mapping.&lt;/li&gt;&lt;/ul&gt; |
| Custom Variable 21&#43; `custom.u#` |  &lt;ul&gt;&lt;li&gt;Use this custom parameter to add custom metrics and dimensions beyond 20 (not supported in Floodlight Search).&lt;/li&gt;&lt;li&gt;Associate with the custom Floodlight variable `u#`.&lt;/li&gt;&lt;li&gt;Replace the `#` sign in mapping with the number you want.&lt;/li&gt;&lt;/ul&gt; |

#### IAB Transparency and Consent Framework v2

|Variable| Description|
|---| ---|
| Enable TCF Support `tag_enable_tcf_support` |  &lt;ul&gt;&lt;li&gt;Values are `true` or `false`.&lt;/li&gt;&lt;/ul&gt; |

### Enhanced Conversions

| Variable  | Type | Description |
|:---------|:------------|:------------|
|  `user_data.email` | String |Email Address  |
|  `user_data.phone_number` | String |Phone Number  |
|  `user_data.address.first_name` | String |First Name  |
|  `user_data.address.last_name` |String |Last Name  |
| `user_data.address.street` | String |Street Address  | 
|  `user_data.address.city` |String |City  |
|  `user_data.address.region` | String |Region  |
| `user_data.address.postal_code` | String |Postal Code  | 
|  `user_data.address.country` | String |Country  |


## Additional documentation

* [Configuring Multiple Floodlight Tags](/client-side-tags/configuring-multiple-floodlight-tags/)
* [Google: Using the Global Site Tag](https://support.google.com/dcm/partner/answer/7568534)
