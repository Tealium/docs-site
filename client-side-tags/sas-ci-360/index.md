---
title: SAS Customer Intelligence 360 Tag Setup Guide
description: This article describes how to set up the SAS Customer Intelligence 360 tag.
url: https://docs.tealium.com/client-side-tags/sas-ci-360/
---
SAS Customer Intelligence 360 provides marketing analytics and dynamic content personalization through its digital intelligence capabilities.

## Tag tips

Use mappings to: 

* Set up event triggers
* Map event-specific parameters to Event Names
* Dynamically override standard config values
* Dynamically override E-Commerce extension values

Supports the following E-Commerce extension parameters:

* Order ID
* Order Total
* Shipping Amount
* Tax Amount
* Customer City
* Customer Country
* Customer Zip
* List of Product IDs
* List of Names
* List of SKUs
* List of Quantities
* List of Prices
* List of Categories


## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Server**: (Required) This variable is populated with the server address for your region or is based on your CNAME configuration. Typically, this is your domain name. (for example, `https://www.[Domain].com`).
* **Tenant ID**: (Required) An alphanumeric value (for example, `111aaaaa1111111111111aaa`).
* **Identity**: (Optional) An alphanumeric value (for example, `111aaaaa1111111111111aaa`).
* **Name**: The location of the identity information. Required if Identity tracking is enabled.
* **Type**: The type of known identity. Required if Identity tracking is enabled.
* **Source**: The source of the identity information. Default value is `cookie`.
* **Obscure**: Obscure the value of the identity name.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| Server `server`  | String |
| Tenant ID `tenantID`  | String |
| Identity `identity`  | Boolean |
| Name `name`  | String |
| Type `type`  | String |
| Source `source`  | String |
| Obscure `obscure`  | Boolean |

### E-Commerce

| Variable | Description |
|:---------|:------------|
| Order ID `orderId` (Overrides `_corder`)  | Number, String |
| Order Total `totalCartValue` (Overrides `_ctotal`)  | Number, String |
| Customer City `billingCity` (Overrides `_ccity`)  | String |
| Customer Country `billingCountry` (Overrides `_ccountry`)  | String |
| Customer Zip `billingPostcode` (Overrides `_czip`)  | String |
| Customer Region `billingRegion`  | String |
| Delivery Type `deliveryType`  | String |
| Payment Type `paymentType`  | String |
| Shipping City `shippingCity`  | String |
| Shipping Amount `shippingCost` (Overrides `_cship`)  | String |
| Shipping Country `shippingCountry`  | String |
| Shipping Zip `shippingPostcode`  | String |
| Shipping Region `shippingRegion`  | String |
| Tax Amount `tax` (Overrides `_ctax`)  | Number, String |
| ID `id`  | String |
| Product IDs `productId` (Overrides `_cprod`)  | Array |
| Product SKUs `productSKU` (Overrides `_csku`)  | Array |
| Product Names `productName` (Overrides `_cprodname`)  | Array |
| Product Quantities `quantity` (Overrides `_cquan`)  | Array |
| Product Prices `unitPrice` (Overrides `_cprice`)  | [Array] |
| Group `group` (Overrides `_ccat`)  | Array |
| Cart ID `cartId`  | [Number, String] |
| Cart Name `cartName`  | String |
| Cart Type `cartType`  | String |
| Savings Message `savingsMessage`  | Array |
| Shipping Message `shippingMessage`  | Array |
| Availability Message `availabilityMessage`  | Array |
| Spot Name `spotName`  | String |

### Click

| Variable | Description |
|:---------|:------------|
| Alt Text `altText`  | String |
| Anchor Id `anchorId`  | String |
| Anchor Name `anchorName`  | Boolean |
| Element Tag Name `elementTagName`  | String |
| onClick `onClick`  | String |
| Target Inner Text `targetInnerText`  | String |
| Target Selector Path `targetSelectorPath`  | String |
| Uri `uri`  | String |

### Media

| Variable | Description |
|:---------|:------------|
| Duration `duration`  | String |
| Player `player`  | String |
| Position `position`  | Boolean |
| Url `url`  | String |
| Uri `uri`  | String |

### Promotion

| Variable | Description |
|:---------|:------------|
| Record Type `recordType`  | String |
| Creative Name `creativeName`  | String |
| Placement Id `placementId`  | String |
| Tracking Code `trackingCode`  | String |

