---
title: Simility Tag Setup Guide
description: This article describes how to set up the Simility tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/simility-tag/
---
## Prerequisites

* Simility account

## Tag Configuration

First, go to the tag marketplace and add the Simility Tag to your profile (See [Add a tag](https://docs.tealium.com/manage-tags/#add-a-tag)).

After adding the tag, configure the below settings:

1. **Customer ID**: The unique identifier that you (or your company) received from Simility during signup. Customer ID is required; you may specify it in this field or set it dynamically with Data Mappings.
1. **Zone**: The location of the datacenter hosting your data. Available options are `US` (default) and `EU`.
1. **Simility Lite**: This is turned ON by default. If you turn it `OFF`, you must send additional user information such as geo-location, mouse movements, etc.
1. **Simility Lite Level**: The numeric (decimal) value you received from the Simility support team.


<blockquote>
**Simility Lite** and **Simility Lite** Level settings are advanced configurations. For more details on these, please contact the Simility support team.
</blockquote>


## Load Rules

[Load Rules](https://docs.tealium.com/about-load-rules/) determine when and where to load an instance of this tag on your site.

## Data Mappings

Mapping is the process of sending data from a [Data Layer Variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a Variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The destination variables for the Simility Tag are built into its Data Mapping tab. Available categories are:

### Standard

| Destination Name     | Description                                                                                                            |
|:---------------------|:-----------------------------------------------------------------------------------------------------------------------|
| Simility Customer ID | (Required) Customer/Account ID provided to you by Simility during signup                                               |
| Simility Lite        | Boolean value (`true`/`false`) to determine whether or not Simility Lite is enabled                                    |
| Simility Lite Level  | The decimal value you received from the Simility support team                                                          |
| Zone                 | The location of the datacenter hosting your data. Make sure the Variable you are mapping contains either `us` or `eu`. |
| Session ID           | (Required) Unique id of the user session                                                                               |
| Event Types          | (Required) A comma-separated string of events associated with the user activity being tracked                          |


<blockquote>
Mapping to a Standard destination overrides its corresponding Tag Setting.
</blockquote>


#### Transaction Info

Lets you send transaction data (for example: user, orders, transactions, applications, profile, et cetera). Data is sent through the `transaction_info` object in the payload.

| Destination Name    | Description                                                                                                                            |
|:--------------------|:---------------------------------------------------------------------------------------------------------------------------------------|
| Entity              | Entity type of the payload; required if using the `transaction_info` object                                                            |
| Transaction ID      | Unique id of the transaction; required if using the `transaction_info` object                                                          |
| First Name          | First name of the user                                                                                                                 |
| Last Name           | Last name of the user                                                                                                                  |
| User ID             | Username of the user                                                                                                                   |
| Email               | Email id of the user                                                                                                                   |
| Is First Order      | Boolean value (`true`/`false`) to determine whether it's the user's first order                                                        |
| Number Of Retries   | Number of attempts to place the order                                                                                                  |
| Custom Field        | Custom data related to the user's transaction. Replace `custom` with your custom parameter name. For example, `field.order_categories` |
| Custom Nested Field | Send transaction data in a nested form. For example, `field.order_details.is_first_order`                                              |

**Example Payload**

Notice how the transaction info mappings are wrapped in the `transaction_info` object whereas all non-transaction mappings are outside the object.

```javascript
var similityContext = {
    "customer_id": "acme",
    "session_id": "1234",
    "user_id" : "user1234",
    "simility_lite": true,
    "transaction_info": [{
      "entity": "orders",
      "id": "xyz101",
      "fields": {
          "first_name": "John",
          "last_name": "Doe",
          "user_id": "user1234",
          "email": "johndoe@example.com",
          "order_categories": ["123", "456", "789"],
          "order_details": { "is_first_order": true, "num_retries": 1 },
       }
   }]
  };
```

### E-Commerce

Since the Simility Tag is e-commerce enabled, it will automatically use the default E-Commerce Extension mappings. Manually mapping in this category is generally not needed unless:

* you want to override any Extension mappings
* an ecommerce variable you want is not offered in the extension

| Destination Name    | Description                    | E-Commerce Extension Variable |
|:--------------------|:-------------------------------|:------------------------------|
| Order ID            | Unique Order ID                | `_corder`                     |
| Order Total         | Total value of order           | `_ctotal`                     |
| Customer ID         | (Required) Unique customer ID. | `_ccustid`                    |
| List of Product IDs | Array of Product IDs           | `_cprod`                      |
| List of Names       | Array of Product Names         | `_cprodname`                  |
| List of Categories  | Array of Product Categories    | `_ccat`                       |
| List of Quantities  | Array of Product Quantities    | `_cquan`                      |
| List of Prices      | Array of Product Prices        | `_cprice`                     |

## Vendor Documentation

* [Simility Javascript](https://simility.com/developer/#devicerecon-javascript)
