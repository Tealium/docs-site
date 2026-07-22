---
title: Install
description: Learn to install Tealium Collect for Google Tag Manager.
url: https://docs.tealium.com/platforms/google-tag-manager/install/
---
## Requirements

* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)

## How it Works

The Tealium Collect Tag for Google Tag Manager is a custom template that loads the Tealium Collect JavaScript file from Tealium once per page.  

For each tag triggered event, the tag automatically flattens the `dataLayer` object into key-value pairs and posts the data to Tealium's data collection endpoint.  A custom endpoint may be used if you use first-party data collection.

The following Google Tag Manager event is prior to being flattened:  
```
dataLayer.push({
  'ecommerce': {
    'purchase': {
      'actionField': {
        'id': 'T12345',
...
```

After being flattened, it becomes the following Tealium event:  
```
"tealium_event": "purchase"
"ecommerce.purchase.actionField.id": "T12345"
...
```

## Install

To add the Tealium Collect Tag with the Google Tag Manager:

1. In Google Tag Manager, click **Templates** in the left navigation.
2. On the **Tag Templates** screen, click **Search Gallery**.
3. Search for and select "Tealium Collect Tag".
4. Add the template by clicking **Add to workspace**.
5. On the "Are you sure you want to add a community template?" screen, click **Add**

### Add New Tag

To add an instance of the Tealium Collect Tag:

1. In Google Tag Manager, click **Tags** in the left navigation.
2. Click the **New** button.
3. Click "Tag Configuration" to choose a tag type. Search and select "Tealium Collect Tag" from the list.
4. Provide a name for the tag to replace the text "Untitled Tag".

After adding the Tag, configure the following settings. Leave optional fields blank if the value is unknown.

* **Tealium Account**: (Required) The Tealium account name. For example, `companyXYZ`.  
* **Tealium Profile**: (Required) The Tealium profile name. For example, `main`.  
* **Tealium Data Source Key**: (Optional) The data source key from your server-side Tealium configuration. For example, `abc123`.  
* **Data Collection Endpoint**: (Optional) Override the Tealium Collect endpoint with your first-party data collection endpoint. For example, `https://collect.example.co.uk/example-event-endpoint`.  
* **Data Object**: (Optional) The custom JavaScript variable to use instead of the global `dataLayer` object. For example, `{{myObject}}`.

### Triggers

For page view tracking, use the built-in "All Pages" trigger. To include event tracking, use an "All Events" trigger to fire for all events.

To set up the "All Events" trigger in Google Tag Manager:

1. In Google Tag Manager, click the **Triggers** in the left navigation.
2. Click the **New** button to add a trigger.
3. Click "Trigger Configuration" to choose a tag type. Search and select "Custom Event" from the list.
3. Select the "Use regex matching" checkbox.
4. Enter the following for the "Event Name" regular expression (regex):    
      ```
      ^(?!gtm.load)(?!gtm.dom)(?!gtm.init)(?!gtm.init_consent).*
      ```
5. Click **Save**, rename the custom trigger a new name, and click **Save** again.

This rule triggers for all events excepting `gtm.load `and `gtm.dom` (two events specific to Google Tag Manager that we want to ignore).

### Data Layer Enrichment

The Tealium Data Layer Enrichment tag brings server-side attributes from Tealium AudienceStream and injects them into the data layer.

To install the Data Layer Enrichment tag:

1. In Google Tag Manager, click **Templates** in the left navigation.
2. On the **Tag Templates** screen, click **Search Gallery**.
3. Search for and select "Tealium Data Enrichment Tag".
4. Add the template by clicking **Add to workspace**.
5. On the "Are you sure you want to add a community template?" screen, click **Add**

## Validation

If the Tealium Collect tag is firing for all events, then every `dataLayer.push` call on your page sends a data collection event to Tealium.  

In your debug console **Network** tab, a POST call goes out to `https://collect.tealiumiq.com/ACCOUNT/PROFILE/2/i.gif`.  

Use [Live Events](https://docs.tealium.com/about-live-events/) to see your event data in real-time.
