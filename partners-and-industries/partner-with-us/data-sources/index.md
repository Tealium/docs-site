---
title: Data Sources
description: Learn how to send data into Tealium from your application using inbound data integrations.
url: https://docs.tealium.com/partners-and-industries/partner-with-us/data-sources/
---

Data sources send data into Tealium. A data source can a website, a CRM system, a mobile SDK, a server-side application, or even a webhook. The number of possible data sources is endless, however there are two primary methods for sending data to Tealium: web-based and API-based. Choose the method that matches your platform to determine how you will send data to Tealium.

## Web

Web based integrations use the Tealium Universal Tag (utag.js) and Universal Data Object (utag_data) to load the Tealium Collect tag, a JavaScript tag that sends data to the Tealium Customer Data Hub. The most common web based integrations are CMS plugins. A Tealium plugin will add the necessary JavaScript tag and data layer object to the pages in the CMS.

A successful CMS integration loads the Universal Tag and dynamically populates a data layer with built-in system data, such as page name, site language, and user login status to name a few. An e-commerce platform would populate product and order variables on the relevant pages in the system.

Examples of web integrations include:

* JavaScript (Web)
* Angular
* Magento
* Shopify
* SiteCore

Learn More

* [An Introduction to the Data Layer]()
* [JavaScript Install](/platforms/javascript/install/)

## API

API based integrations use the Tealium Collect HTTP endpoint or a custom endpoint to send data to the Tealium Customer Data Hub. This approach is useful if your system supports triggered callbacks or webhooks. The most common platforms for API integrations are CRM and email marketing platforms.

The following lists the available API data sources integrations:

- [Affirm]()
- [Airship]()
- [Braze Currents]()
- [Hubspot]()
- [Intercom]()
- [Iterable]()
- [Mailchimp]() ([See example](#example-mailchimp))
- Salesforce
- [SendGrid]()
- Zapier

Learn More

* [Tealium HTTP API](/platforms/http-api/)


## Benefits

Benefits of data source integrations include:

- Tealium users can easily onboard and unify data from various systems to create personalized customer experiences.
- Tealium users can identify the origin of all incoming data for a clearer understanding of their data supply chain.
- Higher quality of incoming data.

Tealium offers a [file import data source]() which processes CSV files from several cloud storage providers. However, file imports are not currently offered as an integration method for partners.


## Example: Mailchimp

Mailchimp is an all-in-one marketing platform that offers webhooks for common email actions such as subscriptions, profile updates, email changes, and campaign statuses. For example, when MailChimp receives a subscribe action it can trigger a webhook with the data related to that event. In this case, the `subscribe` event type has the following fields (brackets indicate nested JSON):

```
{
  &#34;type&#34;: &#34;subscribe&#34;,
  &#34;fired_at&#34;: &#34;2009-03-26 21:35:57&#34;,
  &#34;data[id]&#34;: &#34;8a25ff1d98&#34;,
  &#34;data[list_id]&#34;: &#34;a6b5da1054&#34;,
  &#34;data[email]&#34;: &#34;api@mailchimp.com&#34;,
  &#34;data[email_type]&#34;: &#34;html&#34;,
  &#34;data[merges][EMAIL]&#34;: &#34;api@mailchimp.com&#34;,
  &#34;data[merges][FNAME]&#34;: &#34;Mailchimp&#34;,
  &#34;data[merges][LNAME]&#34;: &#34;API&#34;,
  &#34;data[merges][INTERESTS]&#34;: &#34;Group1,Group2&#34;,
  &#34;data[ip_opt]&#34;: &#34;10.20.10.30&#34;,
  &#34;data[ip_signup]&#34;: &#34;10.20.10.30&#34;
}
```

Tealium&#39;s official data source integration with Mailchimp offers these additional benefits from using the generic HTTP API:

* **Dedicated Endpoint**  
Tealium issues a customized endpoint for this data source. For example: `https://collect.tealiumiq.com/integration/event/my_account/main/abc123`.
* **Variable Transposing**  
Tealium flattens the JSON body and prepends `mailchimp_` to all field names to give all MailChimp data its own namespace. For example, `&#34;data[merges][EMAIL]&#34;` becomes `mailchimp_data_merges_email`.

These benefits provide improved data quality and governance for all downstream data enrichments and actions. By combining the MailChimp data source with other data sources and activations, Tealium users maintain a more accurate and up-to-date single view of their customers.

Learn more: [MailChimp Incoming Webhook Setup Guide]()

## Become a Partner

[Contact us](https://tealium.com/tealium-partner-network/) to integrate your technology.
