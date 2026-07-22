---
title: About Data Connect integrations
url: https://docs.tealium.com/server-side/data-connect/manage-data-connect-integrations/about-integrations/
---

<blockquote>
To enable Data Connect and begin creating and managing recipes, [contact support](https://docs.tealium.com/support/).
</blockquote>


Data Connect uses Workato to create automated, low-code integrations that let you customize how and when to bring your data into Tealium.

Using custom [recipes](https://docs.tealium.com/workato-glossary/), you can select specific schedules, [triggers](https://docs.tealium.com/workato-glossary/), [actions](https://docs.tealium.com/workato-glossary/), and error handling for your source data.

## Prerequisites

* Learn [Workato terms](https://docs.tealium.com/workato-glossary/) for recipes in Tealium.
* Read the [Workato documentation](https://docs.workato.com/recipes/building-recipes.html) to learn about recipe design.
* Use [Workato tutorials](https://docs.workato.com/getting-started/build-first-recipe.html) to build your first recipe.
* Want to get more in depth training in Workato recipes? Sign up for a [Workato certification](https://docs.workato.com/training/automation-institute.html#what-is-automation-institute).
* Familiarize yourself with [Data Connect recipe best practices](https://docs.tealium.com/data-connect-recipe-best-practices/).

## IP addresses to allow

Your security requirements or third-party app may require you to add Data Connect IP addresses to your allowlist. For more information on IP addresses associated with Data Connect, see [Traffic from Workato](https://docs.workato.com/security/ip-allowlists.html#traffic-from-workato) in the Workato documentation.

## Create a recipe

Creating any recipe in Data Connect follows the same basic workflow:

1. [Set up a Tealium Connect data source](https://docs.tealium.com/tealium-connect-data-source/).
1. [Create an event specification](https://docs.tealium.com/tealium-connect-event-spec/).
1. [Set up enrichments for visitor ID attributes in AudienceStream](https://docs.tealium.com/tealium-connect-visitor-id-attr-enrichment/).
1. [Create a recipe](https://docs.tealium.com/create-recipe-data-connect/).
1. [Select a trigger](https://docs.tealium.com/create-recipe-data-connect/#step-1-select-a-trigger).
1. [Configure an action](https://docs.tealium.com/create-recipe-data-connect/#step-2-configure-an-action).
1. [Configure error handling](https://docs.tealium.com/create-recipe-data-connect/#step-3-configure-error-handling).
