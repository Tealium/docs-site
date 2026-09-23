---
title: Developer Portal analytics
description: Monitor API usage, performance, and errors for your applications in the Tealium Developer Portal.
url: https://docs.tealium.com/administration/early-access/developer-portal/dev-portal-analytics/
---
Use the Tealium Developer Portal Analytics to monitor API usage, performance, and error rates for your applications. Filter by time frame (24 hours, 7 days, 30 days, or 90 days), application, and API.

## Summary metrics

The top of the Analytics screen shows the following metrics for the selected time range:

| Metric | Description |
|---|---|
| Total Requests | Total number of API calls made by your applications. |
| Success Rate | Percentage of requests that returned a 2xx status code. |
| Avg Response Time (ms) | Average response time, in milliseconds, across API requests. |
| Error Count | Number of requests that returned 4xx or 5xx status codes. |

## Charts

The Analytics screen includes charts for reviewing API activity over time.

### Request Volume

The Request Volume chart shows 2xx, 4xx, and 5xx responses over the selected time range. Use this chart to identify traffic patterns, peak usage periods, and increases in client or server errors.

### Response Time

The Response Time chart shows average API response time over the selected time range. Use this chart to identify performance changes or request patterns that might require optimization.

### Status Distribution

The Status Distribution chart shows responses grouped by status code category:

| Status code category | Description |
| --- | --- |
| 2xx | Successful requests. |
| 4xx | Client errors, such as authentication failures, invalid parameters, or missing scopes. |
| 5xx | Server errors. If 5xx errors continue, contact Tealium Support. |

### Top APIs

The Top APIs chart shows APIs ranked by request count. Use this chart to identify which APIs receive the most traffic.

## Filter analytics data

Use the filters at the top of the Analytics page to narrow the analytics data:

| Filter | Description |
| --- | --- |
| Time range | Select **24h**, **7d**, **30d**, or **90d**. |
| Application | Select a specific application, or select **All Applications** to view data across all applications. |
| API | Select a specific API, or select **All APIs** to view data across all APIs. |

## Troubleshoot common patterns


### High 403 error rate

A high volume of 403 (Forbidden) responses usually indicates an authorization issue. Check the following:

* Your subscription scopes allow the operations you are performing.
* Your account and profile assignments include the resources you are trying to access.
* Your token requests include all required scopes.

### High 401 error rate

A high volume of 401 (Unauthorized) responses usually indicates an authentication issue. Check the following:

* Your access tokens have not expired before sending requests.
* You have implemented proactive token renewal to avoid using expired tokens.
* Your stored client credentials, including the client secret, are current.

### Increasing response times

If response times are increasing, check the following:

* Look for 429 (Too Many Requests) responses, which indicate rate limiting.
* Use pagination for requests that return large result sets.
* Review request patterns and reduce unnecessary request volume where possible.
