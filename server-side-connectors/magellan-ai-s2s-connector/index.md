---
title: Magellan AI S2S Connector Setup Guide
description: This article describes how to set up the Magellan AI S2S connector.
url: https://docs.tealium.com/server-side-connectors/magellan-ai-s2s-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Magellan AI S2S API
* API Endpoint: `https://mgln.ai`

## Configuration

Navigate to the connector marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Magellan Pixel Token**: Your Magellan AI pixel token. Links all events to your Magellan account. Find this value in your Magellan AI dashboard.

## Actions

| Action Name | AudienceStream | EventStream |
| ----------- | :------------: | :---------: |
| Send Event | ✓ | ✓ |

### Send Event

#### Parameters

| Parameter | Description |
| --- | --- |
| Event Type | (Required) Select the Magellan event type. Determines the endpoint path and controls which fields are relevant for that event.<br>Page View<br>Lead<br>Product<br>Add to Cart<br>Checkout<br>Purchase<br>Identify<br>Code |
| Category | (Optional) Type of action used to submit the lead (for example, `formFill` or `ButtonClick`). |
| Code | (Required for Code events) The coupon or referral code being tracked. Often used for account creation with referrers, where a referral code is passed as the code and `type` is set to `referrer`. Not needed if using Discount Code on a purchase event. |
| Currency | (Required for lead, product, add to cart, checkout, and purchase events) Event currency. Automapped to `_ccurrency` on lead, product, add to cart, checkout, and purchase events. |
| Discount Code | (Optional) Discount or promotional code for checkout and purchase events. Automapped to `_cpromo` for checkout and purchase events. |
| ID | Unique ID used differently across events:<ul><li><code>identify</code> — user ID (required).</li><li><code>view</code> — user ID (optional).</li><li><code>lead</code> — user ID (optional).</li><li><code>checkout</code> — order ID (optional).</li><li><code>purchase</code> — order ID (required).</li></ul>Automapped to <code>_corder</code> on checkout and purchase events. |
| IP Address | (Required) Client IP address. Automapped to the Client IP attribute. |
| Is New Customer | (Optional) Set to `true` when the customer is not a return customer. String values are converted to boolean. |
| Items Product ID | (Optional) Parallel array of product IDs. Automapped to `_cprod` for checkout and purchase events. |
| Items Product Name | (Optional) Parallel array of product names. Automapped to `_cprodname` for checkout and purchase events. |
| Items Product Type | (Optional) Parallel array of product types/categories. Automapped to `_ccat` for checkout and purchase events. |
| Items Product Vendor | (Optional) Parallel array of product vendors. Automapped to `_cbrand` for checkout and purchase events. |
| Items Quantity | (Optional) Parallel array of item quantities. Automapped to `_cquan` for checkout and purchase events. |
| Items Variant ID | (Optional) Parallel array of variant IDs. Automapped to `_csku` for checkout and purchase events. |
| Items Variant Name | (Optional) Parallel array of variant names. |
| Product ID | (Optional) ID of the product. Automapped to `_cprod` for lead, product, and add to cart events (converted to string). |
| Product Name | (Optional) Name of the product. |
| Product Type | (Optional) Type of product (for example, `Women's Shoes`). |
| Product Vendor | (Optional) Vendor of the product. |
| Quantity | (Optional) Event quantity. Automapped to `_cquan` for lead, add to cart, checkout, and purchase events (converted to number). |
| Referrer URL | (Optional) Referrer URL address. Automapped from `dom.referrer` on page view events. |
| Type | (Optional) Category label for the event. For lead events, use to specify the type of lead action, for example `Sales Demo`, `Account Creation`, or `Newsletter signup`. For code events, use to specify the type of code, for example `referrer`. |
| URL | (Required for page view events) URL of the event. Automapped to the Current URL attribute for view events. |
| Value | (Required for lead, product, add to cart, checkout, and purchase events) Value used differently across events:<ul><li><code>lead</code> — total value assigned to the lead. Defaults to <code>0</code> on Lead events.</li><li><code>product</code> — per-item value.</li><li><code>add_to_cart</code> — value of total added to cart.</li><li><code>checkout</code> — total cart value.</li><li><code>purchase</code> — total order value.</li></ul>Automapped to <code>_ctotal</code> on checkout and purchase events, and to the sum of <code>_cprice</code> on add to cart and product events. |
| Variant ID | (Optional) Product variant ID. |
| Variant Name | (Optional) Product variant name. |
| Pixel Token Override | (Optional) Overrides the connector-level Magellan Pixel Token for this action. Use when different events belong to different Magellan pixels. |
| Disable E-Commerce Automapping | When E-Commerce automapping is disabled, standard commerce attributes (**Currency**, **Order ID**, **Value**, **Quantity**, **Product ID**, **Discount Code**, and **Line Items**) are not automapped from Tealium UDO attributes. Map these fields manually in the Event Data and Line Items sections. |
| Disable Identifiers Automapping | When Identifiers automapping is disabled, the **IP Address** is not automapped from the Client IP attribute. Map the IP Address field manually in the Event Data section. |
