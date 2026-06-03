---
title: Known visitor badge guide
description: This guide explains how to create and use a badge for known visitors.
url: https://docs.tealium.com/guides/known-visitor-badge/
---
## How it works

![](/images/server-side/badges-known-visitor.png)

The `Known Visitor` badge is assigned when a visitor takes an action that provides a unique and reliable user identifier. Once created, this badge is commonly used to create audience segments to select visitors who can be targeted with a connector.

This approach simplifies audience rule management by centralizing the logic in one configuration. Instead of creating conditions in multiple audiences to check for an email address or other user identifier, you can configure that logic in the badge and reuse it to build audience segments.

Badges can be combined to create more refined audience segments. For example, the following audience contains visitors that have the `Known Visitor` and `Cart Abandoner` badges and have provided an email address. This audience can be used to trigger a connector to send an email to remind visitors about items left in their cart:

![](/images/guides/server-side/known-visitor-purchaser-abandoned.png)

## Benefit

The `Known Visitor` badge enables personalized, direct communication and tailored targeting strategies that are far more effective than the generic approaches available for unknown visitors. This distinction is critical for improving engagement, conversion rates, and customer retention.

## Identifying events

These events provide opportunities to collect reliable identifiers that can be used to assign a badge to known visitors and build audience segments.

* **Order confirmation**: When a visitor completes a purchase.
* **New user sign-up**: When a visitor creates an account and provides their email address.
* **Newsletter sign-up**: When a visitor subscribes to a newsletter, they typically provide an email address, which serves as a unique identifier.
* **Account login**: When a visitor logs into their account, their email address, username, or another unique identifier is often captured.
* **Form submission**: Any form submission, such as a contact form, lead generation form, or survey, can collect identifiers like email addresses or phone numbers.
* **Loyalty program enrollment**: When a visitor signs up for a loyalty or rewards program, they usually provide personal details like an email address or membership ID.
* **Customer support interaction**: During live chat sessions, support tickets, or phone calls, visitor often provide identifiers like email addresses or phone numbers to verify their identity.

For more information about user identifiers, see [User identifiers]().

## Scenarios
 
The following examples highlight audience segments where the `Known Visitor` badge significantly enhances targeting strategies compared to unknown visitors:

### Cart Abandoners

The `Known Visitor` badge enables direct and personalized communication for more effective retargeting of cart abandoners.

![](/images/guides/server-side/known-visitor-cart-abandoner-email.png)

* **Known Visitors**: Visitors who have abandoned their cart and have provided an email address. This segment can be targeted with personalized email reminders about the items left in their cart, potentially including discounts or incentives to complete the purchase.
* **Unknown Visitors**: Visitors who have abandoned their cart but have not provided an email address. This segment can only be retargeted through less personalized methods, such as display ads or on-site reminders.

### Repeat Purchasers

The `Known Visitor` badge allows for tailored loyalty campaigns that build stronger customer relationships.

![](/images/guides/server-side/known-visitor-purchased-email.png)

* **Known Visitors**: Visitors who have made multiple purchases and have an email address or account. This segment can be targeted with loyalty rewards, exclusive offers, or VIP programs.
* **Unknown Visitors**: Visitors who have made multiple purchases but have not provided identifiable information. This segment can only be targeted with general promotions or on-site messaging.

### High-Value Customers

The `Known Visitor` badge enables personalized outreach to high-value customers, increasing retention and lifetime value.

* **Known Visitors**: Visitors with a high lifetime value and an email address. This segment can be targeted with exclusive offers, early access to sales, or premium services.
* **Unknown Visitors**: Visitors with high spend but no identifiable information. This segment can only be targeted with generic promotions.

### Inactive Users

The `Known Visitor` badge allows for direct re-engagement strategies, which are more likely to bring users back.

* **Known Visitors**: Visitors who have not engaged with the site or made a purchase in a specific time frame (such as 90 days) and have an email address. This segment can be targeted with re-engagement campaigns, such as personalized emails offering discounts or reminders.
* **Unknown Visitors**: Visitors who have been inactive but cannot be identified. This segment can only be targeted with general ads or on-site notifications.

### Event Registrants

The `Known Visitor` badge enables personalized follow-ups, increasing event attendance and engagement.

* **Known Visitors**: Visitors who have registered for an event (such as a webinar or product demo) and provided an email address. This segment can be targeted with follow-up emails, reminders, or post-event content.
* **Unknown Visitors**: Visitors who showed interest in the event but did not register or provide identifiable information. This segment can only be targeted with general ads or on-site messaging.

### Content Consumers

The `Known Visitor` badge allows for personalized content recommendations and lead nurturing.

* **Known Visitors**: Visitors who have downloaded gated content (such as whitepapers or eBooks) and provided an email address. This segment can be targeted with nurture campaigns tailored to their interests.
* **Unknown Visitors**: Visitors who consumed content but did not provide identifiable information. This segment can only be targeted with general ads or recommendations.
