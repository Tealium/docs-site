---
title: Booleans vs. Badges
description: This guide provides a comprehensive comparison between boolean and badge visitor attributes.
url: https://docs.tealium.com/guides/booleans-vs-badges/
---
Booleans and badges are both essential attributes used to capture and represent different types of visitor data. However, they serve distinct purposes and are applied in different scenarios.

## Definitions

![](/images/icons/icon-boolean-flag.png)

### Booleans

Booleans are simple true/false attributes that represent the customer&#39;s inherent state or current status. They are used for atomic attributes, representing a single piece of information about a visitor. They do not change unless explicitly updated.

Examples of visitor booleans include:

  * `is_verified`: Whether a visitor has verified their email address.
  * `has_valid_payment`: Whether a visitor has a valid method of payment on their account.
  * `is_internal_user`: Whether a visitor is an internal user.

![](/images/icons/icon-badge.png)

### Badges

Badges are visitor-only attributes that represent more complex behavior patterns and are assigned or unassigned when customers take significant actions or reach specific milestones. They are used for compound attributes that represent a combination of conditions or behaviors and only assigned when the specified conditions are met.

Badges are treated specially in the UI, appearing with their custom icons in the **Badge Activity** window of the AudienceStream **Dashboard**, the **Visitor Profile** sampler, and **Audience Discovery**.

Examples of badges include:

  * `VIP`: A VIP is a high-valued customer who keeps returning to the site and purchasing.
  * `Cart Abandoner`: A cart abandoner is a visitor who adds products to the shopping cart but doesn’t complete a purchase.
  * `Frequent Business Traveler`: A frequent business traveler is a customer who has traveled more than a certain number of times over a given time period.

For more examples, see .

## Enrichments and logic

Booleans and badges have different sets of enrichments to set a value, as follows:

### Boolean enrichments

* **Set Boolean**: This enrichment sets the boolean attribute to `true` or `false`. For example, to track if a visitor has verified their email address, you can initialize the attribute by setting it to `false`, then set it to `true` whenever the `user_login` event occurs.

There is no enrichment to clear a boolean value. Typically, visitor booleans are permanent values that rarely change.

### Badge enrichments

* **Assign Badge**: This enrichment assigns a badge to a visitor when a set of conditions are met. For example, the `Window Shopper` badge is assigned when a visitor frequently browses the site without making a purchase.
* **Remove Badge**: This enrichment removes a badge when the visitor no longer satisfies the conditions. For example, the `Window Shopper` badge is removed after the visitor makes a purchase.
* **Assign Badge from Another Badge**: This enrichment assigns a badge based on the presence of another badge. For example, earning a `Sports car fan` badge could trigger the assignment of a related badges such as `Car fan`. For more information, see .

## Data representation

Visitor booleans and badges are represented in the platform in the following ways:

### Booleans

Booleans are stored in visitor data records under the data object `flags` as key-value pairs where the key is either the UID or name of the boolean attribute:

```json
{
    ...
    &#34;flags&#34;: {
        &#34;5052&#34;: false
    },
    ...
}
```

In AudienceDB, the column heading depends on the file type (table, view, or normalized):

* Visitor Table: `flag_5052`
* Visitor View: `visitor - flag - is_verified (5052)`
* Visitor Normalized: `visitor - flag - is_verified`

The value in the column is either `t` or `f`.

### Badges

Badges are only available in the visitor scope.

Badges are stored in visitor data records as an array of the badge UIDs or as an array of the badge names:

```json
{
    ...
    &#34;badges&#34;: [&#34;13&#34;,&#34;26&#34;,&#34;52&#34;],
    ...
}
```

In AudienceDB, the column heading depends on the type of database table (table, view, or normalized):

* Table: `badge_13`
* View: `visitor - badge - VIP (13)`
* Normalized: `visitor - badge - VIP`

The value in the column will be `t` or `f`, depending on the presence of the badge.

The **Badge Activity** window of the AudienceStream **Dashboard** lists all the badges on the profile that have been removed or assigned to visitor profiles:

![](/images/server-side/badge-activity-view.png)

And in the **Visitor Profile** sampler, each badge appears with a count and percentage of visitors who have obtained that badge since you started monitoring activity:

![](/images/server-side/visitor-profile-sampler-badges-view.jpg)

## Strings as booleans

In most scenarios, booleans or badges are sufficient for tracking states. However, in **rare cases**, you may need to represent an **unassigned** state in addition to `true` and `false`. Using a string lets you track three distinct states instead of just two.  

For example, when storing user consent: 

* `true`: The user has given consent.  
* `false`: The user has refused consent.  
* **Unassigned**: The user has not yet provided an answer.  

This approach is useful when distinguishing between **no response** and an explicit `false` is necessary. 

## Summary comparison

The following table lists the major differences between booleans and badges:

| Feature | Visitor Booleans | Badges |
| --- | --- | ---- |
| Definition  | True/false state or current status.|  Represents complex behaviors. | 
| Usage | Single conditions. | Complex behaviors/milestones. | 
| Storage | Key-value pairs (true/false) | Array of badge names or badge UIDs. | 
| Changeability  | Explicitly updated. |   Added/removed by conditions. | 
| Enrichments |  Set Boolean.  | Assign, Remove, and Assign from Another Badge. | 

## Related

* 
* 
* 
