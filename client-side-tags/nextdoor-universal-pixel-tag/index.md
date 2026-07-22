---
title: NextDoor Universal Pixel
description: This article describes how to set up the Nextdoor Universal Pixel tag.
url: https://docs.tealium.com/client-side-tags/nextdoor-universal-pixel-tag/
---
The Nextdoor Universal Tracking Pixel enables standardized event-based tracking across your website, supporting Nextdoor’s updated attribution and optimization models.

## Tag Tips

* Use mappings to override Standard parameters.
* Supports E-Commerce extension parameters.
* Restricted data usage gives advertisers control over how your data is used in Nextdoor’s systems and better supports your compliance efforts with various US state privacy regulations. When advertisers enable restricted data usage, Nextdoor limits how it uses personal data from people in certain states, as required by state-specific terms. This may reduce campaign performance and limit retargeting and measurement features.

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Pixel ID**: Your NextDoor Pixel ID.
* **Auto Page View**: Automatically create a trigger for page views.
* **Auto Purchase Event**: Automatically create a trigger for purchase events.
* **Auto Generate Event ID**: Automatically generate an Event ID for every Nextdoor tracking event.

## Load Rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:-----|:------------|
| `pixelId` | String | Pixel ID |
| `autoPageView` | Boolean | Auto page view |
| `autoPurchaseEvent` | Boolean | Auto purchase event |
| `generate_event_id` | Boolean | Auto generate event ID |
| `event_id` | String | Event ID |
| `click_id` | String | Next Door click ID |
| `nickname` | String | Nickname for custom conversion |

### User

| Variable | Type | Description |
|:---------|:-----|:------------|
| `userEmail` | String | User email |
| `userEmailHashed` | String | User email (already hashed) |

### E-Commerce

| Variable | Type | Description |
|:---------|:-----|:------------|
| `order_id` | String | Order ID (Ooverrides `_corder`) |
| `order_value` | String | Order value (overrides `_ctotal`) |
| `id` | Array | List of product IDs (overrides `_cprod`) |
| `quantity` | Array | List of quantities (overrides `_cquan`) |
| `item_price` | Array | List of prices (overrides `_cprice`) |
| `content_name` | Array | List of content names |

### User Attributes

| Variable | Type | Description |
|:---------|:-----|:------------|
| `city` | String | City |
| `country` | String | Country |
| `date_of_birth` | String | Date of birth |
| `external_id` | String | External ID |
| `email` | String | Email |
| `first_name` | String | First name |
| `gender` | String | Gender |
| `last_name` | String | Last name |
| `phone_number` | String | Phone number |
| `state` | String | State |
| `street_address` | String | Street address |
| `zip_code` | String | Zip code |

### Restricted Data Usage

| Variable | Type | Description |
|:---------|:-----|:------------|
| `restricted_data_usage_country` | Number | Usage country |
| `restricted_data_usage_state` | Number | Usage state |

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Event | Description |
|:------|:------------|
| `city` | City |
| `country` | Country |
| `date_of_birth` | Date of birth |
| `external_id` | External ID |
| `email` | Email |
| `first_name` | First name |
| `gender` | Gender |
| `last_name` | Last name |
| `phone_number` | Phone number |
| `state` | State |
| `street_address` | Street address |
| `zip_code` | Zip code |
| `order_id` | Order ID (overrides `_corder`) |
| `order_value` | Order value (overrides `_ctotal`) |
| `id` | List of product IDs (overrides `_cprod`) |
| `quantity` | List of quantities (overrides `_cquan`) |
| `item_price` | List of prices (overrides `_cprice`) |
| `content_name` | List of content names |