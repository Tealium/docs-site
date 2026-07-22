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
* Pass custom event parameters by mapping to "DoubleClick Custom Parameters" and replacing `myvar` with your custom variable name.
* If you do not need a Session ID while using a list, set SessionID to an empty space or empty string.
* For additional information, see the [Google: Floodlight documentation](https://support.google.com/dcm/partner/answer/7568534).

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

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

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/manage-data-mappings/).

The available categories are:

### Standard

|Setting| Description|
|---| ---|
| Advertiser ID `advertiser_id` |  <ul><li>(Required) String/Array</li><li>One or more Advertiser IDs separated by commas.</li><li>For example, `DC-12345678`</li><li>Data will be sent to all IDs.</li><li>Case-sensitive</li></ul> |
| Group Tag String `activity_group` |  <ul><li>(Required) String/Array</li><li>One or more group tag strings separated by commas.</li><li>Must match the length of Advertiser ID.</li><li>Case-sensitive</li></ul> |
| Activity Tag String `activity` |  <ul><li>(Required) String/Array</li><li>One or more activity tag strings separated by commas.</li><li>Must match the length of Advertiser ID.</li><li>Case-sensitive</li></ul> |
| Counting Method `counting_method` |  <ul><li>(Required) String/Array</li><li>One or more counting method names separated by commas.</li><li>Must match the length of Advertiser ID.</li><li>Converts to lowercase.</li></ul> |
| Session ID `session_id` |  <ul><li>String/Array</li><li>Map none, one, or a set of values matching the length of Advertiser ID.</li><li>Place blanks where not needed.</li></ul> |
| Event Name `event_name` |  <ul><li>The name of the current event.</li></ul> |
| Auto Fire Purchase Event `fire_purchase` |  <ul><li>Values are `True` or `False`.</li><li>Fires purchase event when an Order ID is present.</li><li>If counting method is not set, it will be set to transactions.</li></ul> |
| Allow Custom Scripts `custom_scripts` |  <ul><li>Values are `True` or `False`.</li><li>The default value is `True`.</li><li>Enables Dynamic tags to integrate third-party tools for tracking website activity.</li><li>Use to override the configuration value<./li></ul> |
| Cross-Tracking Domains `cross_track_domains` | <ul><li>A comma-separated list of domains to use with Cross-Domain Tracking.</li></ul> |
| Match ID `dc_custom_params.match_id` | <ul><li>A unique advertiser-created identifier (passed through Floodlight) that you can sync with Google to attribute offline conversions.</li><li>This value is case sensitive, limited to 100 characters, and contains only letters (`a-z` or `A-Z`), numbers (`0-9`), underscores (`_`), hyphens (`-`), and periods (`.`).</li></ul> |
| Ordinal `dc_custom_params.ord` | <ul><li>A unique random number that acts as a cachebuster to prevent the browser from loading ad images and clickthrough URLs from cache.</li><li>When you use the [SA360 Enhanced Conversion connector](https://docs.tealium.com/google-sa360-enhanced-conversions-connector/) in conjunction with the Floodlight tag, we recommend that you map `tealium_random` for non-purchase conversions.</li></ul>  |

### Events

Map to these destinations for triggering specific events on a page.

Use the following steps to trigger an event:

1. Select the `tealium_event` variable.
1. Click **+ Add Mapping**.
1. In the left sidebar, click **Event**.
1. In the **Trigger** field, enter the value of the variable being mapped.
1. Select **Conversion** or **Purchase** from the drop-down list.
1. Click **+ Add**.
    * To map additional variables, repeat Steps 4, 5, and 6.
1. Click **Done**.  

The event triggers when the supplied value is found in the data layer.

|**Destination Name**| **Description**|
|---| ---|
| conversion `conversion` |  <ul><li>Map to trigger sending a conversion type event.</li><li>Conversion events are not sent by default.</li><li>Use the `standard`, `unique` or `per_session` counting method for this event.</li></ul> |
| purchase `purchase` |  <ul><li>Map to trigger sending a purchase type event.</li><li>Purchase events are sent automatically when an order ID is present.</li><li>Use the `transactions` or `items_sold` counting method with this event.</li></ul> |

### E-Commerce

As the Floodlight (`gtag.js`) tag is e-commerce enabled, it will automatically use the default E-Commerce extension mappings. Manually mapping in this category is generally not needed unless you want to override any extension mappings or an  e-commerce variable is not offered in the extension.

|**Destination Name**| **Description**|
|---| ---|
| Order ID `order_id` |  <ul><li>Overrides `_corder`.</li></ul> |
| Order Total `order_total` |  <ul><li>Overrides `_ctotal`.</li></ul> |
| List of IDs `product_id` |  <ul><li>Array</li><li>Overrides `_cprod`.</li></ul> |
| List of Quantities `product_quantity` |  <ul><li>Array</li><li>Overrides `_cquan`.</li><li>Accepts a single number override or an array of values.</li></ul> |
| List of Prices `product_unit_price` |  <ul><li>Array</li><li>Overrides `_cprice`.</li></ul> |

### Custom

|**Destination Name**| **Description**|
|---| ---|
| DoubleClick Custom Parameters `dc_custom_params.myvar` |  <ul><li>Use to send custom parameters as part of the `dc_custom_params` object.</li><li>Replace `myvar` with the name of your parameter.</li></ul> |
| Custom Variable 1 `custom.u1` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u1`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 2 `custom.u2` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u2`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 3 `custom.u3` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u3`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 4 `custom.u4` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u4`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 5 `custom.u5` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u5`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 6 `custom.u6` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u6`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 7 `custom.u7` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u7`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 8 `custom.u8` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u8`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 9 `custom.u9` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u9`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 10 `custom.u10` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u10`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 11 `custom.u11` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u11`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 12 `custom.u12` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u12`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 13 `custom.u13` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u13`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 14 `custom.u14` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u14`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 15 `custom.u15` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u15`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 16 `custom.u16` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u16`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 17 `custom.u17` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u17`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 18 `custom.u18` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u18`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 19 `custom.u19` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u19`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 20 `custom.u20` |  <ul><li>Use this custom parameter to add custom metrics and dimensions.</li><li>Associate with the custom Floodlight variable `u20`.</li><li>Defaults to dimension or metric name if not provided in mapping.</li></ul> |
| Custom Variable 21+ `custom.u#` |  <ul><li>Use this custom parameter to add custom metrics and dimensions beyond 20 (not supported in Floodlight Search).</li><li>Associate with the custom Floodlight variable `u#`.</li><li>Replace the `#` sign in mapping with the number you want.</li></ul> |

#### IAB Transparency and Consent Framework v2

|Variable| Description|
|---| ---|
| Enable TCF Support `tag_enable_tcf_support` |  <ul><li>Values are `true` or `false`.</li></ul> |

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

* [Configuring Multiple Floodlight Tags](https://docs.tealium.com/client-side-tags/configuring-multiple-floodlight-tags/)
* [Google: Using the Global Site Tag](https://support.google.com/dcm/partner/answer/7568534)
