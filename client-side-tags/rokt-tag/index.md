---
title: Rokt Tag Setup Guide
description: This article describes how to set up the Rokt tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/rokt-tag/
---
For more information about Rokt's suite of SDKs and APIs, please read the [Rokt Integration Guides](https://docs.rokt.com/docs/developers/integration-guides/overview%20).

## Tag Tips

* Use mapping to override the standard config values and trigger events.

## Tag Configuration

First, go to the tag marketplace and add the Rokt tag. For more information, see [Manage Tags](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Rokt Account ID**: Your Rokt account ID.
* **Two-step Email**: Send email address only on positive engagement.
* **Use Sandbox**: Send events to sandbox account for testing.

## Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of the Rokt tag on your site.

Create a load rule to load the Rokt tag on your conversion page.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable           | Type | Description   |
|:-------------------|:--------------|:--------------|
| `email`| String |Email                   |
| `firstname`| String |First name          |
| `lastname`| String |Last name            |
| `mobile`| String |Mobile number         |
| `zipcode`| String |ZIP or Postal code    |
| `country`| String | ISO Alpha-2 country code    |
| `language`| String |Language             |
| `sandbox`   |Boolean |Select `True` if you would like to send events to a sandbox account for testing.        | 

### E-Commerce

| Variable                        | Attribute           | Type | Description                                             |
|:--------------------------------|:--------------------|:--------------------|:--------------------------------------------------------|
| Confirmation Number             | `confirmationref` | Number | This variable overrides the `_corder` variable.    Confirmation reference number.      |
| Amount                          | `amount`          | Number |This variable overrides the `_ctotal` variable.  Transaction amount.       |
| Currency                        | `currency`        | String |This variable overrides the `_ccurrency` variable. Three-letter currency code (for example, `USD`).     |
| Payment Type                    | `paymenttype`    | String| The payment type (for example, `Credit Card`). |                                                         |
| ccbin                           | `ccbin`           | String | Credit card BIN.                                                         |
| List of Item Prices             | `price`          | Array of Numbers | This array overrides the `_cprice` variable. A list of the price of each product.   |
| List of Item Quantities          | `quantity`        | Array of Numbers |This array overrides the `_cquan` variable. A list of the prices of each product.      |
| List of Item Major Categories   | `majorcat`        | Array of Strings |This array overrides the `_ccat` variable. A list of the categories of each product.       |
| List of Item Major Category IDs | `majorcatid`      | Array of Strings | A list of the major category IDs of each product. |
| List of Item Minor Categories   | `minorcat`        | Array of Strings | This array overrides the `_ccat2` variable. A list of the minor categories of each product.      |
| List of Item Minor Category IDs | `minorcatid`      | Array of Strings | A list of the minor category IDs of each product.                                                |
| List of Product Names           | `productname`     | Array of Strings | This array overrides the `_cprodname` variable. A list of the names of each product.|
| List of Item SKUs               | `sku`             | Array of Strings | This array overrides the `_csku` variable. A list of the SKUs of each product.     |
