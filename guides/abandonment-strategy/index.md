---
title: Abandonment strategy
description: This guide explains different types of abandonment, common reasons for it, key metrics to track, and strategies for retargeting abandoners through segmented campaigns.
url: https://docs.tealium.com/guides/abandonment-strategy/
---
## What is abandonment?

Tealium provides powerful capabilities for tracking and responding to customer behavior, allowing you to create personalized experiences and drive conversions. One key use case is tracking and responding to abandonment, a common challenge for e-commerce businesses.

Abandonment refers to a visitor starting but not completing an action, such as leaving items in a shopping cart without making a purchase. Abandonment events are key indicators of lost sales opportunities, making them ideal for retargeting campaigns.

## How it works 

With Tealium, you can activate and enhance retargeting campaigns by collecting data about abandonment activity such as search terms, viewed products, shopping cart  details, known visitor attributes, and session information. Then you can send this visitor data to your retargeting vendor in real-time using server-side connectors.

There are three components to the solution:

1. **Track conversion funnel events**  
Use Tealium EventStream to define the key events across your website, such as searches, product views, cart adds, and checkouts. This data is essential for understanding where visitors drop off and for defining abandonment audiences for retargeting.
1. **Identify visitor segments**  
Use Tealium AudienceStream to segment visitors based on their behaviors, such as product interest or checkout actions, into audiences. Each audience you create is specific to each retargeting campaign and can be activated in real-time.
1. **Activate vendor integrations**  
Connect Tealium to your retargeting vendors and other marketing tools with server-side connectors. These integrations send your abandonment audiences and campaign data to your vendors for real-time retargeting.

## Types of abandonment

There are several types of abandonment you might want to address:

### Cart abandonment

Cart abandonment happens when a visitor adds products to their cart but doesn't complete the purchase. Retargeting these visitors works well because they've already shown interest in your brand and you know which products caught their attention.

Cart abandonment campaigns often generate strong returns because they are timely, relevant, and offer compelling incentives. These campaigns are especially effective for existing customers who are already familiar with your brand, high-intent shoppers who have looked at products repeatedly, and discount shoppers who are looking for a deal.

### Browse abandonment

Browse abandonment happens when a visitor views a product, perhaps multiple times, but does not add the product to their cart. Retargeting these visitors works well because you know the visitor had intent and you know which products caught their attention.

To determine if your site is a good candidate for browse abandonment, consider tracking the ratio of visitors who browse product pages to visitors who add products to their cart. If this ratio is low, it might indicate an issue in your shopping funnel and a browse abandonment campaign could benefit you. 

When tracking the browsing behavior of your visitors, consider the following as you decide what is important to your retargeting campaigns:

* Do you want to track the number of products that the visitor browses or the number of times they visit product categories?
* Do you want to track behavior over a single visit or multiple visits?
* Do you want to track what the visitor purchases so that you only retarget products or categories that they are likely to buy or avoid retargeting products that the visitor has never bought?
* Do you want to track only certain products or categories that you are trying to sell due to excessive inventory or low margins?

### Search abandonment

Search abandonment happens when a visitor enters a search query for an product, brand, or category but does not add a product to the cart. For example, a visitor may search for shirts on an apparel site, but then leave the site with an empty shopping cart. Retargeting these visitors works well because you have clear and explicit intent from the search keywords the visitor entered.

Your site is a good candidate for search abandonment if you observe any of the following:

* Low conversion rate of visitors that use search.
* High bounce rate from the search results page.
* Popular search terms that do not get purchased.
* High search rates with low product view rates.

You can create an audience to identify search abandonment and send relevant information about these visitors to a retargeting vendor.

## Reasons for abandonment

These are a few reasons a visitor to your site would abandon a cart, a search, or a browsing session, and how a retargeting campaign might help:

* **Unexpected costs**  
Hidden fees such as shipping, taxes, or additional charges during checkout can surprise customers and lead to cart abandonment. Discounts and free shipping can be used to address these concerns and offset the additional costs.
* **Distractions or interruptions**  
External factors such as receiving a phone call, losing internet connection, or being interrupted mid-checkout can cause visitors to abandon their carts and leave the website. Retargeting can bring the customer back when the interruptions or disruptions have ended.
* **Lack of payment options**  
Limited payment options or the absence of preferred payment methods can discourage visitors from completing their purchase. Followup messaging can detail all of the payment options provided that would fit their needs.
* **Indecision or window shopping**  
Visitors may add items to their cart without the intention to purchase, using it as a temporary storage while they browse or consider their options. A retargeting campaign can help nudge these visitors into purchasing the items they've stashed in the cart.
* **Shipping and delivery issues**  
Concerns about delivery time, shipping options, or availability to receive the package can lead visitors to abandon their carts, especially if the shipping costs are high or delivery options are limited.

## Metrics to track

By building attributes and using AudienceStream and AudienceDB, the following metrics can help you identify and resolve the reasons your customers are abandoning the shopping process on your site:

