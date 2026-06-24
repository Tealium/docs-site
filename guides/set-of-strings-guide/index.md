---
title: Advanced attributes: Set of strings
description: This guide explains how to use set of strings attributes to track user interactions and deliver personalized experiences.
url: https://docs.tealium.com/guides/set-of-strings-guide/
---
## How it works

The set of strings attribute lets you track, filter, and adjust collections of information in real-time as users engage with your site. This information can be used to create personalized experiences and improve targeting. Whether it’s tracking the top product categories a user browsed, frequently searched destinations, or specific services engaged with, set of strings provides a way to store and process this data dynamically.

## Why use Set of Strings?

Here are a few real-world examples of how this attribute helps businesses across various industries:

* Retail &amp; e-commerce: Track the top product categories a user browsed in their session for personalized email recommendations.
* Travel &amp; hospitality: Identify which destinations a user is most interested in by filtering out frequently searched locations.
* Healthcare: Store the most researched medical conditions by a user to tailor relevant content.
* Automotive: Track car models a visitor viewed and adjust targeted ads accordingly.
* Subscription services: Capture the most engaged subscription plans or services a visitor interacts with to send relevant recommendations.

Set of strings attributes are updated dynamically using enrichments, often in combination with other attributes such as tally, string, or rule-based logic. This ensures that only the most relevant user interactions are captured, stored, and available for analysis.

## Key benefits

* Track unique customer interests, capturing the most important interactions dynamically.
* Retain only significant engagement data such as top product categories viewed.
* Use real-world engagement data to trigger personalized marketing campaigns.
* Update and refine stored values such as removing booked destinations or returned products to keep data fresh and relevant for retargeting and personalization.

## What this guide covers

This guide walks through how to use set of strings to track, filter, and manage visitor interactions for better personalization and retargeting.

We will cover the following use cases:

* Capture the top three destinations searched during a session for personalized recommendations using the **Set to Top Tally Items** enrichment.
* Store only destinations viewed more than five times, focusing on high-interest items for targeted marketing, using the **Set to Tally Items Above Target** Value enrichment.
* Pass set of strings attributes to an email platform using a connector to deliver dynamic, personalized content based on a visitor’s most searched destinations.

## Set to Top Tally Items example

We’ll use the set of strings attribute to capture the top three destinations a visitor searches for during a session. This information can be used to send personalized follow-up emails, optimize travel recommendations, or improve ad targeting.

For example, if a visitor searches for 5 destinations, the **Set to Top Tally Items** enrichment captures and stores only the relevant top three most frequently searched destinations for follow-up marketing efforts.

### Step 1: Create an Increment Tally attribute

Before we can identify the top three most searched destinations, we need to first track how many times a visitor searches for each destination during their session. To track this, create a visit scoped tally attribute named **Countries of Resorts Browsed in Visit** with the following enrichment:

```
For Tally Countries of Resorts Browsed in Visit increment the value based on &#34;country&#34; by 1
WHEN: Any event
Rule &#34;page_type&#34; equals (ignore case) &#34;resort_details&#34;
```

![](/images/guides/set-of-strings-increment-tally-attribute.png)

### Step 2: Create a Set of Strings attribute

Now that we are tracking how many times each destination is searched, we need to extract only the three destinations searched the most.

Create a set of strings attribute to store the top 3 countries for resorts browsed in visit with the following enrichment:

1. Go to **Transform &gt; Visitor / Visit Attributes**.
1. Click **&#43; Add Attribute**.
1. Select **Visit scope** and click **Continue**.
1. Select **Set of Strings** data type.
1. In the **Title**, enter **Top 3 Countries for Resorts Browsed in Visit**.
1. Click **&#43; Add Enrichment**.
1. Select **Set to Top Tally Items**.
1. Configure the following set of strings:
    ```
    Set Top 3 Countries for Resorts Browsed in Visit to top 3 items in &#34;Countries of Resorts Browsed in Visit&#34;
    WHEN: Any event
    ```
1. Click **Finish**.

![](/images/guides/set-of-strings-set-to-top-tally-items.png)

If a visitor searched for the following destinations: 

