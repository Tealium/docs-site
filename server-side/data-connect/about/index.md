---
title: About Data Connect
description: This article provides an overview of Tealium Data Connect.
url: https://docs.tealium.com/server-side/data-connect/about/
---
 Data Connect is an add-on feature for Tealium customers. If you are already a Tealium customer, contact your Customer Success Manager for a demo and to learn more about Data Connect. If you are a new customer, [contact us](https://tealium.com/products-real-time-data-collection-and-quality/tealium-data-connect/) to request a demo. 

Tealium Data Connect provides a fast, efficient, and scalable architecture to import valuable data from your SaaS applications, CRMs, and data warehouses to Tealium. Use Data Connect to integrate data from your enterprise systems into Tealium AudienceStream CDP or EventStream API Hub for enrichment and real-time personalization and activation.

With Data Connect, you can automate, schedule, and enhance your data workflows to leverage your data in new ways, such as:

* Increase customer engagement through better personalization
* Lookalike audience targeting
* Targeting of qualified leads
* Opt-in/out updates to customer records

## Requirements

* Tealium EventStream or AudienceStream

Data Connect uses third-party iPaaS technology that requires third-party cookies to be enabled in your browser.

## How it works

Data Connect uses [Workato](https://www.workato.com/), a third-party iPaaS technology, to provide integrations with commonly used systems. A Workato integration consists of an app connection and a recipe that contains the rules and data mapping logic to extract data from the app.

The following figure shows the flow of data from your internal systems to Tealium:

![](/images/server-side/dc-events-workflow.png)

Begin by selecting the app you want to connect to Tealium. By using the Data Connect Workato solution, you can then customize how and when you send event data to Tealium. To receive data from Workato, Data Connect uses the Tealium Connect data source with advanced Tealium Collect HTTP API logic specifically designed for Data Connect. You can then use these events in attribute enrichments or connectors in Tealium EventStream, AudienceStream, and Functions.

For more information about Workato integrations, see [About Data Connect integrations]().

## Key benefits

Key benefits of Tealium Data Connect include:

* **Get started quickly with low-code integrations**  
Use the Data Connect Workato integration to easily configure connectors and build recipes with little to no coding.
* **Import data on your schedule or automatically**    
Import net-new events based on an existing dataset using a Workato recipe that imports data on your schedule or automatically in a batch when the source data changes.
* **Use customized, automated workflows** 
Data Connect Workato recipes let you choose what kinds of triggers to use, what apps and actions you can call, and how to configure error handling for your business case. 
* **Complement real-time data and insights with historical context from other systems**  
Import valuable data from systems like Snowflake, Salesforce, Hubspot, etc. and make it actionable in Tealium. Gain easier access to sources like data warehouses, CRM systems, and cloud applications.
* **Add data translations directly into your workflow**  
Using recipes, you can add data translations into your automated workflow making the process of importing data to Tealium more efficient.



## Next steps

Ready to get started with Data Connect?

* Learn [Workato terms]() for recipes in Tealium.
* Read the [Workato documentation](https://docs.workato.com/recipes/building-recipes.html) to learn about recipe design.
* Use [Workato tutorials](https://docs.workato.com/getting-started/build-first-recipe.html) to build your first recipe.
* Want to get more in depth training in Workato recipes? Sign up for a [Workato certification](https://docs.workato.com/training/automation-institute.html#what-is-automation-institute).

When you’re ready, see [About Data Connect integrations](), for more information about recipe creation in Tealium.


