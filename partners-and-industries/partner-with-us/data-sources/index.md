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

* [An Introduction to the Data Layer](https://docs.tealium.com/an-introduction-to-the-data-layer/)
* [JavaScript Install](https://docs.tealium.com/platforms/javascript/install/)

## API

API based integrations use the Tealium Collect HTTP endpoint or a custom endpoint to send data to the Tealium Customer Data Hub. This approach is useful if your system supports triggered callbacks or webhooks. The most common platforms for API integrations are CRM and email marketing platforms.

The following lists the available API data sources integrations:

- [Affirm](https://docs.tealium.com/affirm-incoming-webhook-setup-guide/)
- [Airship](https://docs.tealium.com/airship-incoming-webhook-setup-guide/)
- [Braze Currents](https://docs.tealium.com/braze-currents-data-source-setup-guide/)
- [Hubspot](https://docs.tealium.com/hubspot-workflow-incoming-webhook-setup-guide/)
- [Intercom](https://docs.tealium.com/intercom-incoming-webhook-setup-guide/)
- [Iterable](https://docs.tealium.com/iterable-incoming-webhook-setup-guide/)
- [Mailchimp](https://docs.tealium.com/mailchimp-incoming-webhook-setup-guide/) ([See example](#example-mailchimp))
- Salesforce
- [SendGrid](https://docs.tealium.com/sendgrid-incoming-webhook-setup-guide/)
- Zapier

Learn More

* [Tealium HTTP API](https://docs.tealium.com/platforms/http-api/)


## Benefits

Benefits of data source integrations include:

- Tealium users can easily onboard and unify data from various systems to create personalized customer experiences.
- Tealium users can identify the origin of all incoming data for a clearer understanding of their data supply chain.
- Higher quality of incoming data.


<blockquote>
Tealium offers a [file import data source](https://docs.tealium.com/about-file-import/) which processes CSV files from several cloud storage providers. However, file imports are not currently offered as an integration method for partners.
</blockquote>



## Example: Mailchimp

Mailchimp is an all-in-one marketing platform that offers webhooks for common email actions such as subscriptions, profile updates, email changes, and campaign statuses. For example, when MailChimp receives a subscribe action it can trigger a webhook with the data related to that event. In this case, the `subscribe` event type has the following fields (brackets indicate nested JSON):

```
{
  "type": "subscribe",
  "fired_at": "2009-03-26 21:35:57",
  "data[id]": "8a25ff1d98",
  "data[list_id]": "a6b5da1054",
  "data[email]": "api@mailchimp.com",
  "data[email_type]": "html",
  "data[merges][EMAIL]": "api@mailchimp.com",
  "data[merges][FNAME]": "Mailchimp",
  "data[merges][LNAME]": "API",
  "data[merges][INTERESTS]": "Group1,Group2",
  "data[ip_opt]": "10.20.10.30",
  "data[ip_signup]": "10.20.10.30"
}
```

Tealium's official data source integration with Mailchimp offers these additional benefits from using the generic HTTP API:

* **Dedicated Endpoint**  
Tealium issues a customized endpoint for this data source. For example: `https://collect.tealiumiq.com/integration/event/my_account/main/abc123`.
* **Variable Transposing**  
Tealium flattens the JSON body and prepends `mailchimp_` to all field names to give all MailChimp data its own namespace. For example, `"data[merges][EMAIL]"` becomes `mailchimp_data_merges_email`.

These benefits provide improved data quality and governance for all downstream data enrichments and actions. By combining the MailChimp data source with other data sources and activations, Tealium users maintain a more accurate and up-to-date single view of their customers.

Learn more: [MailChimp Incoming Webhook Setup Guide](https://docs.tealium.com/mailchimp-incoming-webhook-setup-guide/)

## Become a Partner

[Contact us](https://tealium.com/tealium-partner-network/) to integrate your technology.
