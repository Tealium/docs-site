---
title: Rocket Fuel Tag Setup Guide
description: Learn how to set up the Rocket Fuel Tag in your Tealium iQ profile. Also learn how to use the Mapping Toolbox for sending data to this Tag's destinations.
url: https://docs.tealium.com/client-side-tags/rocket-fuel-tag/
---
## Prerequisites

* Rocket Fuel Account ID
* Parameterized Pixel ID
* Conversion Pixel ID

## Add the Tag

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

## Configure the Tag Settings

1. **Title**: Enter a descriptive title to identify the Tag instance.
1. **Account ID (rb)**: Enter the numeric identifier of your Rocket Fuel account.
1. **Parameterized Action ID (ca)**: Enter the numeric identifier of the **Parameterized** Pixel that Rocket Fuel has provided you.
1. **Conversion Action ID (ca)**: Enter the numeric identifier of the **Conversion** Pixel that Rocket Fuel has provided you.


<blockquote>
You have the option to send the Account ID and Action IDs through the Mapping Toolbox of this Tag.
</blockquote>


## Apply Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this Tag on your site. The **Load on All Pages** rule is the default load rule. To load this Tag on a specific page, create a new load rule with the relevant conditions.

**Best Practice**: Load this Tag on all pages of your site.

## Set up Data Mappings

[Mapping](https://docs.tealium.com/about-data-mappings/) is the simple process of sending data from a data source, in your Data Layer, to the matching destination variable of the vendor Tag. The destination variables for this Tag are available in the Mapping toolbox.

For instructions on how to map to a Tag's destination, see [Mapping Data Sources](https://docs.tealium.com/about-data-mappings/) article.

**Before You Begin**, we recommend setting up the [E-Commerce Extension](https://docs.tealium.com/e-commerce-extension/) for this Tag. The Extension, if configured, automatically sends the necessary product and order details to the appropriate Tag destinations. You also have the option to override the Extension by mappings those destinations in the Mapping toolbox (see table below).

| Destination Name                   | Destination Variable | Description                                                                                                                                                                 | E-Commerce Extension Mapping<br>  (Recommended) |
|:-----------------------------------|:---------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------|
| Account ID                         | `rb`                 | Numeric identifier of your Rocket Fuel account                                                                                                                              | N/A                                             |
| Action ID                          | `ca`                 | Is the **Conversion** pixel ID when an order ID value is set in the data layer<br>  Is the **Parameterized** pixel ID when an `order id` value is NOT set in the data layer | N/A                                             |
| Type of Action/Page    | `t`                  | (Required) Page types like search, category, cart, et cetera.                                                                                                                          | N/A                                             |
| Transaction ID                     | `transid`            | Unique identifier of the transaction                                                                                                                                        | `_corder` maps to this destination              |
| Revenue                            | `revenue`            | Total order amount including shipping                                                                                                                                       | `_ctotal" maps to this destination              |
| List of Product IDs (ARRAY)        | `pid`                | Unique identifier of each product in the product array                                                                                                                      | `_cprod` array maps to this destination         |
| List of Categories (ARRAY)         | `cat`                | Category of each product in the product array                                                                                                                               | `_ccat` array maps to this destination          |
| List of Product Quantities (ARRAY) | `pq`                 | Quantity of each product in the product array                                                                                                                               | `_cquan` array maps to this destination         |
| List of Product Prices (ARRAY)     | `price`              | Unit price of each product in the product array                                                                                                                             | `_cprice` array maps to this destination        |
| Customer ID                        | `custid`             | Customer's unique identifier                                                                                                                                                | N/A                                             |
| Type of Customer                   | `custtype`           | Additional attribute identifying the customer                                                                                                                               | N/A                                             |
| Start Date of Conversion           | `startdate`          | Date on which the conversion action was initiated                                                                                                                           | N/A                                             |
| End Date of Conversion             | `enddate`            | Date on which the conversion action ended                                                                                                                                   | N/A                                             |
| Product Make                       | `make`               | Product manufacturer                                                                                                                                                        | N/A                                             |
| Product Model                      | `model`              | Product model                                                                                                                                                               | N/A                                             |
| List of Product Name (ARRAY)       | `pname`              | Name of each product in the product array                                                                                                                                   | N/A                                             |
| List of Brands (ARRAY)             | `brand`              | Brand name/title of each product in the product array                                                                                                                       | N/A                                             |
| Product Type                       | `ptype`              | Product classification                                                                                                                                                      | N/A                                             |
| Property Name                      | `propname`           | Name of the property associated with the product                                                                                                                            | N/A                                             |
| Year                               | `year`               | Year in which the order was submitted                                                                                                                                       | N/A                                             |
| Zip                                | `zip`                | Customer's zipcode information                                                                                                                                              | N/A                                             |
| Sign-in Status                     | `status`             | Customer's login status                                                                                                                                                     | N/A                                             |
| Product Group                      | `pgroup`             | Group which the product belongs to                                                                                                                                          | N/A                                             |
| Email Address - Hashed             | `emailh`             | Hash of the customer's email address                                                                                                                                        | N/A                                             |
| Mobile Application ID              | `appid`              | Mobile app's unique identifier                                                                                                                                              | N/A                                             |
| Type of the app activity           | `etype`              | Type of event in the app                                                                                                                                                    | N/A                                             |

### Mapping to Pagetype "t"

Rocket Fuel has predefined the values to be sent for certain page types, as listed in the table below. You will set those values in a data source before mapping it to the `t` destination.

| Page Type      | Value  |
|:---------------|:-------|
| Product View   | `view` |
| Cart/Checkout  | `cv`   |
| Home           | `home` |
| Search Results | `srp`  |
| Category       | `cat`  |


<blockquote>
"Order Confirmation" and "Other" page types do NOT have predefined values.
</blockquote>


Here's how to set the data source:

1. Add a new [Set Data Value Extension](https://docs.tealium.com/set-data-values-extension/) in your profile and scope it to this Tag.
1. From the **Set** drop-down list, select (or add) a **Data Source** whose value you want to send.
1. Keep the **To** dropdown set to **Text**. Enter the predefined value you want to send.
1. Click **Add Condition** and define the evaluating conditions that determine when to set the Data Source.
1. Repeat for every page type that you want to send. Then proceed to map the data source in the Mapping Toolbox.