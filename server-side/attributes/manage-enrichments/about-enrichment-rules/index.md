---
title: About enrichment rules
description: This article explains how rules work in attribute enrichments and when to apply them for event, visit, and visitor attributes.
url: https://docs.tealium.com/server-side/attributes/manage-enrichments/about-enrichment-rules/
---
A rule defines a condition that must be true before an enrichment runs. Rules determine when enrichments run and what data gets applied to attributes.

Without rules, enrichments run too broadly, which can lead to:

* Enrichments running on every event
* Attributes being overwritten with empty or incorrect values
* Inconsistent data quality over time

Rules let you:

* Restrict enrichments to specific event types
* Prevent unintended overwrites
* Align attribute behavior with business logic

Rules are especially important for event-driven data, where attributes are not populated on every event.

For instructions on applying a rule when adding an enrichment, see [Add an enrichment]().

## How rules work

A rule is made up of one or more condition groups. Each condition evaluates an attribute value against a filter using an operator (such as `equals`, `contains`, or `greater than`). Conditions are evaluated as follows:

* Conditions within a group use AND logic. All conditions in the group must be true.
* Conditions for multiple groups use OR logic. If any group evaluates to true, the enrichment runs.

Rules are evaluated against incoming event data and existing attribute values at the time the enrichment is processed.

## Rules for event attributes

Event attributes receive values directly from incoming event data. These values are not guaranteed to exist on every event.

If you do not apply a rule, the enrichment runs on every event, even when the source data is missing. Running on every event can overwrite valid values with empty or null values.

For example, `order_total` is populated only on purchase events. If you enrich a visitor attribute using `order_total` without a rule:

* The enrichment runs on all events.
* Events without `order_total` overwrite the stored value with an empty value.

Always add a rule to event attribute enrichments to restrict them to events where the data exists.

The following rule restricts an enrichment to purchase events:


[
  [
    {
      &#34;input&#34;: &#34;tealium_event&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;purchase&#34;
    }
  ]
]


## Rules for visit and visitor attributes

Visit and visitor attribute enrichments use the **WHEN** setting to define timing:

* New visitor
* New visit
* Any event
* Visit ended

Rules add a second layer of control on top of the **WHEN** setting. The two settings work together as follows:

* **WHEN** determines when the enrichment is allowed to run.
* **Rule** determines which events qualify.

For example, a &#34;Lifetime Order Total&#34; attribute may use:

* **WHEN**: Any event
* **Rule**: `tealium_event equals purchase`

The rule allows the enrichment to run during the visit, but only on purchase events.

## When to use a rule

Always use a rule when:

* The source data is not present on every event.
* The enrichment should apply only to specific event types.
* You are updating or overwriting an existing value.
* The attribute depends on a specific user action.

In practice, these conditions apply to most event-driven enrichments.

## Examples

### Restrict to a specific event type

Use this pattern to run an enrichment only when `tealium_event` matches a specific value:


[
  [
    {
      &#34;input&#34;: &#34;tealium_event&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;purchase&#34;
    }
  ]
]


### Multiple conditions (AND logic)

Add multiple conditions to the same group to require all conditions to be true:


[
  [
    {
      &#34;input&#34;: &#34;tealium_event&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;purchase&#34;
    },
    {
      &#34;input&#34;: &#34;product_category&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;Electronics&#34;
    }
  ]
]


### Multiple groups (OR logic)

Add separate groups to allow either condition to trigger the enrichment:


[
  [
    {
      &#34;input&#34;: &#34;tealium_event&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;checkout&#34;
    }
  ],
  [
    {
      &#34;input&#34;: &#34;tealium_event&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;purchase&#34;
    }
  ]
]


### Visitor attribute condition

Rules can also evaluate visit or visitor attributes:


[
  [
    {
      &#34;input&#34;: &#34;loyalty_member&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;true&#34;
    }
  ]
]


## Advanced considerations

When designing rules, consider how the enrichment behaves over time:

* **Overwrite behavior**: If the enrichment sets a value, ensure it runs only when valid data is present.
* **Event frequency**: High-frequency events increase the risk of unintended overwrites.
* **Attribute purpose**: Decide whether the attribute represents a single moment (for example, most recent order), a cumulative value (for example, total spend), or a state (for example, registered user). Each pattern requires different rule logic to produce consistent results.

## Related topics

* [About attributes]()
* [About enrichments]()
* [Add an enrichment]()
* [Enrichment usage examples]()