* Vietnam (1 time)
* Paris (4 times)
* London (3 times)
* Rome (2 times)
* New York (5 times)

The final set of strings stores only the top three destinations:

```
[ &#34;New York&#34;, &#34;Paris&#34;, &#34;London&#34; ]
```

## Set to Tally Items Above Target example

In the following example, we store destinations that a visitor searches for more than five times during a session using the **Set to Tally Items Above Target** enrichment. This helps retarget high-intent visitors with personalized ads, travel recommendations, or follow-up emails featuring deals for their most-searched destinations.

We created a visit tally attribute **Countries of Resorts Browsed in Visit** to track how many times a visitor searches for each destination during their session in [step 1 above](#step-1-create-an-increment-tally-attribute). We’ll use this tally to filter out only the high-interest destinations searched **more than five times**.

To create a **Set of Strings** attribute:

1. Go to **Transform &gt; Visitor / Visit Attributes**.
1. Click **&#43; Add Attribute**.
1. Select **Visit scope** and click **Continue**.
1. Select **Set of Strings** data type.
1. In the **Title**, enter **Countries Seen More Than 5 Times**.
1. Click **&#43; Add Enrichment**.
1. Select **Set to Tally Items Above Target Value**.
1. Configure the following set of strings:
    ```
    Set Countries Seen More Than 5 Times to items in &#34;Countries of Resorts Browsed in Visit&#34; where the value is greater than 5
    WHEN: Any event
    ```
1. Click **Finish**.

![](/images/guides/set-of-strings-set-to-tally-items-above-target.png)

If a visitor searches for the following destinations:

* Paris (6 times)
* London (3 times)
* Rome (7 times)
* Madrid (2 times)
* Berlin (1 time)

The final set of strings stores only the destinations searched more than 5 times:

```
[ &#34;Paris&#34;, &#34;Rome&#34; ]
```

This ensures that retargeting efforts focus only on high-interest destinations, improving ad efficiency, recommendations, and personalized email campaigns.

## Use set of strings in a connector action

You can pass a **set of strings** attribute, such as the **Countries Seen More Than 5 Times** attribute, to an email service provider such as **Iterable** using a connector. This attribute captures destinations that a visitor has searched for more than five times in a session, a strong signal of interest. You can apply the same approach with other supported platforms such as Braze, Adobe Campaign, or Salesforce Marketing Cloud.

To trigger the connector, create an audience that includes visitors whose **Countries Seen More Than 5 Times** attribute is assigned. In the connector action, map the attribute to a template variable, such as `countries_seen_more_than_5_times`. You can then reference this variable in your email content to display a personalized list of destinations. When a visitor joins this audience, the connector action will fire and send the **Countries Seen More Than 5 Times** attribute to your email platform.

For example, If a visitor&#39;s set of strings contains: `[&#34;Paris&#34;, &#34;Rome&#34;]`.

The connector passes this list to your email platform, where it can be used to dynamically populate content such as *“Still dreaming about Paris or Rome? Here are top deals just for you.”*

This ensures high-intent visitors receive targeted offers based on their behavior, increasing the likelihood of engagement and conversion.

## Next Steps

Now that you’ve implemented set of strings attributes for tracking, filtering, and activating visitor interactions, consider these next steps to extend your setup:

* **Audit and monitor usage**  
Use [Trace]() and the [Live visitors]() to verify how attributes are populated and used across sessions.
* **Expand to new channels**  
Use your set of strings attributes in other connectors, such as SMS, display ads, or push notifications, to create cohesive cross-channel experiences.

* **Add exclusions and cleanup logic**  
Refine your data by removing irrelevant values (such as booked destinations or expired products) using enrichments like **Remove From Set of Strings**.

* **Combine with other attribute types**  
Pair set of strings with badges, numbers, or booleans to create advanced audience logic and time-sensitive campaigns.

* **Use in real-time personalization**  
Use set of strings in Functions or pass them through EventStream to enrich event data and trigger real-time personalization on your website, mobile app, or other channels.

## Additional Resources

* [Set of Strings Attribute]()
* [Enrichment Usage Examples]()
