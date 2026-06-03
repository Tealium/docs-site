---
title: About Tealium Shopify app
description: This article provides information about the Tealium application in the Shopify Marketplace.
url: https://docs.tealium.com/platforms/shopify/about/
---
The Tealium app in the Shopify Marketplace lets you do the following:

* Use Tealium iQ Tag Management with your Shopify site. The app loads Tealium assets, such as `utag.js` and `utag.data`, on each page of your site.
* Send Shopify event data to Tealium EventStream API Hub.
* Use a custom checkout pixel to send checkout data to EventStream.
* Use Shopify Markets to track events from multiple market regions with a single Shopify store.

Some page events, such as Shopify `purchase` events, are handled differently because they are events that occur on pages managed by Shopify, instead of being managed by iQ Tag Management. The Tealium app sends data for these events to Tealium EventStream.

## Requirements

* Administrative access to your Shopify instance during configuration.
* Your Tealium account and profile information to create a data source in Tealium.
* Tealium EventStream, if you want to send Shopify event data to EventStream.

## Tracked events

The standard data layer is included in the Tealium app and supports the following standard events from Shopify:

| Event | Shopify action |
|-------|----------------|
| `cart_add` | Items added to cart. |
| `cart_remove` | Items removed from cart. |
| `cart_view` | Customer viewed cart. |
| `category_view` | Customer viewed a category. |
| `checkout` | Customer started checkout. |
| `checkout_address_info_submitted` | Customer submitted checkout address information. |
| `page_view `| Customer viewed a page. |
| `product_view` | Customer viewed a product page. |
| `purchase` | Customer completed a purchase. |
| `search` | Customer performed a search. |

For more information, see .

Newsletter sign up events and discount events must be customized for each store.

### Web Pixel Extension events 

| Shopify Event | Tealium Event | Trigger |
|---------------|---------------|---------|
| `page_viewed` | `page_view` | Any storefront page loads. |
| `product_viewed` | `product_view` | Customer views a product detail page. |
| `collection_viewed` | `category_view` | Customer views a collection/category page. |
| `cart_viewed` | `cart_view` | Customer views the cart page. |
| `product_added_to_cart` | `cart_add` | Customer adds item to cart. |
| `product_removed_from_cart` | `cart_remove` | Customer removes item from cart. |
| `search_submitted` | `search` | Customer performs a search query. |

### Checkout Pixel events

| Shopify Event | Tealium Event | Trigger |
|---------------|---------------|---------|
| `checkout_started` | `checkout` | Customer initiates checkout process. |
| `checkout_address_info_submitted` | `checkout_address_info_submitted` | Customer submits shipping address. |
| `checkout_completed` | `purchase` | Order is successfully completed. |

## Webhook events

The following webhooks can be enabled for collecting data:

| Webhook Topic | Tealium Event | Trigger |
|---------------|---------------|---------|
| `CARTS_CREATE` | `cart_create` | Brand new cart is created. |
| `CARTS_UPDATE` | `cart_update` | Cart is modified (add/remove/quantity change). |
| `CHECKOUTS_CREATE` | `checkouts_create` | Checkout session is initiated. |
| `ORDERS_CREATE` | `purchase` | Order is completed and processed. |
| `REFUNDS_CREATE` | `shopify_refund` | Refund is issued on an order. |
| `CUSTOMERS_CREATE` | `Shopify New Customer` | New customer account created. |
| `CUSTOMERS_EMAIL_MARKETING_CONSENT_UPDATE` | `email_consent_change` | Email marketing opt-in/out changes. |
| `CUSTOMERS_MARKETING_CONSENT_UPDATE` | `sms_consent_change` | SMS marketing opt-in/out changes. |

### System/GDPR webhooks

| Webhook Topic | Trigger |
|---------------|---------|
| `APP_UNINSTALLED` | Merchant uninstalls the app. |
| `CUSTOMERS_DATA_REQUEST` | GDPR data access request. |
| `CUSTOMERS_REDACT` | GDPR customer data deletion request. |
| `SHOP_REDACT` | GDPR shop data deletion request. |

## Checkout tracking

Custom pixels are currently the best option for Shopify checkout tracking with Tealium iQ Tag Management. The installation process for the Tealium Shopify app includes the option to configure a custom pixel.

For more information, see [Install the Tealium Shopify app]().