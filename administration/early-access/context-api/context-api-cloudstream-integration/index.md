---
title: Context API and CloudStream integration guide
description: Configure Context API to retrieve real-time visitor data from CloudStream segments.
url: https://docs.tealium.com/administration/early-access/context-api/context-api-cloudstream-integration/
---
## How it works

Context API supports a direct integration with CloudStream, letting you create real-time personalizations using data directly from your data cloud. Retrieve visitor data from CloudStream segments based on cloud data sources like Snowflake or Databricks.

This integration creates a bridge between your data cloud and real-time API responses, enabling personalization scenarios that combine the scale of your data warehouse with the low-latency performance of Context API.

The integration requires configuration in both your CloudStream profile and Context API.

## Prerequisites

* CloudStream profile with at least one configured cloud data source
* CloudStream segments created using cloud attributes
* Context API enabled for your account

## Step 1: Configure the cloud data source

In your CloudStream profile, configure the Context API integration for each cloud data source you want to use with Context API:

1. Go to **Connect > Data Sources** in your CloudStream profile.
1. Either create a new cloud data source or edit an existing one.
1. Navigate to the **Context API Integration** section in the data source configuration.
1. Enable **Context API Integration**.
1. Select the cloud data source column that contains a unique identifier for each record.
    * This identifier should be unique per visitor or entity (for example, a visitor ID, customer ID, or email address).
    * Only columns with string or number data types are supported.
    * The value for this column will be used for the `momentsApiId` parameter in the Context API endpoints.
1. Complete the rest of the data source configuration and save your changes.

The cloud data source is now available as a source for Context API engines.

## Step 2: Create CloudStream segments

Create segments in your CloudStream profile that define the audiences you want to make available through Context API:

1. Go to **Audience** in your CloudStream profile.
1. Create segments using the cloud attributes from your data sources.
1. Save and enable the segments you want to use with Context API.

These segments will be available to select when configuring your Context API engine.

## Step 3: Configure the Context API engine

In your Context API configuration, add the CloudStream data sources and segments you want to include in the API response:

1. Go to **CloudStream > Context API** in your CloudStream profile.
1. Either create a new engine or edit an existing one.
1. In the **Details** screen, configure the engine name, enable status, and domain allow list.
1. Click **Next**.
1. In the **Cloud Data Source** screen:
    * Click **Add Data Source** to add a cloud data source.
    * For each cloud data source you add, select the CloudStream segments to use in the engine configuration.
    * Records from all selected segments will be prepopulated in the engine configuration.
1. Click **Next**.
1. In the **Response** screen, verify that the CloudStream segments appear as audiences in the **Example Response**.
    * You can select additional CloudStream attributes if needed. Supported data types: number, string, boolean, and date.
    * Choose whether to use IDs or names for attributes in the response payload.
1. Review the **Example Response** panel to verify your configuration.
1. Click **Next** and review the engine summary.
1. Click **Done** to save the engine.

## Step 4: Call the Context API endpoint

Use the `momentsApiId` parameter to retrieve visitor data from CloudStream segments.

### Context API endpoint 

```bash
GET https://personalization-api.{REGION}.prod.tealiumapis.com/personalization/accounts/{ACCOUNT}/profiles/{PROFILE}/engines/{ENGINE_ID}/visitors/{momentsApiId}?suppressNotFound={SUPPRESS_NOT_FOUND}
```

### Parameters

| **Parameter** | **Type** | **Description** |
|---|---|---|
| `momentsApiId` | String<br>Path parameter | The value of the cloud attribute configured in the cloud data source Context API Integration. This is the value of the attribute for the column you selected in Step 1. Special characters must be encoded.
|
| `suppressNotFound` | Boolean<br>Query parameter | Determines the response type when a visitor is not found. Default is `false`.<br> `true` - Returns HTTP 200 with an empty response body.<br> `false` - Returns HTTP 404. |

### Example request

```bash
GET https://personalization-api.us-west.prod.tealiumapis.com/personalization/accounts/example-account/profiles/cloudstream-profile/engines/abc123/visitors/user%40example.com?suppressNotFound=true
```

In this example:
* `user%40example.com` is the value of the cloud attribute mapped in the cloud data source configuration.

### Response format

The response follows the standard Context API response format with audiences from CloudStream segments included:

```json
{
    "audiences": [
        "30 Days Since Last Login"
    ],
    "metrics": {
        "Total direct visits": 1
    },
    "properties": {
        "Company Name": "<attr_value>"
    },
    "flags": {
        "Returning visitor": false
    },
    "dates": {
        "First visit": 1491233145706
    }
}
```

## Best practices

* **Choose stable identifiers**: Select columns that contain stable, unique identifiers that persist across sessions (for example, customer ID or email hash).
* **Test with suppressNotFound**: During testing, use `suppressNotFound=true` to avoid HTTP 404 responses for visitors not found in the data source.
* **Monitor segment membership**: Ensure your CloudStream segments are configured to capture the visitor populations you expect in Context API responses.
* **Coordinate updates**: Changes to cloud data source configurations may affect Context API responses. Coordinate updates across both systems.

## Related documentation

* [about-cloudstream](https://docs.tealium.com/about-cloudstream/)
* [about-cloud-data-sources](https://docs.tealium.com/about-cloud-data-sources/)
* [manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)
* [about-context-api](https://docs.tealium.com/about-context-api/)
* [context-api-endpoint](https://docs.tealium.com/context-api-endpoint/)
* [context-api-manage-engines](https://docs.tealium.com/context-api-manage-engines/)
