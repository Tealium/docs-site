---
title: Mailchimp Connector Setup Guide for AudienceStream
description: This article describes how to set up the Mailchimp connector.
url: https://docs.tealium.com/server-side-connectors/mailchimp-connector/
---
## Requirements

* Mailchimp Account
* Mailchimp API Key ([how to find your API key](http://kb.mailchimp.com/integrations/api-integrations/about-api-keys))

## Supported Actions

| Action Name                   | Description                                                | Trigger on Audiences | Trigger on Streams |
|:------------------------------|:-----------------------------------------------------------|:---------------------|:-------------------|
| Subscribe Visitor to List     | Add subscribed members to a list                           | ✓                    | ✗                  |
| Unsubscribe Visitor from List | Remove unsubscribed members from a list                    | ✓                    | ✗                  |
| Upsert Ecommerce Order        | Upsert Ecommerce transaction details for successful orders | ✓                    | ✗                  |
| Upsert Ecommerce Cart         | Upsert Ecommerce details for abandoned carts               | ✓                    | ✗                  |

## Configure Settings

Go to the Connector Marketplace and add a new Mailchimp connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

To configure your vendor,

1. In the **Configure** tab, enter a suitable title.
1. Enter your Mailchimp API key. This is required. ([how to find your API key](http://kb.mailchimp.com/integrations/api-integrations/about-api-keys))
1. (Optional) Provide additional notes about this Mailchimp implementation.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. It's where you'll set up actions and trigger them. This section describes how to set up parameters and options for each action.

### Action - Subscribe Visitor to List

#### Parameters

1. **Target Subscriber List**: (Required) Select the target Mailchimp list to add the subscriber to.
1. **General Properties to Set**: (Required) Lets you send additional data about the subscribed member to specific fields in the target Mailchimp list.
1. **Update Existing Subscriber**: (Recommended) Check this box if you want existing subscriber information to be automatically updated.
1. **Target Interest Group**: Select the interest group(s) to add the subscriber to.
1. **Set Field and Merge Tags**: Add or update tags for the subscriber.
1. **New Notes**: Provide additional notes for the subscriber.

For the following Options, choose an Attribute from the **Map** dropdown and an option from the **To** dropdown.

#### Options - General Properties to Set

| Option                                                                   | Description                                                                                                                                                                                                                               |
|:-------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Email Address - Plain (Required for new subscribers)                     | Plain email address of the subscriber, will be hashed with MD5 automatically according to [Mailchimp email hash requirements](https://developer.mailchimp.com/documentation/mailchimp/guides/manage-subscribers-with-the-mailchimp-api/). |
| Email Address - Hashed<br> (Optional if plain email address is provided) | Hashed email address of the subscriber using MD5, according to [Mailchimp email hash requirements](https://developer.mailchimp.com/documentation/mailchimp/guides/manage-subscribers-with-the-mailchimp-api/).                            |
| New Member Status                                                        | Subscription status of new members. <br> Possible values are: `subscribed`, `unsubscribed`, `cleaned`, and `pending`. If no member status is provided, the status defaults to `subscribed`                                                |
| Email Type                                                               | Indicates the type of email message/content. Possible options are: `html` and `text`                                                                                                                                                      |
| Opt-in IP                                                                | The IP address used by the subscriber to confirm their opt-in status.                                                                                                                                                                     |
| Signup IP                                                                | The IP address of the computer/device used by the subscriber during signup.                                                                                                                                                               |
| Language                                                                 | The language set in the subscriber's browser at the time of signup.                                                                                                                                                                       |
| Location - Latitude/Longitude                                            | [Geolocation](http://kb.mailchimp.com/lists/managing-subscribers/about-geolocation) of the subscriber at the time of signup                                                                                                               |
| Current Status                                                           | Current subscription status of the subscriber. <br> Possible values are: `subscribed`, `unsubscribed`, `cleaned`, and `pending`.                                                                                                          |
| Opt-in Timestamp                                                         | The date and time when the subscriber confirmed their opt-in status                                                                                                                                                                       |
| Signup Timestamp                                                         | The date and time when the subscriber signed up for your list.                                                                                                                                                                            |
| VIP Status (true                                                         | false)| Indicates whether or not the subscriber is marked as a [VIP](http://kb.mailchimp.com/lists/managing-subscribers/designate-and-send-to-vip-subscribers)                                                                            |

#### Options - Set Field and Merge Tags

| Option                           | Description    |
|:---------------------------------|:---------------|
| FNAME - First Name - (type:text) | first name tag |
| LNAME - Last Name - (type:text)  | last name tag  |

### Action - Unsubscribe Visitor from List

#### Parameters

1. **Target Subscriber List**: (Required) Select the target Mailchimp list to add the unsubscribed member to.
1. **General Properties to Set**: (Required) Lets you send the unsubscriber's data to specific fields in the target Mailchimp list (see available options below).

For the following Options, choose an attribute from the **Map** dropdown and an option from the **To** dropdown.

#### Options - General Properties to Set

| Option                           | Description                                                                                      |
|:---------------------------------|:-------------------------------------------------------------------------------------------------|
| Email Address - Plain (Required) | Unhased email address of the subscriber                                                          |
| Email Address - Hashed           | Hashed email address of the subscriber (Optional if the plain email address is already provided) |

### Action - Upsert Ecommerce Order

#### Parameters

1. **Order Data**: (Required) For sending transactional information about the order.
1. **Customer Data**: (Required) For sending information about a specific customer. If the customer exists in your store, their information is updated. Otherwise, a new customer will be created.
1. **Order Line Item(s) Data** (Required for new orders only): For sending information about one or more order line items (make sure the product already exists).

For the following Options, choose an Attribute from the **Map** dropdown and an option from the **To** dropdown.

#### Options - Order Data

| Option                                  | Description                                                                                                                     |
|:----------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------|
| Store Foreign ID              | (Required) Store identifier                                                                                                                |
| Order Foreign ID          |(Required) Unique order identifier                                                                                                         |
| Campaign ID                             | Unique identifier of the campaign associated with the order                                                                     |
| Financial Status                        | The order status (for example, `refunded`, `processing`, `cancelled` etc.)                                                      |
| Fulfillment Status                      | Indicates whether or not the order was fulfilled (for example, `partial`, `fulfilled`, etc.)                                    |
| Currency Code (Required for new orders) | The [three-letter ISO 4217 code](https://en.wikipedia.org/wiki/ISO_4217#Active_codes) for the currency that your store accepts. |
| Order Total (Required for new orders)   | The total transaction (including shipping and tax)                                                                              |
| Tax Total                               | The tax amount in the total transaction                                                                                         |
| Shipping Total                          | The shipping amount in the total transaction                                                                                    |
| Tracking Code                           | The Mailchimp tracking code for the order, for instance, the value of the `mc_tc` parameter in your E-Commerce tracking URLs.   |
| Foreign Processed Time                  | The date and time the order was processed.                                                                                      |
| Foreign Cancel Time                     | The date and time the order was cancelled.                                                                                      |
| Foreign Update Time                     | The date and time the order was updated.                                                                                        |
| Shipping Address - Name                 | The shipping address for the order                                                                                              |
| Shipping Address - Address Field 1      | Additional field for the shipping address                                                                                       |
| Shipping Address - Address Field 2      | Additional field for the shipping address                                                                                       |
| Shipping Address - City                 | The city in the shipping address                                                                                                |
| Shipping Address - Province             | The state or normalized province in the shipping address                                                                        |
| Shipping Address - Province Code        | The two-letter code for the province or state in the shipping address                                                           |
| Shipping Address - Postal Code          | The postal or zip code in the shipping address                                                                                  |
| Shipping Address - Country              | The country in the shipping address                                                                                             |
| Shipping Address - Country Code         | The two-letter code for the country in the shipping address                                                                     |
| Shipping Address - Longitude            | The longitude for the shipping address location                                                                                 |
| Shipping Address - Latitude             | The latitude for the shipping address location                                                                                  |
| Shipping Address - Phone Number         | The phone number for the shipping address                                                                                       |
| Shipping Address - Company              | The company associated with the shipping address                                                                                |
| Billing Address - Name                  | The name associated with the billing address                                                                                    |
| Billing Address - Address Field 1       | The billing address for the order                                                                                               |
| Billing Address - Address Field 2       | Additional field for the billing address                                                                                        |
| Billing Address - City                  | The city in the billing address                                                                                                 |
| Billing Address - Province              | The state or normalized province in the billing address                                                                         |
| Billing Address - Province Code         | The two-letter code for the province in the billing address                                                                     |
| Billing Address - Postal Code           | The postal or zip code in the billing address                                                                                   |
| Billing Address - Country               | The country in the billing address                                                                                              |
| Billing Address - Country Code          | The two-letter code for the country in the billing address                                                                      |
| Billing Address - Longitude             | The longitude for the billing address location                                                                                  |
| Billing Address - Latitude              | The latitude for the billing address location                                                                                   |
| Billing Address - Phone Number          | The phone number for the billing address                                                                                        |
| Billing Address - Company               | The company associated with the billing address                                                                                 |

#### Options - Customer Data

| Option                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|:-------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Customer Foreign ID             | (Required) Customer identifier                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Email Address (Required for new customers) | The customer's email address                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Opt-in Status                              | The customer’s opt-in status. This flag applies only to list members that were added through Mailchimp's E-commerce API endpoints; however it will not overwrite the opt-in status of existing list members. Customers who didn't opt into your Mailchimp list will be added as [Transactional members](http://developer.mailchimp.com/documentation/mailchimp/guides/getting-started-with-ecommerce/#about-subscribers-and-customers). Possible values are `true` and `false` |
| Company                                    | The customer's company                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| First Name                                 | The customer's first name                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Last Name                                  | The customer's last name                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Orders Count                               | The customer's total order count                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Total Spent                                | The total amount the customer has spent                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Address Field 1                            | The mailing address of the customer                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Address Field 2                            | Additional field for the customer's mailing address.                                                                                                                                                                                                                                                                                                                                                                                                                       |
| City                                       | The city the customer is located in                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Province                                   | The customer's state name or normalized province                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Province Code                              | The two-letter code for the customer's province or state                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Postal Code                                | The customer's postal or zip code                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Country                                    | The customer's country                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Country Code                               | The two-letter code for the customer's country                                                                                                                                                                                                                                                                                                                                                                                                                             |

#### Options - Order Line Item(s)

| Option                                             | Description                                                                      |
|:---------------------------------------------------|:---------------------------------------------------------------------------------|
| Line Item(s) Foreign ID              | (Required) The unique identifier of the order line item                                     |
| Line Item(s) Product Foreign ID       | (Required) The unique identifier of the product associated with the order line item         |
| Line Item(s) Product Variant Foreign ID  | (Required) The unique identifier of the product variant associated with the order line item |
| Line Item(s) Quantity                  | (Required) The quantity of an order line item                                               |
| Line Item(s) Price                 | (Required) The price of an order line item                                                  |

### Action - Upsert Ecommerce Cart

#### Parameters

1. **Cart Data**: (Required) For sending general information about the cart.
1. **Customer Data**: (Required) For sending information about a specific customer. If the customer exists in your store, their information is updated. Otherwise, a new customer will be created.
1. **Cart Line Item(s) Data**: (Required) For sending one or more cart line items (make sure the product already exists).

For the following Options, choose an Attribute from the **Map** dropdown and an option from the **To** dropdown.

#### Options - Cart Data

| Option                                  | Description                                                                                                                     |
|:----------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------|
| Store Foreign ID          | (Required) Store identifier                                                                                                                |
| Cart Foreign ID               |(Required) Unique order identifier                                                                                                         |
| Campaign ID                             | Unique identifier of the campaign associated with the cart                                                                      |
| Checkout URL                            | The URL of the cart                                                                                                             |
| Currency Code (Required for new orders) | The [three-letter ISO 4217 code](https://en.wikipedia.org/wiki/ISO_4217#Active_codes) for the currency that your store accepts. |
| Order Total (Required for new orders)   | The total transaction (including shipping and tax)                                                                              |
| Tax Total                               | The tax amount in the total transaction                                                                                         |

## Example

So far, we learned how to set up a new Mailchimp Connector. Next, we'll look at an example scenario on how to add a specific visitor segment, let's say shoe lovers, to a subscription list. Refer to the [Usage Example article](https://support.tealiumiq.com/en/support/solutions/articles/36000363504-mailchimp-connector-usage-example) for more.

## Vendor Documentation

* [Lists](http://kb.mailchimp.com/lists)
* [Managing Subscribers and Unsubscribers](http://kb.mailchimp.com/managing-subscribers)
* [Groups](http://kb.mailchimp.com/lists/groups/getting-started-with-groups)
* [Merge Tags](http://kb.mailchimp.com/merge-tags/getting-started-with-merge-tags)
* [Mailchimp for Ecommerce](http://kb.mailchimp.com/integrations/e-commerce/how-to-use-mailchimp-for-e-commerce)
* [Mailchimp API Reference](http://developer.mailchimp.com/documentation/mailchimp/reference/overview/)

## Connector Changelog

### Released December 08, 2016

We have made changes to the following actions to support Mailchimp's most recent API v3.0.


<blockquote>
According to Mailchimp, [prior versions will NOT be supported after 2016](https://apidocs.mailchimp.com/api/changelog.php). Hence, we strongly recommend you doublecheck all existing Mailchimp Actions in your AudienceStream profile and reconfigure them as necessary.
</blockquote>


#### Subscribe Visitor to List - Updated

| Parameter                 | Functionality Change                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | What to do                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|:--------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| General Properties to Set | <ul><li>Renamed option `email.email` to Email Address - Plain</li><li>Added new option Email Address - Hashed</li><li>Added new option New Member Status</li><li>Renamed `email_type` to Email Type - (`html` or `text`)</li><li>Renamed `merge_vars.optin_ip` to Opt-in IP</li><li>Added new option Signup IP</li><li>Renamed option `merge_vars.mc_language` to Language</li><li>Renamed option `merge_vars.mc_location.latitude`) to Location - Latitude</li><li>Renamed option `merge_vars.mc_location.longitude` to Location - Longitude)</li><li>Added new option Current Status - (`subscribed` or `unsubscribed`, `cleaned`, `pending`)</li><li>Renamed option `merge_vars.optin_time` to Opt-in Timestamp</li><li>Added new option Signup Timestamp</li><li>Added new option VIP Status (`true` or `false`)</li><li>Deprecated options  <ul><li>`send_welcome`</li><li>`merge_vars.new-email`</li><li>`merge_vars.mc_location.anything`</li><li>`email.leid`</li><li>`email.euid`</li><li>`double_optin`</li><li>`replace_interests`</li></ul> </li></ul> | Reconfigure the deprecated General Properties mappings using the new options. |
| Target Interest Group     | No functionality changes but reconfiguration might be needed                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | If the dropdown doesn't show your previously selected option, please select the appropriate option again.                                                                                                                                                                                                                                                                                                                                                                                                            |
| Set Field and Merge Tags  | No functionality changes but reconfiguration might be needed                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | If the dropdown doesn't show your previously selected option, please select the appropriate option again.                                                                                                                                                                                                                                                                                                                                                                                                            |

#### Unsubscribe Visitor from List - Updated

| Parameter                 | Functionality Change                                                                                                                                                                                                                                                   | What to do                                                                                                  |
|:--------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------|
| General Properties to Set | <ul><li>Renamed option `email.email` to Email Address - Plain</li><li>Added new option Email Address - Hashed</li><li>Deprecated options  <ul><li>email.euid</li><li>email.leid</li><li>delete\_member</li><li>send\_goodbye</li><li>send\_notify</li></ul> </li></ul> | Reconfigure the deprecated General Properties mappings using the new options. |

#### Add E-Commerce 360 - Deprecated

This is now replaced by the new [Upsert Ecommerce Order Action](https://docs.tealium.com/mailchimp-connector/). You must migrate all deprecated parameters and options to a new action instance.
