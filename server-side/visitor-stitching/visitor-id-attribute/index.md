---
title: Visitor ID attributes
description: This article provides information on visitor ID attributes, best practices for using visitor ID attributes, and when and how to assign a value to them.
url: https://docs.tealium.com/server-side/visitor-stitching/visitor-id-attribute/
---
Before you begin, familiarize yourself with the following:

* [Using Attributes]()
* [Using Enrichments]()
* [About Visitor Stitching]()

A visitor ID attribute is configured in AudienceStream to uniquely identify visitors. When you create a visitor ID attribute, you add an enrichment to set the value to a user identifier, which is an event attribute, such as `email_address_hash` or `customer_id`. For visitor stitching to work properly, you must choose a unique user identifier, create a rule to determine when to identify a visitor, and verify that the chosen attribute is unique for each visitor. For more information about selecting a user identifier, see [Best practices for selecting user identifiers]().


<blockquote>
Visitor stitching is disabled by default. Contact your account manager to enable it.
</blockquote>


Visitor ID attributes are available in the Visitor scope.

![](https://docs.tealium.com/images/server-side/screenshot-2019-11-11-at-1.27.27-pm.png)

## System requirements for visitor ID attributes

A visitor ID attribute must meet the following system requirements:

* **Length**: Values must be between 6 and 255 characters in length.
* **Non-repeating**: Values must contain at least 3 different characters. A 10-character identifier with only 2 different characters ( `"a1a1a1a1a1"` ) is invalid.
* **Enrichment** : Attributes with a data type of Number cannot be used to enrich a visitor ID attribute.
* **Size**: The maximum size of a visitor ID attribute is 2 KB.

UTF-8 character sets are supported.


<blockquote>
The system automatically validates these requirements. You do not need these rule conditions in your visitor ID attribute configuration.
</blockquote>


## Best practices

A visitor ID attribute should follow these best practices:

* **Uniqueness** - Each visitor ID attribute value should be unique for each visitor.
    * **Strong identifiers** - Only use values that could be associated with a single visitor and are not likely to change, such as a hashed email address or customer ID.
    * **Weak identifiers** - Avoid values that cannot be guaranteed to be unique for each visitor or that have a high likelihood of changing over time, such as first and last name, username, or phone number.

* **Case Sensitive** - Values are case sensitive, so convert them to lower-case. For example, a single email address can be written with case variations such as `FirstLast@example.com` and `firstlast@example.com`, which would be treated as two different IDs in AudienceStream.
* **Verifying the Value** - If you are using an email address, you may want to verify that the address contains the `@` symbol. You may also want to check the string for other values such as, `undefined`, `unknown`, or `not set` or any text that would not be a valid value for a visitor ID attribute.


<blockquote>
See [Create a Visitor ID Attribute]() for a guide to creating the most accurate visitor ID attribute possible.
</blockquote>


## When to set a value for a visitor ID attribute

Set the value for a visitor ID attribute during a qualifying event, which is an event that occurs when a customer provides a reliable, unique means of identification, such as registering an account or completing a purchase.

A visitor ID attribute should not be a marketing activation ID (such as a gid). These third-party identifiers can be stored as visitor attribute for use in connectors, but are not recommended as visitor ID attributes.

## Enrich a visitor ID attribute

Use an enrichment to store a user identifier for a visitor in a visitor ID attribute. For example, when a user registers or signs up, your system might generate an internal ID that is added to the data layer as `customer_id`. In this case, you would use an enrichment to set a visitor ID attribute to `customer_id` when the `user_register` event occurs.


<blockquote>
After a visitor ID attribute is set, it cannot be updated.
</blockquote>
