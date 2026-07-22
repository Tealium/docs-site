---
title: OpenAI Measurement Pixel Tag
description: This article describes how to set up the OpenAI Measurement Pixel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/openai-measurement-pixel-tag/
---
OpenAI Measurement Pixel lets you measure conversions and customer actions on your website to optimize OpenAI ad campaigns.

## Tag tips

* Use the **Events** tab to wire a data layer variable to one of the OpenAI event types. The tag fires one measurement per matched trigger.
* Use the **Configuration** tab to override **Pixel ID** or **Custom SDK URL** per-fire (for example, multi-brand profiles). Use the **General** tab for event-level options and consent, and the **E-Commerce** tab for order totals, currency, and per-product arrays. Use the **Event-specific Parameters** tab to override either for a single event.
* Global values are automatically filtered per event. For example, `plan_id` is attached only to `subscription_created`, `trial_started`, and `custom` events.
* Page views and purchases auto-fire by default. Disable via the **Auto Page View** and **Auto Order Created** options.
* Supports these E-Commerce extension parameters:
    * Sub Total (`_csubtotal`)
    * Currency (`_ccurrency`)
    * Order ID (`_corder`)
    * List of Product IDs (`_cprod`)
    * List of Product Names (`_cprodname`)
    * List of Categories (`_ccat`)
    * List of Quantities (`_cquan`)
    * List of Prices (`_cprice`)
* **Amount** and **Product Amount** are mapped in major units (for example, 129.99). The tag converts to integer minor units per the OpenAI API.
* When **Product Type** is unmapped, contents default to `product` so every call passes vendor validation.
* To fire a custom OpenAI event, select **Custom** on the **Events** or **Event-specific Parameters** tab and enter the vendor event name in the field that appears. Any event name mapped here that is not in the OpenAI standard list is auto-routed as a `custom` event with that name.
* Obtain your **Pixel ID** from your OpenAI account team. Self-serve provisioning via OpenAI Ads Manager is not supported.
* Respects the Tealium consent state via `utag.gdpr.getConsentState()` and skips firing when consent is denied. Map the **Consent** destination to forward grant or revoke directly to the OpenAI SDK.
* Do not send **User Object** fields (email, phone, IP, and so on).

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Pixel ID**: Your OpenAI Pixel ID. Obtain this value from your OpenAI account team.
* **Debug Mode**: Enable OpenAI SDK debug logging in the browser console.
* **Custom SDK URL**: (Optional) Override base URL.
* **Auto Page View**: Auto-queue `page_viewed` on every Tealium view event (default `true`). Skips if `page_viewed` is already queued from an explicit **Events** tab trigger.
* **Auto Order Created**: Auto-queue `order_created` when the **E-Commerce** extension has populated `_corder` and `order_created` is not already queued (default `true`).

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Configuration

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `pixel_id` | `String` | Pixel ID |
| `custom_sdk_url` | `String` | Custom SDK URL |


### General

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `plan_id` | `String` | Plan ID |
| `consent` | `String` | Consent |


### E-Commerce

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `amount` | `Integer` | Amount (Overrides `_csubtotal`) |
| `currency` | `String` | Currency (Overrides `_ccurrency`) |
| `product_id` | `Array` | Product ID (Overrides `_cprod`) |
| `product_name` | `Array` | Product Name (Overrides `_cprodname`) |
| `product_type` | `Array` | Product Type (Overrides `_ccat`) |
| `product_quantity` | `Array` | Product Quantity (Overrides `_cquan`) |
| `product_amount` | `Array` | Product Amount (Overrides `_cprice`) |
| `product_currency` | `Array` | Product Currency (Overrides `_ccurrency`) |


### Event-specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Event | Description |
|:------|:------------|
| `amount` | Amount (Overrides `_csubtotal`) |
| `currency` | Currency (Overrides `_ccurrency`) |
| `plan_id` | Plan ID |
| `product_id` | Product ID (Overrides `_cprod`) |
| `product_name` | Product Name (Overrides `_cprodname`) |
| `product_type` | Product Type (Overrides `_ccat`) |
| `product_quantity` | Product Quantity (Overrides `_cquan`) |
| `product_amount` | Product Amount (Overrides `_cprice`) |
| `product_currency` | Product Currency (Overrides `_ccurrency`) |