* **Cart abandonment rate**  
The percentage of users who add items to their shopping cart but do not complete the checkout process. This metric indicates the overall effectiveness of your checkout process and can help identify potential barriers to conversion.
* **Checkout abandonment steps**  
Analyze the steps users take during the checkout process and identify where they are abandoning their carts most frequently. Metrics such as step-by-step abandonment rates, time spent on each step, and drop-off points can reveal specific areas of friction or confusion.
* **Exit page analysis**  
Identify the pages where users exit the website most frequently without completing any significant actions. Pages with high exit rates may indicate issues with content, navigation, or user experience.
* **Search abandonment rate**  
Measure the percentage of users who conduct a search on the website but do not click on any search results or refine their query. High search abandonment rates may indicate relevance issues, poor search functionality, or lack of relevant content. Testing your site search engine regularly and ensuring that each product and category are properly tagged can help reduce search issues.
* **Session duration**  
Analyze the average duration of user sessions on the website. Short session duration may suggest that users are not finding what they are looking for or encountering usability issues that lead to abandonment.
* **Device and browser analysis**  
Analyze user behavior and abandonment rates across different devices and browsers. Variations in abandonment rates between devices or browsers may indicate compatibility issues or usability challenges.
* **User feedback and surveys**  
Collect feedback from users through surveys, feedback forms, or user testing sessions to understand their reasons for abandonment directly. Qualitative insights from users can complement quantitative metrics and provide deeper understanding.


<blockquote>
For some of these metrics, you will need both AudienceStream and AudienceDB activated on your account. Also, you will need to add visit and visitor attributes, and then create audiences based on those attributes.
</blockquote>


These additional metrics, beyond the scope of Tealium, can also help to measure the effectiveness of your site:

* **Bounce rate**  
The percentage of users who land on a page and then leave the website without interacting with any other pages. High bounce rates may indicate that visitors are not finding the information or products they expect, leading to abandonment. Bounce rate measurement is typically available from your main analytics provider.
* **Page load times**  
Monitor the loading times of key pages and elements on the website, such as product pages, checkout pages, and search results. Slow loading times can frustrate users and contribute to abandonment. This metric requires configuration of Tealium iQ Tag Management on the client-side.
* **Error rates**  
Track the occurrence of errors or technical issues encountered by users during their browsing or checkout process. Common errors such as 404 pages, payment processing errors, or form validation issues can lead to abandonment. This metric requires configuration of Tealium iQ Tag Management on the client-side.
* **Scroll tracking**  
Track where viewers engage or abandon your site, or if they read through your site at all. Scroll tracking can help you find the optimal location for calls-to-action (CTA), more engaging content, or modular content sections to allow for easier consumption. This metric requires configuration on the client-side through Tealium iQ Tag Management event listeners.

## Retarget abandoners

There are many ways you can use Tealium to engage and convert abandoners:

* **Personalized email**  
Create an email template at an email service provider vendor and then send a personalized email to the abandoner with their name, the item or items they left behind on your site, and any deals or discounts you want to use to entice them back for a purchase.
* **Limited-time offers**  
Create a sense of urgency by telling the visitor that their cart will expire soon or that those items are in limited supply.
* **Exit Popups**  
As the visitor is leaving the site, send them a popup window that offers a discount or reminds them what they are leaving behind in their cart.
* **Multi-Channel Marketing**  
Use multiple methods of contacting the visitor. Combine email, SMS, push notifications, targeted ads, and other methods so they cannot ignore all of them. You can accomplish this by activating an audience or segment with multiple connectors.
* **Segmentation**  
People abandon their carts, searches, and sites for various reasons. After you have run your visitors through AudienceStream to build up audience numbers and determine that you have an actionable number of abandoners, you can further segment your abandoners based on their behavior patterns to customize the engagement methods to fit their needs.


<blockquote>
If you launch segmentation too early, your audiences and segments may not be large enough for integrated vendors to activate and retarget.
</blockquote>


## Abandoner segments

There are many ways you can use Tealium to further segment your abandoners into specific audiences:

* **How often do they abandon the site?**  
If they abandon the site frequently, ponder offering them a loyalty discount or a reminder service to bring them back to the site. If it's a rare event, a simple reminder email should bring them back.
* **How much did they abandon?**  
If a person is abandoning a cart with high-value items, you will want to spend more effort and attention on that visitor than someone who abandoned a search for an inexpensive low-margin item.
* **When did they abandon the effort?**  
Visitors who abandon a cart right before purchase may need just a little bit of extra effort to get them to convert, while those who abandon the process earlier during a search will need more information or incentive to continue their shopping.
* **What other items have they bought?**  
With the visitor's past purchase history, you can determine their preferences and adjust the messaging to fit their needs. If they bought similar items, offer them related products or other recommendations.

## Next steps

* [cart-abandonment-guide](https://docs.tealium.com/cart-abandonment-guide/)