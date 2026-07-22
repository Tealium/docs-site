---
title: Google SA360 Enhanced Conversions Implementation Guide
description: This article provides information about implementing Google SA360 Enhanced Conversions.
url: https://docs.tealium.com/partners-and-industries/tech-partners/google-sa360-enhanced-conversions-implementation-guide/
---
The Tealium EventStream Google SA360 Enhanced Conversions (EC) connector leverages the Google Campaign Manager 360 API (CM360 API) to enhance client-side conversions that contain PII. Enhanced Conversions in CM360 API is a hybrid solution, using both tags and API. Floodlight tags are still used client-side to capture conversion events.

## Requirements - Google

### Accept the Terms of Service in CM360

To accept the terms of service in CM360, perform the following steps:

1. Log in to the CM360 account and select the advertiser you want to implement Enhanced Conversions with. 
1. On the left side, go to **Floodlight > Configuration**, check the checkbox under **Enhanced conversion section**.

### Identify parameters for Floodlight tag

Open **Floodlight > Activities** and find or create the activity you are using to receive the Enhanced Conversions data. The important parameters are: 

* Advertiser ID (**floodlight Configuration ID** or `floodlightConfigurationId`) 
* Activity ID 
* Activity tag string 
* Group tag string 
* Type (`counter` or `sales`)

### Add Tealium service account as a user in CM360

Add the `api@tealium.com `user to your CM360 account and grant it access with **Insert** and **Update offline conversions** permissions. After that user is added to your CM360 account, note the generated profile ID for use in the EventStream connector configuration.

## Requirements - Tealium iQ Tag

For basic setup of the TiQ Floodlight tag, see [Floodlight tag](https://docs.tealium.com/floodlight-gtagjs-tag/).

Use the configuration values noted above (Advertiser ID, Activity tag string, Group tag string, and Type), along with event mappings to trigger conversions, in the basic tag configuration.

The Enhanced Conversions feature requires two additional values to be passed to Google. The following values must match on both the client-side and the API calls for a given conversion event:

* Match ID (`match_id`): A unique identifier for the particular conversion to be used in matching client-side and API events. 
* Ordinal (`ord`): A cache-busting value to force the browser or app to load the most recent version of a file to ensure unique conversion counts for a given visitor.

Use the Tealium iQ library-generated `tealium_random` attribute. Map this to both attributes in the Tealium iQ Floodilght tag.

## Requirements - Tealium EventStream Connector

The [SA360 Enhanced Conversions connector](https://docs.tealium.com/google-sa360-enhanced-conversions-connector/) has the following implementation steps:

### Connector Configuration

After adding the connector, configure the following settings:

**Floodlight Profile ID**: This is the profile ID generated in CM360 when the `api@tealium.com` user was added to the account.

#### Action Source

**Event Feed**: Create an [event feed](https://docs.tealium.com/about-event-feeds/) for the relevant Floodlight conversion and use this feed as the source of the connector action.

#### Action Configuration

###### Conversion Data

The following fields are required:

* **Floodlight Configuration ID**: The advertiser ID value from CM360, without the `DC-` prefix.
* **Floodlight Activity ID**: The ID for the activity, found in the CM360 conversion information next to the activity name.
* **Match ID**: Map the same attribute used for `match_id` in the Tealium iQ tag.
* **Ordinal**: Map the same attribute used for `ord` in the Tealium iQ tag.
* **Quantity**: The quantity for the conversion. In most cases this should match the Tealium iQ tag quantity unless you are updating the conversion quantity.
* **Value**: The value for the conversion. In most cases this should match the Tealium iQ tag value unless you are updating the conversion value.

The following fields are required for conversions updated through API calls:

* **Timestamp**: Tealium generates a timestamp based on the incoming event time, in microseconds. Conversions updated through API must pass a timestamp value which matches the client-side event within 2 minutes.

##### User Data

Map PII data for the conversion event. The minimum requirements are as follows:

* Hashed Email
* Hashed Phone Number
* Address Info

Select either **apply SHA256 hash** or **already SHA256 hash** mapping, depending on the event attribute's hash state. If event data is already hashed, it must have been lowercased, trimmed, and have had periods preceding the domain name in `gmail.com` and `googlemail.com` email addresses removed prior to hashing.


<blockquote>
The CM360 API requires a 120 minute delay before it can accept conversion updates. The Tealium SA360 connector has this delay built in, but when using Trace our connectors bypass batching delays. You will encounter `CONVERSION_NOT_FOUND` errors in the API responses when using Trace, as the conversion has not yet been indexed by Google.
</blockquote>