### Load

| Variable | Description |
|:---------|:------------|
| Page Title `pageTitle`  | String |
| Referrer `referrer`  | String |
| Uri `uri`  | String |

### Identity

| Variable | Description |
|:---------|:------------|
| Login Id `loginId`  | String |
| Login Event Type `loginEventType`  | String |
| Obfuscate Fields `obfuscateFields`  | String |

### Custom

| Variable | Description |
|:---------|:------------|
| customName `customName`  | String |
| customGroupName `customGroupName`  | String |
| customRevenue `customRevenue`  | String |

### Event Triggers
To map events, refer to [Create an Event Mapping](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| Cart, Cart View Action (`cart-cartview`) | `cart-cartview` |
| Cart, Checkout Action (`cart-checkout`) | `cart-checkout` |
| Cart, Purchase Action (`cart-purchase`) | `cart-purchase` |
| Cart Action, Add Action (`cartaction-add`) | `cartaction-add` |
| Cart Action, Update Action (`cartaction-update`) | `cartaction-update` |
| Cart Action, Remove Action (`cartaction-remove`) | `cartaction-remove` |
| Media, End Action (`media-end`) | `media` |
| Media, Start Action (`media-start`) | `media` |
| Media, Stop Action (`media-stop`) | `media` |
| Change (`change`) | `change` |
| Click (`click`) | `click` |
| Clickthrough (`clickthrough`) | `clickthrough` |
| Content Change (`contentchange`) | `contentchange` |
| Attach Identity Blocking (`attachIdentityBlocking`) | `attachIdentityBlocking` |
| Attach Identity (`attachIdentity`) | `attachIdentity` |
| Detach Identity Cross Channel (`detachIdentityCrossChannel`) | `detachIdentityCrossChannel` |
| Detach Identity (`detachIdentity`) | `detachIdentity` |
| Document (`document`) | `document` |
| Impression (`impression`) | `impression` |
| Impression Viewable (`impressionViewable`) | `impressionViewable` |
| Internal Search (`internalSearch`) | `internalSearch` |
| JS Var Change (`jsvarchange`) | `jsvarchange` |
| Load (`load`) | `load` |
| Product View (`productView`) | `productView` |
| Promotion (`promotion`) | `promotion` |
| Submit (`submit`) | `submit` |
| Visibility Change (`visibilityChange`) | `visibilityChange` |
| Custom (`custom`) | `custom` |

### Event-specific Parameters
To map events, refer to [Create an Event Mapping](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| Cart, Cart View Action (`cart-cartview`) | `cart-cartview` |
| Cart, Checkout Action (`cart-checkout`) | `cart-checkout` |
| Cart, Purchase Action (`cart-purchase`) | `cart-purchase` |
| Cart Action, Add Action (`cartaction-add`) | `cartaction-add` |
| Cart Action, Update Action (`cartaction-update`) | `cartaction-update` |
| Cart Action, Remove Action (`cartaction-remove`) | `cartaction-remove` |
| Media, End Action (`media-end`) | `media` |
| Media, Start Action (`media-start`) | `media` |
| Media, Stop Action (`media-stop`) | `media` |
| Change (`change`) | `change` |
| Click (`click`) | `click` |
| Clickthrough (`clickthrough`) | `clickthrough` |
| Content Change (`contentchange`) | `contentchange` |
| Attach Identity Blocking (`attachIdentityBlocking`) | `attachIdentityBlocking` |
| Attach Identity (attachIdentity) | `attachIdentity` |
| Detach Identity Cross Channel (`detachIdentityCrossChannel`) | `detachIdentityCrossChannel` |
| Detach Identity (`detachIdentity`) | `detachIdentity` |
| Document (`document`) | `document` |
| Impression (`impression`) | `impression` |
| Impression Viewable (`impressionViewable`) | `impressionViewable` |
| Internal Search (`internalSearch`) | `internalSearch` |
| JS Var Change (`jsvarchange`) | `jsvarchange` |
| Load (`load`) | `load` |
| Product View (`productView`) | `productView` |
| Promotion (`promotion`) | `promotion` |
| Submit (`submit`) | `submit` |
| Visibility Change (`visibilityChange`) | `visibilityChange` |
| Custom (`custom`) | `custom` |

