---
title: CookieConsent v3 Logging
description: Use the CookieConsent v3 Logging extension to capture user consent decisions and send them to a configurable endpoint.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/cookieconsent-v3-logging-extension/
---
Use this extension to log user consent decisions collected through the CookieConsent v3 interface. It captures relevant information such as the consent ID, accepted categories, and the consent model, then sends this data as a JSON payload to your endpoint using the `fetch()` API. You can configure the payload to match your system’s requirements, whether you are sending to the Tealium Collect endpoint or a custom destination.

## Requirements

The CookieConsent v3 Logging extension requires the Manage JavaScript Code Extensions permission.

## How it works

This extension listens for `consent_updated` events from the CookieConsent interface. When a user makes or updates a consent decision, the extension retrieves the consent state and sends the information as a JSON payload to a specified endpoint using the `fetch()` method.

The payload typically includes:

* `tealium_event`: The event type, such as `consent_decision`.
* `consent_id`: Unique identifier for the user&#39;s consent decision.
* `decision_type`: Whether the user accepted or rejected categories.
* `accepted_purposes` and `rejected_purposes`: The categories selected by the user.
* `consent_model`: Either `opt-in` or `opt-out`.
* `url`: The current page URL without query parameters.
* `decision_timestamp`: The time the consent was last updated.
* `expiration_time`: How long the consent is valid.
* `revision`: The current version of the consent configuration.
* `tealium_account` and `tealium_profile`: Where the event should be sent.
* `tealium_visitor_id`: (Optional) Included if already available in the `utag_main` cookie.

You can adjust this payload to suit your endpoint or data model.

## How to configure

1. In Tealium iQ, go to **Extensions** and click **Add Extension**.
1. Click the **Privacy** tab.
1. Click **&#43; Add** next to the **CookieConsent v3 Logging** extension.
1. Enter a **Title** for the extension.
1. Under **Scope**, use the default option **DOM Ready**. It supports load conditions, which lets you control when the extension runs. The **Preloader** scope is also supported but doesn&#39;t allow load conditions.
1. (Optional) Click **Add Condition** to apply load conditions for this extension. Ensure the conditions match your consent integration’s enforcement rules to avoid issues.
1. In the **Configuration** code do one of the following:
    * If you&#39;re sending logs to Tealium Collect, replace the placeholder values for `tealium_account` and `tealium_profile` with your actual values.
    * If you&#39;re sending logs to a different endpoint, update the `fetch()` URL to the destination you want to send the consent logs.

