---
title: Yandex Metrica Connector Setup Guide
description: This article describes how to set up the Yandex Metrica connector.
url: https://docs.tealium.com/server-side-connectors/yandex-metrica-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Yandex API
* API Version: v1.0
* API Endpoint: `https://api-metrika.yandex.net/cdp/api/v1`
* Documentation: [Yandex API](https://yandex.com/dev/metrika/doc/api2/concept/about.html)

## Batch Limits
  
This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 5 minutes
* Max size of requests: 2 MB

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Order Event | ✗ | ✓ |
| Send Order Event Batch | ✗ | ✓ |
| Upsert Contact | ✓ | ✓ |
| Upsert Contact Batch | ✗ | ✓ |
| Send Page View Event | ✗ | ✓ |
| Send Goal Event | ✓ | ✓ |
| Send Ecommerce Event | ✗ | ✓ |
| Send Advanced Matching Event | ✓ | ✓ |

## Configuration

Navigate to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Bearer Token**:
   * Generate a bearer token by granting Tealium access to the Yandex app using the [Yandex OAuth service](https://oauth.yandex.ru/authorize?response_type=token&client_id=2d25c09a45cc4c7090d6edbb318e65f0).
   * After granting access in the Yandex app, you will be redirected to a page where you can copy the token.
   * Paste the token into the Yandex Metrica connector.
   * The token is valid for one year.
* **Counter ID**:
    The Counter ID for the configuration.

## Actions

The following section lists the supported parameters for each action.

### Send Order Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Update Type | <ul><li>Save - All previously transmitted information is completely replaced with new information.</li><li>Update - Only the information you are currently loading is updated.</li><li>Append - New information is added to the previously downloaded data.</li></ul> |
| ID | <ul><li>(Required) Order ID.</li></ul> |
| Client Unique ID | <ul><li>(Required) ID of the customer in CRM associated with the order.</li></ul> |
| Create Date Time | <ul><li>(Required) The date and time the order was created in the counter's time zone. The value cannot be changed.</li><li>For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).</li></ul> |
| Order Status | <ul><li>(Required) Order status ID.</li><li>Arbitrary string.</li><li>The status can be changed.</li><li>For more information, see [Comparison of order statuses](https://yandex.ru/dev/metrika/doc/api2/crm/schema/maporderstatuses.html).</li><li>Default possible values: **PAID**, **IN_PROGRESS**, **CANCELLED**, **SPAM**.</li><li>Additional values you create are accepted. </li></ul> |
| Update Date Time | <ul><li>The date and time the order was updated in the counter's time zone.</li><li>If the parameter is not passed, the value is substituted automatically.</li><li>For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).</li></ul> |
| Finish Date Time | <ul><li>The date and time the order was completed in the counter's time zone.</li><li>For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).</li></ul> |
| Revenue | <ul><li>Income - The total cost of the order.</li><li>Decimal - Transfer the proceeds from the order.</li><li>This value will be used in [End-to-End Analytics](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders) reports to show the income from advertising channels.</li><li>The value will be shown in the **Revenue** metric.</li></ul> |
| Cost | <ul><li>Cost price.</li><li>You can pass the cost of orders to take profit into account in [End-to-End Analytics](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders) reports.</li><li>Profit will be calculated using the formula: `Revenue - Cost`. |
| Product IDs | <ul><li>(Required) Pass product identifiers and their quantity in the object.</li><li>Identifiers will be available when creating a segment in Metrica if you do not transfer lists of products.</li><li>If you [create lists of products](https://yandex.ru/dev/metrika/doc/api2/crm/schema/createproducts.html), then data from these lists will be available in Yandex Metrica.</li><li> For example, `{"Product A" : 173, "Product B" : 146}`.</li></ul> |
| Product Quantities | <ul><li>(Required) Product quantities.</li></ul> |
| Attribute Values | <ul><li>Attributes to be customized and passed in the specified order.</li></ul> |

### Send Order Event Batch

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Update Type | <ul><li>Save - All previously transmitted information is completely replaced with new information.</li><li>Update - Only the information you are currently loading is updated.</li><li>Append - New information is added to the previously downloaded data.</li></ul> |
| ID | <ul><li>(Required) Order ID.</li></ul> |
| Client Unique ID | <ul><li>(Required) ID of the customer in CRM associated with the order.</li></ul> |
| Create Date Time | <ul><li>(Required) The date and time the order was created in the counter's time zone. The value cannot be changed.</li><li>For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).</li><li>For example, `2023-04-21 10:00:00`.</li></ul> |
| Order Status | <ul><li>(Required) Order status ID.</li><li>Arbitrary string.</li><li>The status can be changed.</li><li>Specify the value you passed when [matching statuses in the id field](https://yandex.ru/dev/metrika/doc/api2/crm/schema/maporderstatuses.html).</li><li>Default possible values: PAID, IN_PROGRESS, CANCELLED, SPAM.</li><li>The user can create additional values, therefore other values must be accepted.</li></ul> |
| Update Date Time | <ul><li>The date and time the order was updated in the counter's time zone.</li><li>If the parameter is not passed, the value is substituted automatically.</li><li>For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).</li></ul> |
| Finish Date Time | <ul><li>The date and time the order was completed in the counter's time zone.</li><li>For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).</li></ul> |
| Revenue | <ul><li>Income - The total cost of the order.</li><li>Decimal - Transfer the proceeds from the order.</li><li>This value will be used in [End-to-End Analytics](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders) reports to show the income from advertising channels.</li><li>The value will be shown in the Revenue metric.</li></ul> |
| Cost | <ul><li>Cost price.</li><li>You can pass the cost of orders to take profit into account in [End-to-End Analytics](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders) reports.</li><li>Profit will be calculated using the formula: `Revenue - Cost`.</li></ul> |
| Product IDs | <ul><li>(Required) Pass product identifiers and their quantity in the object.</li><li>Identifiers will be available when creating a segment in Metrica if you do not transfer lists of products.</li><li>If you [create lists of products](https://yandex.ru/dev/metrika/doc/api2/crm/schema/createproducts.html), then data from these lists will be available in Yandex Metrica.</li><li> For example, `{"Product A" : 173, "Product B" : 146}`.</li></ul> |
| Product Quantities | <ul><li>(Required) Product quantities.</li></ul> |
| Attribute Values | <ul><li>Attributes to be customized and passed in the specified order.</li></ul> |

### Upsert Contact

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Update Type | <ul><li>Save - All previously transmitted information is completely replaced with new information.</li><li>Update - Only the information you are currently loading is updated.</li><li>Append - New information is added to the previously downloaded data.</li></ul> |
| Unique ID | <ul><li>(Required) Custom client ID. It can be a `customer_id` or the `tealium_visitor_id`.</li></ul> |
| Client ID | <ul><li>Yandex Metrika Client ID (`_ym_uid`).</li></ul> |
| Name | <ul><li>Client name.</li><li>If you provide the last name, first name, and patronymic, the line will be condensed into the format **John S**, where **S** is the truncated last name.</li></ul> |
| Create Date Time | <ul><li>The date and time the contact was created in the counter's time zone.</li><li>The value cannot be changed.</li><li>For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).</li></ul> |
| Update Date Time | <ul><li>The date and time the contact was updated in the counter's time zone.</li><li>If the parameter is not passed, the value is substituted automatically.</li><li>For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).</li></ul> |
| Client IDs | <ul><li>List of client IDs.</li></ul> |
| Emails | <ul><li>List of client email addresses.</li></ul> |
| Phones | <ul><li>List of client phone numbers.</li></ul> |
| Emails MD5 | <ul><li>List of client email addresses, [hashed in MD5 format](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing).</li><li>Normalize email addresses before hashing by converting text to lowercase and removing leading/trailing spaces and commas. </li><li>For Google domain addresses, remove dots in the username. For example, convert `name.example@gmail.com` to `nameexample@gmail.com`.</li><li>For Yandex domain addresses, replace dots in the username with dashes. For example, convert `name.example@yandex.ru` to `name-example@yandex.ru`.</li><li>For addresses on multiple Yandex domains such `@ya.ru` or `@yandex.com`, standardize them to `@yandex.ru`. For example, change `example@@ya.ru` to `example@yandex.ru`.</li><li>If the email address contains a `+` sign such as `name+commercial@example.com`, retain only the name before `+`: `name@example.com`.</li></ul> |
| Phones MD5 | <ul><li>List of customer phone numbers, [hashed in MD5 format](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing).</li><li>Enter the number with the country code excluding the `+` sign.</li><li>Normalize phone numbers before hashing.</li><li>Convert text to lowercase.</li><li>Remove leading/trailing spaces and commas.</li><li>Use only digits.</li><li>For example, `70123456789`.</li></ul> |
| Attribute Values | <ul><li>Attributes to be customized and passed in the specified order.</li></ul> |

### Upsert Contact Batch

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Update Type | <ul><li>Save - All previously transmitted information is completely replaced with new information.</li><li>Update - Only the information you are currently loading is updated.</li><li>Append - New information is added to the previously downloaded data.</li></ul> |
| Unique ID | <ul><li>(Required) Custom client ID. It can be a `customer_id` or the `tealium_visitor_id`.</li></ul> |
| Client ID | <ul><li>(Required) Yandex Metrika Client ID (`_ym_uid`).</li></ul> |
| Name | <ul><li>Client name.</li><li>If you provide the last name, first name, and patronymic, the line will be condensed into the format **John S**, where **S** is the truncated last name.</li></ul> |
| Create Date Time | <ul><li>The date and time the contact was created in the counter's time zone.</li><li>The value cannot be changed.</li><li>For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).</li></ul> |
| Update Date Time | <ul><li>The date and time the contact was updated in the counter's time zone.</li><li>If the parameter is not passed, the value is substituted automatically.</li><li>For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).</li></ul> |
| Client IDs | <ul><li>List of client IDs.</li></ul> |
| Emails | <ul><li>List of client email addresses.</li></ul> |
| Phones | <ul><li>List of client phone numbers.</li></ul> |
| Emails MD5 | <ul><li>List of client email addresses, [hashed in MD5 format](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing).</li><li>Normalize email addresses before hashing.</li><li>Convert text to lowercase.</li><li>Remove leading/trailing spaces and commas.</li><li>For Google domain addresses, remove dots in the username. For example, convert `name.example@gmail.com` to `nameexample@gmail.com`.</li><li>For Yandex domain addresses, replace dots in the username with dashes. For example, convert `name.example@yandex.ru` to `name-example@yandex.ru`.</li><li>For addresses on multiple Yandex domains such `@ya.ru` or `@yandex.com`, standardize them to `@yandex.ru`. For example, change `example@@ya.ru` to `example@yandex.ru`.</li><li>If the email address contains a `+` sign such as `name+commercial@example.com`, retain only the name before `+`: `name@example.com`.</li></ul> |
| Phones MD5 | <ul><li>List of customer phone numbers, [hashed in MD5 format](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing).</li><li>Enter the number with the country code excluding the `+` sign.</li><li>Normalize phone numbers before hashing.</li><li>Convert text to lowercase.</li><li>Remove leading/trailing spaces and commas.</li><li>Use only digits.</li><li>For example, `70123456789`.</li></ul> |
| Attribute Values | <ul><li>Attributes to be customized and passed in the specified order.</li></ul> |

### Send Page View Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Page Url | <ul><li>Current URL</li></ul> |
| Yandex Client ID | <ul><li>(Required) Yandex Metrica Client ID (`_ym_uid`).</li></ul> |
| Page Ref | <ul><li>Referral URL. If empty, the default URL is `https://tealium.com`.</li></ul> |
| Site Info | <ul><li>Custom object.</li></ul> |
| Custom Query Parameters | <ul><li>Additional custom query parameters.</li></ul> |

### Create a new session

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Page Url | <ul><li>Current URL</li></ul> |
| Yandex Client ID | <ul><li>(Required) Yandex Metrica Client ID (`_ym_uid`).</li></ul> |
| Page Ref | <ul><li>Referral URL. If empty, the default URL is `https://tealium.com`.</li></ul> |
| Site Info | <ul><li>Custom object.</li></ul> |
| Custom Query Parameters | <ul><li>Additional custom query parameters.</li></ul> |

### Send Goal Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Trigger Open Session Call | <ul><li>Yandex Metrica requires an open session call before triggering the **Send Goal Event** action.</li></ul> |
| Site Domain | <ul><li>(Required) The site domain.</li></ul> |
| Goal ID | <ul><li>(Required) The goal number.</li></ul> |
| Yandex Client ID | <ul><li>(Required) Yandex Metrica Client ID (`_ym_uid`)</li></ul> |
| Page Ref | <ul><li>Referral URL. If empty, the default URL is `https://tealium.com`.</li></ul> |
| Site Info | <ul><li>Custom object.</li></ul> |
| Custom Query Parameters | <ul><li>Additional custom query parameters.</li></ul> |

### Send Ecommerce Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Trigger Open Session Call | <ul><li>Yandex Metrica requires an open session call before triggering the **Send Ecommerce Event** action.</li></ul> |
| Page Url | <ul><li>Referral URL. If empty, the default URL is `https://tealium.com`.</li></ul> |
| Yandex Client ID | <ul><li>(Required) Yandex Metrica Client ID (`_ym_uid`).</li></ul> |
| Action Type | <ul><li>The field name, which replaces `actionType`, serves as the identifier for an action performed with a set of products.</li><li>Possible values:</li><li>Detail: View the full item description (product card).</li><li>Add: Add an item to the basket.</li><li>Remove: Remove an item from the basket.</li><li> Purchase: Purchase an item.</li><li>If information about removing the item was transmitted to Yandex Metrica, the report might show a negative number of items (the total is calculated by subtracting the number of deleted items from the total number of added items). If the price of the item was transmitted, it might also have a negative value in the report.</li></ul> |
| Currency Code | <ul><li>Three-letter [ISO 4217 currency code](https://www.six-group.com/en/products-services/financial-information/data-standards.html#scrollTo=currency-codes).</li><li>If a different currency is passed, null values will be sent instead of currencies and amounts.</li></ul> |
| ID | <ul><li>ID of the product purchased.</li></ul> |
| Coupon | <ul><li>A promo code associated with the entire purchase.</li></ul> |
| Goal ID | <ul><li>The [goal](https://yandex.ru/support/metrica/general/goals.html) number.</li><li>Specified if the **Send Ecommerce Event** [action](https://yandex.ru/support/metrica/ecommerce/data.html#about__action_type) was the goal.</li><li>The goal must be set as a [JavaScript event](https://yandex.ru/support/metrica/general/goal-js-event.html) type.</li><li>To see the goal number, go to the **Goals** tab and select **Settings** in the Yandex Metrica dashboard.</li></ul> |
| Revenue | <ul><li>The revenue received.</li><li>If omitted, it is calculated automatically as the sum of the prices of all the items associated with the purchase.</li></ul> |
| ID | <ul><li>Item ID.</li><li>For example, the SKU.</li><li>You must specify either **Name** or **ID**.</li></ul> |
| Name | <ul><li>Name of the product.</li><li> For example, **T-shirt**.</li><li>You must specify either **Name** or **ID**.</li></ul> |
| Brand | <ul><li>The brand or trademark associated with the item.</li><li>For example, **Yandex**.</li></ul> |
| Category | <ul><li>The category the item belongs to.</li><li>The hierarchy of categories supports up to 5 nesting levels. Use the `/` symbol to separate levels.</li><li>For example, **Clothing/Men's**, **clothing/T-shirts**.</li></ul> |
| Coupon | <ul><li>A promo code associated with the item.</li><li>For example, `PARTNER_SITE_15.`</li></ul> |
| Position | <ul><li>Position of the item in the list.</li><li>For example, `2`.</li></ul> |
| Price | <ul><li>Price of a product unit.</li></ul> |
| Quantity | <ul><li>Quantity of product units.</li></ul> |
| Variant | <ul><li>A variation of the item.</li><li>For example, **Red**.</li></ul> |
| Custom Query Parameters | <ul><li>Additional custom query parameters.</li></ul> |

### Send Advanced Matching Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Trigger Open Session Call | Yandex Metrica requires an open session call before triggering the **Send Advanced Matching Event** action. |
| Page Url | Referral URL. If empty, the default URL is `https://tealium.com`. |
| Yandex Client ID | (Required) Yandex Metrica Client ID (`_ym_uid`). |
| MD5 Hashed | Select if value is MD5 hashed. |
| Email | User's email address. |
| Phone Number | Enter the phone number including the country code, without the `+` symbol and spaces. For example, `70123456789`. |
| First Name | User's first name. |
| Last Name | User's last name. |
| Street | Street. |
| City | City. |
| Region | Region. |
| Postal Code | Accepts any integer. |
| Country | Accepts any string. |
| Custom Query Parameters | Additional custom query parameters. |

