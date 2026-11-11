---
title: Wootric Tag Setup Guide
description: This article describes how to set up the Wootric tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/wootric-tag/
---Wootric helps you get the most from NPS—measure customer loyalty, optimize products, retain customers, and build an army of brand advocates. 

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Account Token**: The unique ID which identifies your account, provided by Wootric

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see the [Load Rules](https://docs.tealium.com/about-load-rules/) documentation.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

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
