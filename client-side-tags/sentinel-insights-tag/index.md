---
title: Sentinel Insights Tag Setup Guide
description: This article describes how to set up the Sentinel Insights tag.
url: https://docs.tealium.com/client-side-tags/sentinel-insights-tag/
---
Deploy the Sentinel Insights observer to detect tracking issues, data-layer anomalies, broken pixels, and consent-flow problems in real time across your marketing technology stack.

## Tag tips

* Sentinel Insights passively observes other tags, the data layer, and the consent flow. It must run first in load order to monitor everything else. Enable the **Prioritized** advanced setting on this tag.
* For full pre-`utag.js` coverage, copy the Sentinel loader stub from your account team into your `utag.sync.js` template via the iQ UI in addition to deploying this tag. The in-tag deployment captures everything from `utag.js` load onward.
* Obtain your **Environment ID** from your Sentinel Insights account team. For multi-environment setups, configure **Environment ID (Dev / Test)** as well and override per fire using the `env_id` mapping destination, a Lookup Table, or per-environment load rules.
* Use the **Configuration** tab to override `env_id` or `custom_page_name` per fire, for example in multi-brand profiles.
* **Consent Logic** is a JavaScript function body that the SDK calls to read the current consent state. The function receives one argument (`utils`) that exposes `utils.getCookie(name)`, which reads `document.cookie` and returns the URL-decoded value, or an empty string if the cookie does not exist. Your snippet must return a string that Sentinel uses as the consent signal. Avoid embedding credentials in this field, because the tag configuration ships in the customer&#39;s `utag.js`.

  ```javascript
  var val = utils.getCookie(&#39;consent_status&#39;);
  return val === &#39;granted&#39; || val === &#39;accepted&#39; ? &#39;granted&#39; : &#39;denied&#39;;
  ```
* Use the **Cookie Consent** tab to map a data layer variable to `grant` or `revoke`. The tag then signals a consent update to Sentinel, which re-reads the **Consent Logic** function for the new state.
* **Trigger toggles** control which Sentinel events fire: Data Layer Updates (default on), SPA Page Changes, and Resume Load. Pair the SPA toggles with customer-side extensions that fire `spa_page_change` or `spa_resume` Tealium events.
* This tag is exempt from the standard Tealium GDPR consent gate. Sentinel Insights observes consent state rather than relying on it. The **Consent Logic** function is the consent integration point.
* CSP requirements: allow `script-src https://config.datas3ntinel.com` and `connect-src https://collect.datas3ntinel.com`.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see .

When adding the tag, configure the following settings:

* **Environment ID (Production)**: Required Sentinel Insights environment identifier for production traffic. Must be a UUID (format: 8-4-4-4-12 hex).
* **Environment ID (Dev / Test)**: Optional non-production environment identifier. Override using load rules, a Lookup Table, or a per-fire `env_id` mapping.
* **Consent Logic (Function Body)**: JavaScript function body the SDK calls to determine consent state. See tag tips for usage details.
* **Delay Start**: When `True`, the SDK initializes but defers monitoring until an explicit resume event. Use for SPA flows that require controlled activation.
* **Auto Page View Tracking**: When `True`, the tag sends a page-view event automatically on initial load.
* **Custom Page Name (SPA)**: Optional fallback name used by SPA Page Change events when the URL does not change.
* **Trigger: Data Layer Updates**: When `True`, forwards data-layer payloads on every view, link, and custom event. Default on.
* **Trigger: SPA Page Changes**: When `True`, fires a Sentinel pageView event when the tag receives a Tealium event named `spa_page_change`.
* **Trigger: Resume Load (SPA)**: When `True`, fires a Sentinel resume event when the tag receives a Tealium event named `spa_resume`. Use with **Delay Start** set to `True`.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Configuration

| Variable | Type | Description |
|:---------|:-----|:------------|
| `env_id` | String | Environment ID |
| `custom_page_name` | String | Custom page name |
