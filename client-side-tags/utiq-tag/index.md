---
title: Utiq Tag Setup Guide
description: This article describes how to set up the Utiq tag.
url: https://docs.tealium.com/client-side-tags/utiq-tag/
---
## Tag tips

* Use mappings to override or dynamically set tag configurations.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **HOST**: The client&#39;s domain.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:-----|:------------|
| `host`  | String | The domain name where the Utiq tag is deployed. |
| `customUtiqHost`  | String | Custom host. |
| `consentManagerOrigin`  | String | Consent manager origin. |
| `consentManagerDataLayer`  | String | Consent manager data layer. |

### Listeners

| Variable | Type | Description |
|:---------|:-----|:------------|
| `listener_ids_available` | Boolean | Set this to `true` if you want to trigger the `utiq_ids_available` event when the `Martechpass` and `Adtechpass` become available. The event feeds the following data layer variables: `utiq_mtid`, `utiq_category`. |
| `listener_consent_update_finished` | Boolean | Set this to `true` if you want to trigger the `utiq_consent_update_finished` event when the consent update has finished. The event feeds the following data layer variable: `utiq_consent_granted`. |
| `listener_consent_changing` | Boolean | Set this to `true` if you want to trigger the `utiq_consent_changing` event when Utiq gets a signal from the browser (or client) to change the consent status to the one held with the parameter. The event feeds the following data layer variable: `utiq_consent_granted`. |
| `listener_initialised` | Boolean | Set this to `true` if you want to trigger the `utiq_initialised` event when Utiq is fully initialized on every page load or navigation. |
| `listener_eligibility_checked` | Boolean | Set this to `true` if you want to trigger the `utiq_eligibility_checked` event when the user eligibility check information is performed for the current client. The event feeds the following data layer variable: `utiq_is_eligible`. |

### Events

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `handleConsentChange` | Change consent. |
| `showConsentManager` | Display consent manager. |
| `setVerboseLoggingLevel` | Enable verbose logging. |
| `resetLoggingLevel` | Disable verbose logging. |
| Custom | Custom event. |

### Event-specific Parameters

To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `handleConsentChange` | Change consent. |
| `showConsentManager` | Display consent manager. |
| `setVerboseLoggingLevel` | Enable verbose logging. |
| `resetLoggingLevel` | Disable verbose logging. |
| Custom | Custom event. |