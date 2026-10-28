---
title: Follow a customer through Tealium
description: See how Tealium collects, enriches, and activates one customer's data across your website, app, data cloud, and support team.
url: https://docs.tealium.com/get-started/follow-a-customer-through-tealium/
---
This example follows one customer, Alex, through a retailer's Tealium setup.

## Collect events from the website and app

Alex visits the retailer's website without logging in and views several pairs of running shoes. The collection tag sends each product view to Tealium as an event with attributes such as the product ID and category. Tealium creates a new anonymous visitor profile for Alex and updates it from each event. Later, Alex opens the mobile app, and Tealium creates a separate visitor profile for the app.

For more information, see [Collect customer data](https://docs.tealium.com/collect-customer-data/).

## Merge profiles and update attributes

Alex logs in to the app with an email address. The email address populates the visitor ID attribute, and visitor stitching merges Alex's web and app profiles into one. Enrichments set Alex's favorite category to running shoes, and Alex joins the `High-intent shoppers` audience.

For more information, see [Build visitor profiles](https://docs.tealium.com/build-visitor-profiles/).

## Activate data in real time

Alex adds running shoes to a cart and leaves without buying. Alex joins the `Cart abandoners` audience, and an audience action sends Alex's profile data to the email platform, which sends a reminder. The next day, Alex opens the app. The app requests Alex's current profile data and shows running shoes first.

For more information, see [Activate customer data](https://docs.tealium.com/activate-customer-data/).

## Add data from the data cloud

Each night, a model in the retailer's data cloud scores customers for churn risk. A cloud data source imports Alex's score, and Alex's profile updates. Separately, the marketing team activates a segment of recent buyers in place, without copying the data into Tealium, to exclude those buyers from paid media campaigns.

For more information, see [Work with your data cloud](https://docs.tealium.com/work-with-your-data-cloud/).

## Give an AI agent customer context

Alex contacts support about a late order. An AI enrichment has already inferred from Alex's recent browsing that Alex is comparing products. The support team's AI agent pulls Alex's profile through the Context API MCP server, sees the high churn risk score, and suggests a discount on the next order.

For more information, see [Use AI with Tealium](https://docs.tealium.com/use-ai-with-tealium/).

## Respect a consent change

Alex withdraws consent for marketing on the website. The consent manager blocks the marketing tags, and consent orchestration stops event connectors from sending Alex's events to marketing vendors. To exclude Alex from audience connectors, the retailer uses manual consent enforcement.

For more information, see [Govern customer data](https://docs.tealium.com/govern-customer-data/).
