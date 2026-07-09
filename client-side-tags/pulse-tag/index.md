---
title: Pulse by Analytics Intelligence Tag Setup Guide
description: This article describes how to set up the Pulse by Analytics Intelligence tag.
url: https://docs.tealium.com/client-side-tags/pulse-tag/
---
Pulse by Analytics Intelligence is a first-party behavioral analytics platform that runs entirely client-side. It auto-captures user interactions and ties them to pseudonymous identifiers, campaign attribution, and approximate geolocation. Data is batched to an Analytics Intelligence EU-hosted backend with no third-party data sharing.  

## Tag tips

* Enter your **Company/Profile ID** from Analytics Intelligence in the tag configuration panel. The ID is required for the tag to load.
* The tag loads the Pulse core library once per page. Pulse then auto-captures user interactions (pageviews, clicks, scrolls, form input, focus/blur, mouse movement, clipboard, campaign attribution, and session end) and batches them to the Analytics Intelligence EU-hosted backend.
* Use the **General** tab to enrich the initial pageview with data layer values: `page_name`, `page_type`, `site_section`, `user_id`, `environment`, and `language`. Each falls back to a sensible default (for example, `document.title`, `navigator.language`) when unmapped.
* Use the **Configuration** tab to override **Company/Profile ID** per fire (for example, multi-brand profiles).
* Pulse sets analytics cookies (`ai_pulse_uid`, `ai_pulse_did`, `ai_pulse_cpid`). Assign this tag to the **Analytics** consent category. The tag respects the Tealium consent state via `utag.gdpr.getConsentState()` and does not load when analytics consent is not granted.
* Analytics Intelligence stores all data in AWS `eu-west-1`. All identifiers are pseudonymous and no data transfers occur outside the EU. The vendor excludes sensitive form inputs (password, card, card verification value (CVV), social security number (SSN), pin) from capture.
* Recommended scope: Fire on **All Pages** at **DOM Ready**.
* Turn off **Enable Geolocation** for more conservative privacy programs, and **Enable Batching** to send events individually instead of in 60-second batches.

## Tag configuration

Navigate to the tag marketplace to add a new tag. For more information, see .

When adding the tag, configure the following settings:

* **Company / Profile ID**: Required. The Pulse company or profile ID from Analytics Intelligence. 
* **Environment**: Optional. Environment label sent with events. The default is `production`.
* **Language**: Optional. Language override sent with the pageview. The default is the browser language (`navigator.language`).
* **Enable Batching**: Batch events and send every 60 seconds (default). Set to `False` to send each event immediately.
* **Enable Geolocation**: Allow Pulse to fetch approximate IP-based geolocation once per session. The default is `True`. Set to `False` for more conservative privacy programs.
* **Debug Mode**: Enable Pulse debug logging in the browser console.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Configuration

| Variable | Type | Description |
|:---------|:-----|:------------|
| `company_id` | String | Company or profile ID |

### General

| Variable | Type | Description |
|:---------|:-----|:------------|
| `page_name` | String | Page name |
| `page_type` | String | Page type |
| `site_section` | String | Site section |
| `user_id` | String | User ID |
| `environment` | String | Environment |
| `language` | String | Language |
