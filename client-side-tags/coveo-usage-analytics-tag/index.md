---
title: Coveo Usage Analytics Tag Setup Guide
description: This article describes how to set up the Coveo Usage Analytics (Coveo UA) tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/coveo-usage-analytics-tag/
---
Coveo for Commerce is a data-driven platform that offers recommendations, search, and the ability to manage relevance. The Coveo Usage Analytics JavaScript is used to send events occurring in and out of Coveo-powered pages.

For more information about Coveo UA Javascript, see the Coveo [Collect Commerce Events](https://docs.coveo.com/en/3188/coveo-for-commerce/collect-commerce-events) documentation.

## Tag Tips

Use mappings to:

* Dynamically override config data
* Dynamically override the E-Commerce extension values
* Send additional data values
* Event trigger

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Coveo API Key**: Coveo API Key for Analytics created for your catalog.
* **Alternate Endpoints**: Specify the Coveo endpoint for your region.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules]() documentation.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Global Fields

| Variable                                  | Description |
|:------------------------------------------|:------------|
| Coveo API Key (`coveoApiKey`)             | [String]    |
| Endpoint (`customEndpoint`)               | [String]    |
| Currency Code (`currencyCode`)            | [String]    |
| Anonymize Ip (`anonymizeIp`)              | [Boolean]   |
| Loyalty Card Id (`loyaltyCardId`)         | [String]    |
| Loyalty Tier (`loyaltyTier`)              | [String]    |
| Third Party Persona (`thirdPartyPersona`) | [String]    |
| Company Name (`companyName`)              | [String]    |
| Favorite Store (`favoriteStore`)          | [String]    |
| Store Name (`storeName`)                  | [String]    |
| User Industry (`userIndustry`)            | [String]    |
| User Role (`userRole`)                    | [String]    |
| User Department (`userDepartment`)        | [String]    |
| Business Unit (`businessUnit`)            | [String]    |

### Page Fields

| Variable              | Description |
|:----------------------|:------------|
| Page (`page`)         | [String]    |
| Title (`title`)       | [String]    |
| Location (`location`) | [String]    |

### Product Data Fields

| Variable                                   | Description |
|:-------------------------------------------|:------------|
| ID (`id`) (Overrides `_csku`)              | [Array]     |
| Name (`name`) (Overrides `_cprodname`)     | [Array]     |
| Brand (`brand`) (Overrides `_cbrand`)      | [Array]     |
| Category (`category`) (Overrides `_ccat`)  | [Array]     |
| Group (`group)                             | [Array]     |
| Variant (`variant`)                        | [Array]     |
| List (`list`)                              | [Array]     |
| Price (`price`) (Overrides `_cprice`)      | [Array]     |
| Quantity (`quantity`) (Overrides `_cquan`) | [Array]     |
| Coupon (`coupon`) (Overrides `_cpdisc`)    | [Array]     |
| Position (`position`)                      | [Array]     |

### Transaction Fields

| Variable                    | Description     |
|:----------------------------|:----------------|
| ID (`id`)                   | [Number]        |
| Affiliation (`affiliation`) | [String]        |
| Revenue (`revenue`)         | [String/Number] |
| Tax (`tax`)                 | [String/Number] |
| Shipping (`shipping`)       | [String/Number] |
| Coupon (`coupon`)           | [String]        |

### Quote Fields

| Variable                    | Description |
|:----------------------------|:------------|
| ID (`id`)                   | [Number]    |
| Affiliation (`affiliation`) | [String]    |

### Review Fields

| Variable            | Description |
|:--------------------|:------------|
| ID (`id`)           | [Number]    |
| Rating (`rating`)   | [Number]    |
| Comment (`comment`) | [String]    |

### Events

| Variable                            | Description     |
|:------------------------------------|:----------------|
| Click (`click`)                     | `click`           |
| Detail (`detail`)                   | `detail`          |
| Quick View (`quickview`)            | `quickview`       |
| Impression (`impression`)           | `impression`      |
| Add (`add`)                         | `add`             |
| Remove (`remove`)                   | `remove`          |
| Purchase (`purchase`)               | `purchase`        |
| Refund (`refund`)                   | `refund`          |
| Bookmark Add (`bookmark_add`)       | `bookmark_add`    |
| Bookmark Remove (`bookmark_remove`) | `bookmark_remove` |
| Compare Add (`compare_add`)         | `compare_add`     |
| Compare Remove (`compare_remove`)   | `compare_remove`  |
| Review Add (`review_add`)           | `review_add`      |
| Review Remove (`review_remove`)     | `review_remove`   |
| Quote (`quote`)                     | `quote`           |
| Checkout (`checkout`)               | `checkout`        |
| Checkout Option (`checkout_option`) | `checkout_option` |
| Custom                              | `custom`          |
