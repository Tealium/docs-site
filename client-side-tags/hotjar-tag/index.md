---
title: Hotjar Tag Setup Guide
description: This article describes how to configure the Hotjar Tag.
url: https://docs.tealium.com/client-side-tags/hotjar-tag/
---
## Tag tips

Use mapping to dynamically override the standard config values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Hotjar ID**
  * Your Hotjar Site ID.

* **Hotjar Snippet Version**
  * The version of your tracking code from Hotjar.

### Add Tag from Code (Optional)

Use the following steps to add the Hotjar tag from code"

1. Log in to your Hotjar account.
1. From the account dashboard, click **Install code manually**.
1. Click **Copy to clipboard**.
1. Log in to Tag Management, go to **Tag Management &gt; Tags**.
1. Click **Add Tag**.
1. Click **Detect Tag from Code**.
1. Paste the code you copied in Step 3.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`hjid`|  <ul><li>Hotjar ID</li></ul> |
| `hjsv` |  <ul><li>Hotjar Snippet Version</li></ul> |
