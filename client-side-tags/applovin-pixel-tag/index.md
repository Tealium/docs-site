---
title: AppLovin Pixel Tag Setup Guide
description: This article describes how to set up the AppLovin Pixel tag in your tag management account.
url: https://docs.tealium.com/client-side-tags/applovin-pixel-tag/
---
AppLovin Pixel loads the AppLovin web pixel on your site and sends page view, ecommerce, and lead events to AppLovin to measure and optimize your web campaigns.

## Tag tips

* The tag loads `https://s.axon.ai/pixel.js` on the first tag fire and sends events only on subsequent fires. The page supports only one Event Key, which must be exactly 36 characters, otherwise the tag does not fire.
* Map variables to the 13 AppLovin catalog events on the **Events** tab. Custom events are not supported. **Auto Page View** sends `page_view` on every view and never fires twice.
* The tag filters fields per event and does not send empty values. Use **Event-specific Parameters** to override a field for a single event. The tag logs missing required fields in debug mode and still fires the event.
* The `user_data` field holds email, phone, and user ID. Each item in `add_to_cart`, `remove_from_cart`, and `purchase` requires a quantity. Fields per event (required / *optional*):
   * `page_view`, `login`: *user_data*
   * `view_item`, `view_cart`, `add_to_cart`, `remove_from_cart`: items / *currency, value, user_data*
   * `begin_checkout`: currency, value, items / *user_data*
   * `add_payment_info`: *currency, value, items, payment_type, user_data*
   * `purchase`: transaction_id, currency, value, shipping, tax, items, user_data / *is_new_customer*
   * `search`: search_term / *results, user_data*
   * `generate_lead`: currency, value / *user_data*
   * `sign_up`: user_data / *method*
   * `subscribe`: *currency, value, user_data*
* The tag supports E-Commerce Extension variables: `_ccurrency`, `_csubtotal`, `_corder`, `_cship`, `_ctax`, `_cprod`, `_cprodname`, `_cprice`, `_cquan`, `_ccat`, `_csku`, `_cbrand`, and `_cpdisc`.
* The tag accepts email and phone values as plaintext or pre-hashed SHA256. The pixel hashes plaintext values automatically.
* **Generate Event ID** sends a unique `dedupe_id` per event and stores it in `utag.globals` as `applovin_event_id_<event>`. A mapped `dedupe_id` takes precedence.
* The tag suppresses events when consent is denied via `utag.gdpr`.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Event Key**: Your 36-character AppLovin Event Key. Find it in the AppLovin dashboard under **Account > General > Keys**.
* **Auto Page View**: Sends `page_view` on every tag view event. Set to **False** to control page view firing from the Events tab instead. Default: **True**.
* **Generate Event ID**: Generates a unique ID for each event and passes it as `dedupe_id` for browser/server deduplication. The ID is also stored in `utag.globals` as `applovin_event_id_<event>`. Default: **False**.

## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Configuration

Use the Configuration category to override the tag-level Event Key for a specific tag fire.

| Variable | Type/Values | Description |
|:---------|:------------|:------------|
| `event_key` | String | AppLovin Event Key for this fire. Must be exactly 36 characters. Overrides the value set in tag configuration. |

### General

Values mapped in the General category apply to every event. To override a value for a specific event, use the [Event-specific Parameters](#event-specific-parameters) category.

| Variable | Type/Values | Description |
|:---------|:------------|:------------|
| `dedupe_id` | String | (Optional) Deduplication ID passed with the event. |
| `event_data` | Object | (Optional) GA4-formatted ecommerce object. General and E-Commerce mappings override matching keys. Keys the event does not accept are dropped. |
| `user_data.email` | String | (Optional) User email address (plaintext or pre-hashed SHA256). |
| `user_data.phone` | String | (Optional) User phone number (plaintext or pre-hashed SHA256). |
| `user_data.user_id` | String | (Optional) Customer identifier. |
| `payment_type` | String | (Optional) Payment method. Used with `add_payment_info` events. |
| `search_term` | String | (Required for `search`) Text the user searched for. |
| `method` | String | (Optional) Sign-up method (for example, `email` or `google`). Used with `sign_up` events. |
| `is_new_customer` | Boolean | (Optional) Whether the purchaser is a new customer. Used with `purchase` events. |

### E-Commerce

Values mapped in the E-Commerce category override the corresponding E-Commerce Extension variables.

| Variable | Type/Values | Description |
|:---------|:------------|:------------|
| `currency` | String | ISO 4217 currency code (for example, `USD`). Required for `begin_checkout`, `purchase`, and `generate_lead`. (Overrides `_ccurrency`.) |
| `value` | Number | Monetary value of the event. Required for `begin_checkout`, `purchase`, and `generate_lead`. (Overrides `_csubtotal`.) |
| `transaction_id` | String | Unique order identifier. Required for `purchase`. (Overrides `_corder`.) |
| `shipping` | Number | Shipping cost. Required for `purchase`. Sent as `0` when unmapped. (Overrides `_cship`.) |
| `tax` | Number | Tax amount. Required for `purchase`. Sent as `0` when unmapped. (Overrides `_ctax`.) |
| `product_id` | Array | Product IDs, one per item. Required for `view_item`, `view_cart`, `add_to_cart`, `remove_from_cart`, `begin_checkout`, and `purchase`. (Overrides `_cprod`.) |
| `product_name` | Array | Product names, one per item. (Overrides `_cprodname`.) |
| `product_price` | Array | Unit prices, one per item. (Overrides `_cprice`.) |
| `product_quantity` | Array | Quantities, one per item. Required per item for `add_to_cart`, `remove_from_cart`, and `purchase`. (Overrides `_cquan`.) |
| `product_category_id` | Array | Integer category IDs, one per item. Non-integer values are dropped. (Overrides `_ccat`.) |
| `product_variant_id` | Array | Variant IDs, one per item. (Overrides `_csku`.) |
| `product_brand` | Array | Brand names, one per item. (Overrides `_cbrand`.) |
| `product_discount` | Array | Per-item discount amounts. (Overrides `_cpdisc`.) |
| `product_image_url` | Array | Product image URLs, one per item. |
| `product_affiliation` | Array | Affiliation values, one per item. |

### Events

To map events, see [Create an event mapping](#add-an-event-mapping).

Only the following 13 catalog events are supported. Custom event names are silently skipped.

| Event | Required | Optional |
|:------|:---------|:---------|
| `page_view` | None | `user_data` |
| `view_item` | `items` | `currency`, `value`, `user_data` |
| `view_cart` | `items` | `currency`, `value`, `user_data` |
| `add_to_cart` | `items` (each item requires `quantity`) | `currency`, `value`, `user_data` |
| `remove_from_cart` | `items` (each item requires `quantity`) | `currency`, `value`, `user_data` |
| `begin_checkout` | `currency`, `value`, `items` | `user_data` |
| `add_payment_info` | None | `currency`, `value`, `items`, `payment_type`, `user_data` |
| `purchase` | `transaction_id`, `currency`, `value`, `shipping`, `tax`, `items` (each item requires `quantity`), `user_data` | `is_new_customer` |
| `search` | `search_term` | `results`, `user_data` |
| `generate_lead` | `currency`, `value` | `user_data` |
| `sign_up` | `user_data` | `method` |
| `login` | None | `user_data` |
| `subscribe` | None | `currency`, `value`, `user_data` |

### Event-specific Parameters

Use the Event-specific Parameters category to override any General or E-Commerce mapping for a single event. Values set here take precedence over the General and E-Commerce categories for the selected event.
