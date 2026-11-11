---
title: Uplift Tag Setup Guide
description: This article describes how to set up the UpLift tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/uplift-tag/
---## Tag tips

* Use mapping to dynamically override the standard configuration values.
* The Domain configuration has been deprecated.

### Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **UP Code**
  * The UP Code (Account ID) provided by your Uplift contact.
* **Domain**
  * The domain of the host site. (Deprecated)

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`acct`|  <ul><li>UP Code</li></ul> |
|`domain`|  <ul><li>Domain</li><li>Deprecated</li></ul> |
