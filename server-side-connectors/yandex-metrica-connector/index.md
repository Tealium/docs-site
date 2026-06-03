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
  
This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

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

Navigate to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Bearer Token**:
   * Generate a bearer token by granting Tealium access to the Yandex app using the [Yandex OAuth service](https://oauth.yandex.ru/authorize?response_type=token&amp;client_id=2d25c09a45cc4c7090d6edbb318e65f0).
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
| Update Type | &lt;ul&gt;&lt;li&gt;Save - All previously transmitted information is completely replaced with new information.&lt;/li&gt;&lt;li&gt;Update - Only the information you are currently loading is updated.&lt;/li&gt;&lt;li&gt;Append - New information is added to the previously downloaded data.&lt;/li&gt;&lt;/ul&gt; |
| ID | &lt;ul&gt;&lt;li&gt;(Required) Order ID.&lt;/li&gt;&lt;/ul&gt; |
| Client Unique ID | &lt;ul&gt;&lt;li&gt;(Required) ID of the customer in CRM associated with the order.&lt;/li&gt;&lt;/ul&gt; |
| Create Date Time | &lt;ul&gt;&lt;li&gt;(Required) The date and time the order was created in the counter&#39;s time zone. The value cannot be changed.&lt;/li&gt;&lt;li&gt;For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).&lt;/li&gt;&lt;/ul&gt; |
| Order Status | &lt;ul&gt;&lt;li&gt;(Required) Order status ID.&lt;/li&gt;&lt;li&gt;Arbitrary string.&lt;/li&gt;&lt;li&gt;The status can be changed.&lt;/li&gt;&lt;li&gt;For more information, see [Comparison of order statuses](https://yandex.ru/dev/metrika/doc/api2/crm/schema/maporderstatuses.html).&lt;/li&gt;&lt;li&gt;Default possible values: **PAID**, **IN_PROGRESS**, **CANCELLED**, **SPAM**.&lt;/li&gt;&lt;li&gt;Additional values you create are accepted. &lt;/li&gt;&lt;/ul&gt; |
| Update Date Time | &lt;ul&gt;&lt;li&gt;The date and time the order was updated in the counter&#39;s time zone.&lt;/li&gt;&lt;li&gt;If the parameter is not passed, the value is substituted automatically.&lt;/li&gt;&lt;li&gt;For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).&lt;/li&gt;&lt;/ul&gt; |
| Finish Date Time | &lt;ul&gt;&lt;li&gt;The date and time the order was completed in the counter&#39;s time zone.&lt;/li&gt;&lt;li&gt;For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).&lt;/li&gt;&lt;/ul&gt; |
| Revenue | &lt;ul&gt;&lt;li&gt;Income - The total cost of the order.&lt;/li&gt;&lt;li&gt;Decimal - Transfer the proceeds from the order.&lt;/li&gt;&lt;li&gt;This value will be used in [End-to-End Analytics](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders) reports to show the income from advertising channels.&lt;/li&gt;&lt;li&gt;The value will be shown in the **Revenue** metric.&lt;/li&gt;&lt;/ul&gt; |
| Cost | &lt;ul&gt;&lt;li&gt;Cost price.&lt;/li&gt;&lt;li&gt;You can pass the cost of orders to take profit into account in [End-to-End Analytics](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders) reports.&lt;/li&gt;&lt;li&gt;Profit will be calculated using the formula: `Revenue - Cost`. |
| Product IDs | &lt;ul&gt;&lt;li&gt;(Required) Pass product identifiers and their quantity in the object.&lt;/li&gt;&lt;li&gt;Identifiers will be available when creating a segment in Metrica if you do not transfer lists of products.&lt;/li&gt;&lt;li&gt;If you [create lists of products](https://yandex.ru/dev/metrika/doc/api2/crm/schema/createproducts.html), then data from these lists will be available in Yandex Metrica.&lt;/li&gt;&lt;li&gt; For example, `{&#34;Product A&#34; : 173, &#34;Product B&#34; : 146}`.&lt;/li&gt;&lt;/ul&gt; |
| Product Quantities | &lt;ul&gt;&lt;li&gt;(Required) Product quantities.&lt;/li&gt;&lt;/ul&gt; |
| Attribute Values | &lt;ul&gt;&lt;li&gt;Attributes to be customized and passed in the specified order.&lt;/li&gt;&lt;/ul&gt; |

### Send Order Event Batch

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Update Type | &lt;ul&gt;&lt;li&gt;Save - All previously transmitted information is completely replaced with new information.&lt;/li&gt;&lt;li&gt;Update - Only the information you are currently loading is updated.&lt;/li&gt;&lt;li&gt;Append - New information is added to the previously downloaded data.&lt;/li&gt;&lt;/ul&gt; |
| ID | &lt;ul&gt;&lt;li&gt;(Required) Order ID.&lt;/li&gt;&lt;/ul&gt; |
| Client Unique ID | &lt;ul&gt;&lt;li&gt;(Required) ID of the customer in CRM associated with the order.&lt;/li&gt;&lt;/ul&gt; |
| Create Date Time | &lt;ul&gt;&lt;li&gt;(Required) The date and time the order was created in the counter&#39;s time zone. The value cannot be changed.&lt;/li&gt;&lt;li&gt;For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).&lt;/li&gt;&lt;li&gt;For example, `2023-04-21 10:00:00`.&lt;/li&gt;&lt;/ul&gt; |
| Order Status | &lt;ul&gt;&lt;li&gt;(Required) Order status ID.&lt;/li&gt;&lt;li&gt;Arbitrary string.&lt;/li&gt;&lt;li&gt;The status can be changed.&lt;/li&gt;&lt;li&gt;Specify the value you passed when [matching statuses in the id field](https://yandex.ru/dev/metrika/doc/api2/crm/schema/maporderstatuses.html).&lt;/li&gt;&lt;li&gt;Default possible values: PAID, IN_PROGRESS, CANCELLED, SPAM.&lt;/li&gt;&lt;li&gt;The user can create additional values, therefore other values must be accepted.&lt;/li&gt;&lt;/ul&gt; |
| Update Date Time | &lt;ul&gt;&lt;li&gt;The date and time the order was updated in the counter&#39;s time zone.&lt;/li&gt;&lt;li&gt;If the parameter is not passed, the value is substituted automatically.&lt;/li&gt;&lt;li&gt;For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).&lt;/li&gt;&lt;/ul&gt; |
| Finish Date Time | &lt;ul&gt;&lt;li&gt;The date and time the order was completed in the counter&#39;s time zone.&lt;/li&gt;&lt;li&gt;For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).&lt;/li&gt;&lt;/ul&gt; |
| Revenue | &lt;ul&gt;&lt;li&gt;Income - The total cost of the order.&lt;/li&gt;&lt;li&gt;Decimal - Transfer the proceeds from the order.&lt;/li&gt;&lt;li&gt;This value will be used in [End-to-End Analytics](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders) reports to show the income from advertising channels.&lt;/li&gt;&lt;li&gt;The value will be shown in the Revenue metric.&lt;/li&gt;&lt;/ul&gt; |
| Cost | &lt;ul&gt;&lt;li&gt;Cost price.&lt;/li&gt;&lt;li&gt;You can pass the cost of orders to take profit into account in [End-to-End Analytics](https://yandex.ru/dev/metrika/doc/api2/api_v1/presets/preset_crm_orders.html#preset_cdp_orders) reports.&lt;/li&gt;&lt;li&gt;Profit will be calculated using the formula: `Revenue - Cost`.&lt;/li&gt;&lt;/ul&gt; |
| Product IDs | &lt;ul&gt;&lt;li&gt;(Required) Pass product identifiers and their quantity in the object.&lt;/li&gt;&lt;li&gt;Identifiers will be available when creating a segment in Metrica if you do not transfer lists of products.&lt;/li&gt;&lt;li&gt;If you [create lists of products](https://yandex.ru/dev/metrika/doc/api2/crm/schema/createproducts.html), then data from these lists will be available in Yandex Metrica.&lt;/li&gt;&lt;li&gt; For example, `{&#34;Product A&#34; : 173, &#34;Product B&#34; : 146}`.&lt;/li&gt;&lt;/ul&gt; |
| Product Quantities | &lt;ul&gt;&lt;li&gt;(Required) Product quantities.&lt;/li&gt;&lt;/ul&gt; |
| Attribute Values | &lt;ul&gt;&lt;li&gt;Attributes to be customized and passed in the specified order.&lt;/li&gt;&lt;/ul&gt; |

### Upsert Contact

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Update Type | &lt;ul&gt;&lt;li&gt;Save - All previously transmitted information is completely replaced with new information.&lt;/li&gt;&lt;li&gt;Update - Only the information you are currently loading is updated.&lt;/li&gt;&lt;li&gt;Append - New information is added to the previously downloaded data.&lt;/li&gt;&lt;/ul&gt; |
| Unique ID | &lt;ul&gt;&lt;li&gt;(Required) Custom client ID. It can be a `customer_id` or the `tealium_visitor_id`.&lt;/li&gt;&lt;/ul&gt; |
| Client ID | &lt;ul&gt;&lt;li&gt;Yandex Metrika Client ID (`_ym_uid`).&lt;/li&gt;&lt;/ul&gt; |
| Name | &lt;ul&gt;&lt;li&gt;Client name.&lt;/li&gt;&lt;li&gt;If you provide the last name, first name, and patronymic, the line will be condensed into the format **John S**, where **S** is the truncated last name.&lt;/li&gt;&lt;/ul&gt; |
| Create Date Time | &lt;ul&gt;&lt;li&gt;The date and time the contact was created in the counter&#39;s time zone.&lt;/li&gt;&lt;li&gt;The value cannot be changed.&lt;/li&gt;&lt;li&gt;For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).&lt;/li&gt;&lt;/ul&gt; |
| Update Date Time | &lt;ul&gt;&lt;li&gt;The date and time the contact was updated in the counter&#39;s time zone.&lt;/li&gt;&lt;li&gt;If the parameter is not passed, the value is substituted automatically.&lt;/li&gt;&lt;li&gt;For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).&lt;/li&gt;&lt;/ul&gt; |
| Client IDs | &lt;ul&gt;&lt;li&gt;List of client IDs.&lt;/li&gt;&lt;/ul&gt; |
| Emails | &lt;ul&gt;&lt;li&gt;List of client email addresses.&lt;/li&gt;&lt;/ul&gt; |
| Phones | &lt;ul&gt;&lt;li&gt;List of client phone numbers.&lt;/li&gt;&lt;/ul&gt; |
| Emails MD5 | &lt;ul&gt;&lt;li&gt;List of client email addresses, [hashed in MD5 format](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing).&lt;/li&gt;&lt;li&gt;Normalize email addresses before hashing by converting text to lowercase and removing leading/trailing spaces and commas. &lt;/li&gt;&lt;li&gt;For Google domain addresses, remove dots in the username. For example, convert `name.example@gmail.com` to `nameexample@gmail.com`.&lt;/li&gt;&lt;li&gt;For Yandex domain addresses, replace dots in the username with dashes. For example, convert `name.example@yandex.ru` to `name-example@yandex.ru`.&lt;/li&gt;&lt;li&gt;For addresses on multiple Yandex domains such `@ya.ru` or `@yandex.com`, standardize them to `@yandex.ru`. For example, change `example@@ya.ru` to `example@yandex.ru`.&lt;/li&gt;&lt;li&gt;If the email address contains a `&#43;` sign such as `name&#43;commercial@example.com`, retain only the name before `&#43;`: `name@example.com`.&lt;/li&gt;&lt;/ul&gt; |
| Phones MD5 | &lt;ul&gt;&lt;li&gt;List of customer phone numbers, [hashed in MD5 format](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing).&lt;/li&gt;&lt;li&gt;Enter the number with the country code excluding the `&#43;` sign.&lt;/li&gt;&lt;li&gt;Normalize phone numbers before hashing.&lt;/li&gt;&lt;li&gt;Convert text to lowercase.&lt;/li&gt;&lt;li&gt;Remove leading/trailing spaces and commas.&lt;/li&gt;&lt;li&gt;Use only digits.&lt;/li&gt;&lt;li&gt;For example, `70123456789`.&lt;/li&gt;&lt;/ul&gt; |
| Attribute Values | &lt;ul&gt;&lt;li&gt;Attributes to be customized and passed in the specified order.&lt;/li&gt;&lt;/ul&gt; |

### Upsert Contact Batch

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Update Type | &lt;ul&gt;&lt;li&gt;Save - All previously transmitted information is completely replaced with new information.&lt;/li&gt;&lt;li&gt;Update - Only the information you are currently loading is updated.&lt;/li&gt;&lt;li&gt;Append - New information is added to the previously downloaded data.&lt;/li&gt;&lt;/ul&gt; |
| Unique ID | &lt;ul&gt;&lt;li&gt;(Required) Custom client ID. It can be a `customer_id` or the `tealium_visitor_id`.&lt;/li&gt;&lt;/ul&gt; |
| Client ID | &lt;ul&gt;&lt;li&gt;(Required) Yandex Metrika Client ID (`_ym_uid`).&lt;/li&gt;&lt;/ul&gt; |
| Name | &lt;ul&gt;&lt;li&gt;Client name.&lt;/li&gt;&lt;li&gt;If you provide the last name, first name, and patronymic, the line will be condensed into the format **John S**, where **S** is the truncated last name.&lt;/li&gt;&lt;/ul&gt; |
| Create Date Time | &lt;ul&gt;&lt;li&gt;The date and time the contact was created in the counter&#39;s time zone.&lt;/li&gt;&lt;li&gt;The value cannot be changed.&lt;/li&gt;&lt;li&gt;For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).&lt;/li&gt;&lt;/ul&gt; |
| Update Date Time | &lt;ul&gt;&lt;li&gt;The date and time the contact was updated in the counter&#39;s time zone.&lt;/li&gt;&lt;li&gt;If the parameter is not passed, the value is substituted automatically.&lt;/li&gt;&lt;li&gt;For more information, see the [Date and time format](https://yandex.ru/dev/metrika/doc/api2/crm/date.html#orders).&lt;/li&gt;&lt;/ul&gt; |
| Client IDs | &lt;ul&gt;&lt;li&gt;List of client IDs.&lt;/li&gt;&lt;/ul&gt; |
| Emails | &lt;ul&gt;&lt;li&gt;List of client email addresses.&lt;/li&gt;&lt;/ul&gt; |
| Phones | &lt;ul&gt;&lt;li&gt;List of client phone numbers.&lt;/li&gt;&lt;/ul&gt; |
| Emails MD5 | &lt;ul&gt;&lt;li&gt;List of client email addresses, [hashed in MD5 format](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing).&lt;/li&gt;&lt;li&gt;Normalize email addresses before hashing.&lt;/li&gt;&lt;li&gt;Convert text to lowercase.&lt;/li&gt;&lt;li&gt;Remove leading/trailing spaces and commas.&lt;/li&gt;&lt;li&gt;For Google domain addresses, remove dots in the username. For example, convert `name.example@gmail.com` to `nameexample@gmail.com`.&lt;/li&gt;&lt;li&gt;For Yandex domain addresses, replace dots in the username with dashes. For example, convert `name.example@yandex.ru` to `name-example@yandex.ru`.&lt;/li&gt;&lt;li&gt;For addresses on multiple Yandex domains such `@ya.ru` or `@yandex.com`, standardize them to `@yandex.ru`. For example, change `example@@ya.ru` to `example@yandex.ru`.&lt;/li&gt;&lt;li&gt;If the email address contains a `&#43;` sign such as `name&#43;commercial@example.com`, retain only the name before `&#43;`: `name@example.com`.&lt;/li&gt;&lt;/ul&gt; |
| Phones MD5 | &lt;ul&gt;&lt;li&gt;List of customer phone numbers, [hashed in MD5 format](https://yandex.ru/dev/metrika/doc/api2/practice/crm/hashing.html#hashing).&lt;/li&gt;&lt;li&gt;Enter the number with the country code excluding the `&#43;` sign.&lt;/li&gt;&lt;li&gt;Normalize phone numbers before hashing.&lt;/li&gt;&lt;li&gt;Convert text to lowercase.&lt;/li&gt;&lt;li&gt;Remove leading/trailing spaces and commas.&lt;/li&gt;&lt;li&gt;Use only digits.&lt;/li&gt;&lt;li&gt;For example, `70123456789`.&lt;/li&gt;&lt;/ul&gt; |
| Attribute Values | &lt;ul&gt;&lt;li&gt;Attributes to be customized and passed in the specified order.&lt;/li&gt;&lt;/ul&gt; |

### Send Page View Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Page Url | &lt;ul&gt;&lt;li&gt;Current URL&lt;/li&gt;&lt;/ul&gt; |
| Yandex Client ID | &lt;ul&gt;&lt;li&gt;(Required) Yandex Metrica Client ID (`_ym_uid`).&lt;/li&gt;&lt;/ul&gt; |
| Page Ref | &lt;ul&gt;&lt;li&gt;Referral URL. If empty, the default URL is `https://tealium.com`.&lt;/li&gt;&lt;/ul&gt; |
| Site Info | &lt;ul&gt;&lt;li&gt;Custom object.&lt;/li&gt;&lt;/ul&gt; |
| Custom Query Parameters | &lt;ul&gt;&lt;li&gt;Additional custom query parameters.&lt;/li&gt;&lt;/ul&gt; |

### Create a new session

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Page Url | &lt;ul&gt;&lt;li&gt;Current URL&lt;/li&gt;&lt;/ul&gt; |
| Yandex Client ID | &lt;ul&gt;&lt;li&gt;(Required) Yandex Metrica Client ID (`_ym_uid`).&lt;/li&gt;&lt;/ul&gt; |
| Page Ref | &lt;ul&gt;&lt;li&gt;Referral URL. If empty, the default URL is `https://tealium.com`.&lt;/li&gt;&lt;/ul&gt; |
| Site Info | &lt;ul&gt;&lt;li&gt;Custom object.&lt;/li&gt;&lt;/ul&gt; |
| Custom Query Parameters | &lt;ul&gt;&lt;li&gt;Additional custom query parameters.&lt;/li&gt;&lt;/ul&gt; |

### Send Goal Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Trigger Open Session Call | &lt;ul&gt;&lt;li&gt;Yandex Metrica requires an open session call before triggering the **Send Goal Event** action.&lt;/li&gt;&lt;/ul&gt; |
| Site Domain | &lt;ul&gt;&lt;li&gt;(Required) The site domain.&lt;/li&gt;&lt;/ul&gt; |
| Goal ID | &lt;ul&gt;&lt;li&gt;(Required) The goal number.&lt;/li&gt;&lt;/ul&gt; |
| Yandex Client ID | &lt;ul&gt;&lt;li&gt;(Required) Yandex Metrica Client ID (`_ym_uid`)&lt;/li&gt;&lt;/ul&gt; |
| Page Ref | &lt;ul&gt;&lt;li&gt;Referral URL. If empty, the default URL is `https://tealium.com`.&lt;/li&gt;&lt;/ul&gt; |
| Site Info | &lt;ul&gt;&lt;li&gt;Custom object.&lt;/li&gt;&lt;/ul&gt; |
| Custom Query Parameters | &lt;ul&gt;&lt;li&gt;Additional custom query parameters.&lt;/li&gt;&lt;/ul&gt; |

### Send Ecommerce Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Trigger Open Session Call | &lt;ul&gt;&lt;li&gt;Yandex Metrica requires an open session call before triggering the **Send Ecommerce Event** action.&lt;/li&gt;&lt;/ul&gt; |
| Page Url | &lt;ul&gt;&lt;li&gt;Referral URL. If empty, the default URL is `https://tealium.com`.&lt;/li&gt;&lt;/ul&gt; |
| Yandex Client ID | &lt;ul&gt;&lt;li&gt;(Required) Yandex Metrica Client ID (`_ym_uid`).&lt;/li&gt;&lt;/ul&gt; |
| Action Type | &lt;ul&gt;&lt;li&gt;The field name, which replaces `actionType`, serves as the identifier for an action performed with a set of products.&lt;/li&gt;&lt;li&gt;Possible values:&lt;/li&gt;&lt;li&gt;Detail: View the full item description (product card).&lt;/li&gt;&lt;li&gt;Add: Add an item to the basket.&lt;/li&gt;&lt;li&gt;Remove: Remove an item from the basket.&lt;/li&gt;&lt;li&gt; Purchase: Purchase an item.&lt;/li&gt;&lt;li&gt;If information about removing the item was transmitted to Yandex Metrica, the report might show a negative number of items (the total is calculated by subtracting the number of deleted items from the total number of added items). If the price of the item was transmitted, it might also have a negative value in the report.&lt;/li&gt;&lt;/ul&gt; |
| Currency Code | &lt;ul&gt;&lt;li&gt;Three-letter [ISO 4217 currency code](https://www.six-group.com/en/products-services/financial-information/data-standards.html#scrollTo=currency-codes).&lt;/li&gt;&lt;li&gt;If a different currency is passed, null values will be sent instead of currencies and amounts.&lt;/li&gt;&lt;/ul&gt; |
| ID | &lt;ul&gt;&lt;li&gt;ID of the product purchased.&lt;/li&gt;&lt;/ul&gt; |
| Coupon | &lt;ul&gt;&lt;li&gt;A promo code associated with the entire purchase.&lt;/li&gt;&lt;/ul&gt; |
| Goal ID | &lt;ul&gt;&lt;li&gt;The [goal](https://yandex.ru/support/metrica/general/goals.html) number.&lt;/li&gt;&lt;li&gt;Specified if the **Send Ecommerce Event** [action](https://yandex.ru/support/metrica/ecommerce/data.html#about__action_type) was the goal.&lt;/li&gt;&lt;li&gt;The goal must be set as a [JavaScript event](https://yandex.ru/support/metrica/general/goal-js-event.html) type.&lt;/li&gt;&lt;li&gt;To see the goal number, go to the **Goals** tab and select **Settings** in the Yandex Metrica dashboard.&lt;/li&gt;&lt;/ul&gt; |
| Revenue | &lt;ul&gt;&lt;li&gt;The revenue received.&lt;/li&gt;&lt;li&gt;If omitted, it is calculated automatically as the sum of the prices of all the items associated with the purchase.&lt;/li&gt;&lt;/ul&gt; |
| ID | &lt;ul&gt;&lt;li&gt;Item ID.&lt;/li&gt;&lt;li&gt;For example, the SKU.&lt;/li&gt;&lt;li&gt;You must specify either **Name** or **ID**.&lt;/li&gt;&lt;/ul&gt; |
| Name | &lt;ul&gt;&lt;li&gt;Name of the product.&lt;/li&gt;&lt;li&gt; For example, **T-shirt**.&lt;/li&gt;&lt;li&gt;You must specify either **Name** or **ID**.&lt;/li&gt;&lt;/ul&gt; |
| Brand | &lt;ul&gt;&lt;li&gt;The brand or trademark associated with the item.&lt;/li&gt;&lt;li&gt;For example, **Yandex**.&lt;/li&gt;&lt;/ul&gt; |
| Category | &lt;ul&gt;&lt;li&gt;The category the item belongs to.&lt;/li&gt;&lt;li&gt;The hierarchy of categories supports up to 5 nesting levels. Use the `/` symbol to separate levels.&lt;/li&gt;&lt;li&gt;For example, **Clothing/Men&#39;s**, **clothing/T-shirts**.&lt;/li&gt;&lt;/ul&gt; |
| Coupon | &lt;ul&gt;&lt;li&gt;A promo code associated with the item.&lt;/li&gt;&lt;li&gt;For example, `PARTNER_SITE_15.`&lt;/li&gt;&lt;/ul&gt; |
| Position | &lt;ul&gt;&lt;li&gt;Position of the item in the list.&lt;/li&gt;&lt;li&gt;For example, `2`.&lt;/li&gt;&lt;/ul&gt; |
| Price | &lt;ul&gt;&lt;li&gt;Price of a product unit.&lt;/li&gt;&lt;/ul&gt; |
| Quantity | &lt;ul&gt;&lt;li&gt;Quantity of product units.&lt;/li&gt;&lt;/ul&gt; |
| Variant | &lt;ul&gt;&lt;li&gt;A variation of the item.&lt;/li&gt;&lt;li&gt;For example, **Red**.&lt;/li&gt;&lt;/ul&gt; |
| Custom Query Parameters | &lt;ul&gt;&lt;li&gt;Additional custom query parameters.&lt;/li&gt;&lt;/ul&gt; |

### Send Advanced Matching Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Trigger Open Session Call | Yandex Metrica requires an open session call before triggering the **Send Advanced Matching Event** action. |
| Page Url | Referral URL. If empty, the default URL is `https://tealium.com`. |
| Yandex Client ID | (Required) Yandex Metrica Client ID (`_ym_uid`). |
| MD5 Hashed | Select if value is MD5 hashed. |
| Email | User&#39;s email address. |
| Phone Number | Enter the phone number including the country code, without the `&#43;` symbol and spaces. For example, `70123456789`. |
| First Name | User&#39;s first name. |
| Last Name | User&#39;s last name. |
| Street | Street. |
| City | City. |
| Region | Region. |
| Postal Code | Accepts any integer. |
| Country | Accepts any string. |
| Custom Query Parameters | Additional custom query parameters. |

