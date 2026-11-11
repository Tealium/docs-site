---
title: LinkedIn Insight Tag Setup Guide
description: This article describes how to set up the LinkedIn Insight tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/linkedin-insight-tag/
---
## Tag tips

* Override standard configurations through mapping.
* For multiple Partner IDs, enter a comma-separated list in the **Partner ID** field.
* Uses the following E-Commerce variables:
    * Order ID (`_corder`)
    * Order Total (`_ctotal`)
    * Order Currency (`_ccurrency`)
    * Customer ID (`_ccustid`)

## Tag configuration
 
Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Partner ID**: The partner ID for the LinkedIn account.
* **Generate Event ID**: Automatically generate an event ID for every LinkedIn tracking event. The default value is `true`.

### Conversions API for Web

To support the LinkedIn Conversions API for Web, the tag generates a unique event ID for each event tracked and sends it to Event Streaming for use in the LinkedIn Conversions connector. The event ID may be mapped in the connector to synchronize the web-based on server-based integrations. This feature requires an active [Tealium Collect tag](https://docs.tealium.com/tealium-collect-tag/).

The tag emits new event attributes using the following naming convention:

```nohl
linkedin_event_id_{CONVERSION_EVENT}_{TAG_UID}
```

For example: `window.lintrk('track', { conversion_id: 11563522 });`

See the [LinkedIn Conversions Connector Setup Guide](https://docs.tealium.com/linkedin-conversions-connector/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description|
|---| ---|
| `partner_id`| Partner ID|
| `event_id` | Event ID |
| `linkedin.custom_channel_id` | Custom Channel |
| `linkedin.custom_group_id` | Custom Group ID |
| `linkedin.custom_user_id` | Custom User ID |
| `linkedin.zoom_info_id` | Zoom Info ID |
| `linkedin.title` | Title |
| `linkedin.domain` | Domain |
| `linkedin.company` | Company |
| `linkedin.gender` | Gender |
| `linkedin.location` | Location |
| `linkedin.education` | Education |
| `linkedin.email_sha256` | Email SHA256 |
| `linkedin.email_sha512` | Email SHA512 |
| `linkedin.raw_data` | Raw Data |
| `linkedin.raw_data_overwrite` | Raw Data Overwrite |
| `linkedin.encrypted_data` | Encrypted Data |
| `linkedin.partner_data` | Partner Data |
| `linkedin.sic_codes` | Sic Code |
| `linkedin.employee_range` | Employee Range |
| `linkedin.default_keywords` | Default Keywords |
| `linkedin.async_target` | Async Target |
| `linkedin.use_iframe` | Use Iframe |
| `linkedin.use_callback` | Use Callback |
| `linkedin.test_url` | Test URL |
| `conversionId` | Conversion ID |