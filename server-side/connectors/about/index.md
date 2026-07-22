---
title: About connectors
description: This article describes how to add and configure connectors for Tealium EventStream API Hub and Tealium AudienceStream CDP.
url: https://docs.tealium.com/server-side/connectors/about/
---
## How it works

A connector is an integration that transmits data between Tealium and another vendor in real-time. A connector offers actions that represent vendor-supported APIs. An action is triggered in real-time by an incoming event from a feed or a visitor joining or leaving an audience. An action sends data based on mappings that associate Tealium attributes to the expected vendor parameters.

In CloudStream, segment data is not persisted or stored in Tealium systems. After retrieving the data and sending it to configured connectors, Tealium discards it.

### Terminology

* **Connector**  
A connector represents the connection to your vendor account. The connection is configured using credentials such as an account ID, username and password, or an API key.
* **Action**  
An action is a vendor operation, such as triggering an email, building a custom audience, or managing leads. Actions vary depending on the vendor service. Multiple actions can be associated with a single connector.
* **Frequency Cap**  
A connector action performs in real-time, but some actions are designed to have a wait period before they are triggered. The frequency cap lets you set a downtime period for actions so that they do not trigger immediately. For more information, see [action-frequency-capping-amp-prioritization](https://docs.tealium.com/action-frequency-capping-amp-prioritization/).
* **Source**  
Source indicates the origin of the data being acted upon. A source can be an audience or an event feed.

### Consent categories

Each connector in the marketplace has one or more consent categories assigned for each available action. The consent information for a connector action is shown on the **Action Details** screen, under **Additional Details**. 

![](https://docs.tealium.com/images/server-side/eventstream-connector-consent-categories.png)

AudienceStream is categorized in the **CDP** consent category and DataAccess is categorized in the **Big Data** consent category. For additional information about server-side consent, see [Consent Preferences Manager](https://docs.tealium.com/iq-tag-management/consent-management/consent-preferences-dialog/manage/).

### Retries

If a connector action fails, it is retried three times at 1-minute, 5-minute, and 30-minute intervals. If the request is successful on any of the subsequent retry attempts, the request is reported as a success in the UI. If all three retries fail, the request is dropped and reported as an error in the UI.

A retry is attempted when any of the following error codes occur:

* 408 – Forbidden
* 429 – Too Many Requests
* 500 – Internal Server Error
* 502 – Bad Gateway
* 503 – Service Unavailable
* 504 – Gateway Timeout

A retry is not attempted when a **Response Timeout - Vendor API did not respond within 5000 milliseconds** response is received. The request payload was sent, but the vendor did not send a response within our allowed time of five seconds. The request may have succeeded on the vendor's side, but because it took longer than five seconds to get a response, we treat it as a failure.

### Overload protection

Connectors perform actions through multiple instances of a data handler. Sometimes, data handlers encounter transmission errors with vendors. If errors exceed a configured threshold, Tealium can pause or throttle data transmission to vendors until the error rate drops.

For example, if the overall rate of failure for an instance exceeds 40% per 100 attempts, that instance pauses processing actions for 1 minute. The instance then attempts to process half of the actions in the queue. If the failure rate for these 50 attempts remains above 20%, the instance pauses for another 60 seconds before trying again. Otherwise, the instance resumes full operation.

Tealium activates and adjusts the thresholds at the various levels as needed to ensure maximum success and performance for customers.

### Restricted data

Restricted data settings do not apply to connectors. Attributes marked as restricted data are always included, whether you are sending them through mappings or as part of the visitor profile. This cannot be changed. Learn more about [Restricted Data](https://docs.tealium.com/about-restricted-data/).

### IP allow lists

If a connector you use has strict rules about which systems it accepts requests from, you can add the IP addresses of the Customer Data Hub to your allow list. The IP addresses that make connector requests can be found in the [IP Addresses for Customer Data Hub]().

### Visitor identity synchronization

To improve visitor identity matching between Tealium and third-party vendors, use a cookie matching tag. A cookie matching tag synchronizes visitor identifiers between Tealium and the vendor. It requests a third-party identifier, receives an anonymous ID, and saves it in a cookie. This enables more accurate tracking and enriched data for connector actions. For more information, see [About persistent cookie matching](https://docs.tealium.com/about-persistent-cookie-matching/).

## Screen navigation

### Overview screen

The connectors overview screen displays the following data about each connector:

* **Actions**  
The number of connector actions configured for each data type (event and visitor). Click the information (i) icon to display the timeline for the total in this column.
* **Total Volume**  
The number of actions triggered for the connector.
* **Success**  
The number of action successes.
* **Error**  
The number of action errors.
* **Date Modified**  
The date the connector was last modified. 
* **Labels**  
The labels applied to the connector.
* **Status**  
The connector status, which can be **Active**, **Inactive**, or **Deprecated**.

Export metrics (total volume, successes, errors, and retries) for all connectors by clicking **Export Metrics**. The data downloads as a CSV file.

Expand the menu for a connector to access additional actions: **Edit Labels**, **Duplicate**, and **Delete**:

![](https://docs.tealium.com/images/server-side/connectors/connector-menu-expanded.png)

For more information, see [Add a connector]().

### Details screen

When you click a connector action, the connector details screen appears. The **Overview** tab is displayed by default and shows information about action trends, including successful actions, actions with errors, and a graph of the delivery status.

![](https://docs.tealium.com/images/server-side/connectors/connector-details-status.png)

You can view the trends data for the **Past 24 hours**, **Past 7 days**, or **Past 30 days**. The default is the **Past 24 hours**. Successful actions are shown in green and errors are shown in blue. Click any part of the graph to view a summary of the data for that display.

#### View sampled errors for an action

Use the following steps to view error information for a connector action:

1. Go to **Connect > Connectors**, then select a connector.
1. Click the **Actions** tab, then select an action that has errors.  
The **Action Details** screen is displayed.
1. Under **Trends**, select **24 Hours**, **7 Days**, **30 Days**, or a custom date range.
1. Below the graph, a list of error messages is shown. Each entry in the list displays the error category, the message, the number of errors included in the report, and the total number of occurrences of the error.
1. To view the details for an error, click the list entry.  
The detailed view includes a sample of the affected code with a timestamp containing the day of the week, the date, and the time.

#### Export sampled errors

Use the following steps to export sampled errors for a connector:

1. Go to **Connect > Connectors**, then select a connector.
1. Click the **Actions** tab, then select an action that has errors.  
The **Action Details** screen is displayed.
1. Click **Export Sampled Errors**.  
The errors are exported to a CSV file that is saved to your default download location.
1. Open the CSV file to examine the details or share the file with others for further collaboration.

### Deprecated connectors and actions

Connectors and actions can be deprecated, which means they may be unsupported or removed in the future. Deprecation typically occurs when a connector or an action has been replaced with a newer version or a new connector or action that should be used instead.

There are two types of deprecation, as follows:

* **Functional Deprecation** – The connector or action is deprecated, and may be removed in the future, but is still working.
* **Full Deprecation** – The connector or action is deprecated and no longer works. Actions for a fully deprecated connector are not executed.

![](https://docs.tealium.com/images/server-side/connectors/deprecated-status.png)