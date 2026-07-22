---
title: Wootric Tag Setup Guide
description: This article describes how to set up the Wootric tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/wootric-tag/
---Wootric helps you get the most from NPS—measure customer loyalty, optimize products, retain customers, and build an army of brand advocates. 

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Account Token**: The unique ID which identifies your account, provided by Wootric

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/iq-tag-management/data-mappings/manage/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The destination variables for the Wootric tag are built into its data mapping tab. Available categories are:

### Standard

|**Destination Name**| **Description**|
|---| ---|
|Email (email)| The email for the currently logged in user|
|User ID (external\_id)| The custom ID for the currently logged in user|
|Created At (created\_at)| The sign-up date for the currently logged in user. Must be 10 digit UNIX timestamp in seconds|
|Product Name (product\_name)| The name of your product or service being tracked|
|Account Token (account\_token)| The unique ID for your account. Use to override the default in tag config|

## Vendor documentation

* [Wootric Docs](http://docs.wootric.com/)
* [Knowledge Base](http://help.wootric.com/help_center)
