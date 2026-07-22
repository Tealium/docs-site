---
title: The Trade Desk Universal Pixel Tag Setup Guide
description: This article describes how to set up The Trade Desk Universal Pixel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/the-trade-desk-universal-pixel-tag/
---
## Tag Configuration

First, go to the tag marketplace and add The Trade Desk Universal Pixel Tag to your profile (See [Add a tag](https://docs.tealium.com/manage-tags/#add-a-tag)).

After adding the tag, configure the following settings:

1. **Advertiser ID**: Enter your Advertiser ID supplied by Trade Desk. This is present in your Universal Pixel Tag.
1. **Pixel ID**: Enter your Pixel ID supplied by Trade Desk. This is present in your Universal Pixel Tag.


<blockquote>
Use data mappings if you prefer to configure the tag settings dynamically.
</blockquote>


## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

Recommended Load Rule: **Load on all pages**.

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The destination variables for the The Trade Desk Universal Pixel Tag are built into its Data Mapping tab.

The available categories are:

### Standard

|**Destination Name**| **Description**|
|---| ---|
|Advertiser ID| Unique advertiser identifier supplied by Trade Desk|
|Pixel ID| Unique pixel identifier supplied by Trade Desk|
| `td1`| Customer parameter #1   |
| `td2`| Customer parameter #2   |
| `td3`| Customer parameter #3   |
| `td4`| Customer parameter #4   |
| `td5`| Customer parameter #5   |
| `td6`| Customer parameter #6   |
| `td7`| Customer parameter #7   |
| `td8`| Customer parameter #8   |
| `td9`| Customer parameter #9   |
| `td10`| Customer parameter #10   |

### Consent (GDPR)

The consent parameters follow the IAB specification for URL-based services.

Reference: [IAB GDPR Consent Passing for URL-Based Services](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/URL-based%20Consent%20Passing_%20Framework%20Guidance.md)


<blockquote>
The creator of the URL should ensure these parameters are added only once and are passed to services that are expecting them and can properly handle them.
</blockquote>


|Destination Name| **Value**| **Description**|
|---| ---| ---|
|`gdpr`| `0` / `1`| Determines if GDPR should apply to the user. Value of `1` means `yes`, default value of `0` means `no`. |
|`gdpr_consent`| URL-safe base64-encoded GDPR consent string| This parameter should only be passed if `gdpr` has a value of `1` and `gdpr_consent` is not an empty string.|
|`gdpr_pd`| `0` / `1`| This parameter is optional and determines if personal data is included. Value of `1` means `yes`, default value of `0` means `no`. |


<blockquote>
Other personal data, such as IP addresses or tracking pixel cookies, may be passed as part of the request. The `gdpr` and `gdpr_consent` parameters should be used by the callee to determine whether an identifier cookie or other personal data can be set and/or used.
</blockquote>

