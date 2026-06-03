---
title: Workato glossary
description: This article describes terms used in the Workato interface and documentation.
url: https://docs.tealium.com/server-side/data-connect/glossary/
---
**[Actions](https://docs.workato.com/workato-concepts.html#steps-and-actions)**: Actions carry out an operation in your target app, such as a create, update, or search operation. Each action requires a set of input fields and typically returns data, for example, an output data tree.

**[Connections](https://docs.workato.com/connectors.html)**: The building blocks of recipes. Connectors are comprised of authentication configurations, triggers, and actions for a specific third-party application. Documentation will often refer to these as &#34;apps&#34;.

**[Datapill](https://docs.workato.com/workato-concepts.html#datatree-and-datapills)**: Datapills are output data from a trigger or an action step. They are variables that you can use to map business logic into recipe steps.

**[Jobs](https://docs.workato.com/workato-concepts.html#jobs)**: A subunit of a recipe that includes processing a trigger event and running a series of actions.

**[Recipes](https://docs.workato.com/workato-concepts.html#recipes)**: The Workato automated workflows. Recipes can trigger actions to pull data from a data source, retry actions when errors occur, and send events to Tealium. Data Connect users can create, edit, delete, and run recipes depending on their permissions settings.

**[Steps](https://docs.workato.com/recipes/steps.html#action-step)**: Recipe steps can be actions, or control flow statements that help you describe business logic. Examples of steps in a Tealium recipe are: action steps, repeat steps, handle errors steps.

**[Task](https://docs.workato.com/recipes/tasks.html#tasks)**: A subunit of a recipe that requires computational resources. For example, each connector action (batch processing, emailing results, error handling, and so on) counts as one task. A recipe job may consist of more than one task and the number of tasks depend on the recipe logic and data of the trigger event.
 Each Data Connect-enabled Tealium account has a task limit for all profiles in that account. Contact your Tealium Customer Success Manager for more information about Data Connect task limits.

**[Triggers](https://docs.workato.com/workato-concepts.html#triggers)**: Determine what events to listen for to execute the actions described in a recipe. Triggers can be real-time or scheduled. 

For more information about Workato terms, see [Concepts](https://docs.workato.com/workato-concepts.html#recipes) in the Workato documentation.