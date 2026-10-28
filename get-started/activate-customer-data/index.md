---
title: Activate customer data
description: Learn how Tealium activates customer data in real time by pushing it to your vendors through connectors or returning it to apps and AI agents on request.
url: https://docs.tealium.com/get-started/activate-customer-data/
---
Activation turns event and profile data into action. A reminder email follows a cart abandonment, an ad campaign stops targeting visitors after they buy, and a home page greets returning visitors with the products they browsed last time.

## Push data with connectors and functions

Connectors send data to the vendors you already use, such as email, advertising, analytics, and CRM platforms, in real time. You configure each integration in Tealium instead of building and maintaining a separate data pipeline for every vendor.

Each connector runs actions. An action decides what data to send to the vendor and when:

* **Audience actions**: Send data when a visitor joins or leaves an audience, or at the start or end of a visit. Use audience actions to add cart abandoners to an email series or to remove buyers from an ad campaign as soon as they convert.
* **Event actions**: Send data for every event in an event feed, without waiting for profile history. Use event actions to send page views to your analytics vendor or orders to your CRM.

When a connector doesn't fit your use case, functions run your own JavaScript code, so they can apply any logic that JavaScript supports, such as calling an external API. Data transformation functions clean up incoming events before Tealium processes them. Event functions and visitor functions run after processing, so they can act on the finished event or profile.


![](https://docs.tealium.com/images/icons/icon-connector.svg)

#### Connectors

Learn how connectors and actions send data to your vendors.



![](https://docs.tealium.com/images/icons/icon-product-functions.svg)

#### Functions

Learn how to run your own code on events and visitors.


## Pull data on request

Some experiences need data at the moment a visitor arrives. When a returning visitor opens your home page, the page needs that visitor's interests before it finishes loading. Tealium returns a visitor's current audiences, badges, and attributes on request, so your website, app, or service workflow can personalize the experience in real time.

The Context API returns only the data each experience needs, not the whole visitor profile. AI agents use it the same way, through the Context API MCP server. For more information, see [Use AI with Tealium](https://docs.tealium.com/use-ai-with-tealium/).


![](https://docs.tealium.com/images/icons/icon-moments-api.svg)

#### Context API

Learn how apps and services retrieve current visitor data on request.

