---
title: Configure Shopify Markets
description: This article provides information about how to configure Shopify Markets for use with the Tealium application.
url: https://docs.tealium.com/platforms/shopify/configure-shopify-marketplace/
---
Shopify Markets lets you manage multiple market regions from a single Shopify store. Use the Tealium Shopify app with Shopify Markets to configure market-specific settings to ensure accurate data collection and reporting.

## Prerequisites

* Shopify Markets must be enabled in your Shopify admin (**Settings &gt; Markets**).
* At least one market must be configured in Shopify before using the **Markets** tab.
* Complete the global Tealium configuration in the **Config** tab first.

## Accessing the Markets Tab

1. Open the Tealium app in your Shopify admin.
1. Click the **Markets** tab.
1. The tab displays all markets configured in your Shopify store.

## Configure a market

1. Click the **Configure** button next to the market you want to set up.
1. A modal form opens with the following fields:
   * **Tealium Account**: The Tealium account name for this market.
   * **Tealium Environment**: Select `dev`, `qa`, or `prod`.
   * **Client-Side Profile**: Profile for `utag.js` loading.
   * **Server-Side Profile**: Profile for webhook data (if using server-side tracking).
   * **First-Party Domain**: (Optional) Custom domain for `utag.js`.
   * **Custom Data Layer Config**: (Optional) JSON object for additional data layer variables.
1. Click **Save** to apply the configuration.

## Using inherit defaults

Each market has an **Inherit Defaults** option:

* **Checked**: The market uses the global configuration from the **Config** tab.
* **Unchecked**: The market uses its own custom configuration.

Use this option when most markets share the same settings, but one or two need different profiles.

## Custom data layer configuration

Add market-specific variables to the data layer using JSON format.

Two value types are supported:

**Literal Values**:

```json
{ &#34;market_region&#34;: &#34;EMEA&#34;, &#34;market_currency&#34;: &#34;EUR&#34; }
```
**JavaScript References**:

```json
{ &#34;page_title&#34;: document.title, &#34;current_url&#34;: window.location.href }
```

Dynamic variables (for example, `{{ product.id }}`) are not supported in custom data layer configuration.

## Global vs market settings

Some settings are always global and cannot be changed per market:

* **Tracking Mode**: Client-side, server-side, or both (set in **Config** tab).
* **Webhook Selection**: Which webhooks are enabled (set in **Server Events** tab).

The following settings can be customized per market:

* Tealium Account
* Tealium Environment
* Client-Side Profile
* Server-Side Profile
* First-Party Domains
* Custom Data Layer Variables

## Verifying market configuration

To verify the correct configuration is loading:

1. Enable debug mode (see Debugging section).
1. Navigate to your storefront using a market-specific URL. For example, `/en-de/` for Germany.
1. Open browser developer tools and check the console for Tealium configuration output.
1. Verify that the account, profile, and environment match your market configuration.