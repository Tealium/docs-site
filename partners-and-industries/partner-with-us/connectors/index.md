---
title: Connectors
description: Learn how to integrate your server-side API for real-time activation of event and customer data in Tealium.
url: https://docs.tealium.com/partners-and-industries/partner-with-us/connectors/
---

Do you offer an API for data collection or activation? Do you have a server-side equivalent to your client-side JavaScript tag? If so, this guide explains how API integrations for outbound data work in the Tealium Customer Data Hub.

## How Connectors Work

A _connector_ is an integration between Tealium and a vendor for transmitting data. A connector offers _actions_ that represent methods from a vendor's API. Connectors provide Tealium users a simplified workflow for activating data in real-time and sending it directly to a vendor.

### Event and Customer Data

Connectors that send _event data_, such as web analytics, are used in [Tealium EventStream](https://docs.tealium.com/introduction-to-eventstream/).

Connectors that send _customer data_, such as email subscription status, are used in [Tealium AudienceStream](https://docs.tealium.com/introduction-to-audiencestream/).

### Configuration

A connector is managed in the following parts:

* **Connector**  
The connector establishes a connection to the vendor, usually with an API key or account ID, or even [authentication credentials](#authentication).
* **Actions**  
Actions implement a specific vendor API method. Each action requires a source of data (event or customer), data mappings, and any required vendor settings. Multiple actions are associated with a single connector.
* **Data Mappings**  
Data mappings determine which dynamic values from the event or customer are sent to the vendor.

### Action Examples

The following examples show common connector actions from various vendor categories:

* **Analytics**  
Send an analytics event such as a page view, order purchase, or user registration.
* **Display Ads**  
Add or remove from an advertising segment.
* **Email**  
Add or remove from a list, trigger email, or add relational data for a subscriber.
* **CRM**  
Create a lead or contact, convert a lead, or upsert (insert or update) a record.
* **Mobile**  
Send an SMS or a push notification, track an app install, or send in-app events.

[Learn more about connectors](https://docs.tealium.com/audiencestream-connectors/).

## Example: Facebook Audiences Connector

With the [Facebook Audiences Connector](https://docs.tealium.com/facebook-audiences-connector/) for Facebook Ads users, Tealium users are able to manage their custom audiences in real-time, based on user behavior collected from one or more data sources.

This connector provides the following actions:

* Add User to Custom Audience
* Remove User from Custom Audience
* Opt Out User from All Custom Audiences

For each action, a list of required and optional fields for Facebook Custom Audiences is available for data mapping.

## Authentication

In cases where a vendor API requires authentication, Tealium offers two solutions:

* **Tealium-Provided Credentials**  
Tealium creates and manages a server-side app to act on behalf of our users. Tealium maintains the authentication relationship with the vendor.
* **Customer-Provided Credentials**  
The Tealium user obtains the necessary API access from the vendor to authenticate the connection.

For both solutions, Tealium supports the following authentication types:

- Basic Auth (username and password)
- OAuth 2.0
- JSON Web Tokens (JWT)


<blockquote>
If your API places limits on the number of concurrent tokens, Tealium users may encounter issues since we are globally distributed across dozens of servers at any given time.
</blockquote>


## Best Practices

### Asset Creation

Asset creation is the ability for Tealium users to create resources for use with a connector without leaving the Tealium Customer Data Hub (CDH). For example, in the Facebook Audiences connector, users are able to create a new Facebook custom audience and then select that audience as the target for a new connector action.

This optional feature is provided for all vendors that support API methods to create resources that are related to a connector action. Some common examples of create methods include:

- **Display Ads**  
Create advertiser segment or audience.
- **Email**  
Create subscriber list or contact list.

### Dynamic Vendor Options

Tealium assists users in configuring a connector action by dynamically populating connector options with data retrieved directly from the vendor's platform.

For example, on the configuration screen of the Facebook Audiences connector, Tealium makes API calls to get the list of custom audiences from the user's Facebook Ads account. This permits the user to browse their external resources with familiar names and helpful metadata to ensure they are selecting the right resources.

These dynamic configuration options may sometimes need to be executed as sequential calls. In a CRM connector, for example, to fetch a CRM object's primary key field, we must first retrieve the list of CRM objects.

### Upsert by Default

For API methods that create or update records in a vendor platform, Tealium prefers native support for `upsert` in a single request. This will minimize the number of outgoing API calls from Tealium. For example, before creating or updating a record, an API user must first verify whether a record exists. If the record doesn't exist, the next API call will create the record. If the record does exist, the next API call will update the existing record.

### Batching and Rate Limits

While Tealium's goal is to provide real-time performance, some vendors prefer that data be sent in small batches to manage resource costs. This is especially true when dealing with large volumes of data.


<blockquote>
We recommend that vendors rate limit individual accounts using their APIs. This prevents a small group of high-volume accounts from impacting your entire system.
</blockquote>


Tealium connectors conform to the thresholds you want for the API endpoints used. The following are rate limits examples:

- 50 events per request with a maximum of 10 requests per second = 500 requests/second
- 10,000 events per minute with a maximum 10KB per request = ~167 requests/second

## Limitations

Tealium connectors do not currently support the following:

- File transfers
- Vendor APIs that do not connect within 5000ms
- Vendor APIs that do not respond to requests within 5000ms (10s for batch requests)

## Become a Partner

[Contact us](https://tealium.com/tealium-partner-network/) to integrate your technology.
