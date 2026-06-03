---
title: About Audience Discovery
description: This article describes the features of Audience Discovery.
url: https://docs.tealium.com/server-side/audiences/audience-discovery/about/
---
Audience Discovery simplifies the task of identifying valuable segments of visitors for your business case. By using graphical visualizations of visitor data, you can quickly validate details about your site visitors and their browsing behavior with each site visit. Exploring and analyzing segments of visitor profiles through the lens of your attributes can help guide you to more accurate information about your visitors, fueling your campaign strategies.

Using **Audience Discovery**, you can quickly and easily:

* Discover insights about audiences that meet your defined criteria.
* View a visual representation of your customer data through the lens of visitor and visit attributes.
* Filter a selected audience on-the-fly to refine your target visitor segment.
* Overlay important metrics to compare data points.
* View your audiences from a variety of perspectives.

For information about creating audiences, see [Create an audience]().

## How it works

Audience Discovery uses your data and adapts to your custom-defined visitor schema to display historic (end-of-session) unified real-time data or in-session real-time charts of the visit and visitor attributes you define, as you define them.

### Attributes, audiences, and perspectives

To filter your data for use with Audience Discovery, it is important to understand the differences between data attributes, audiences, and perspectives.

* **[Attributes]()**  
In Audience Discovery, attributes are used to define the data in your data layer that is associated with the properties of a visitor, the characteristics of a visitor session, and event data collected during the visitor session.  
For example, a visitor attribute contains event data specific to the visitor, such as the email address or member ID for the visitor. A visit attribute contains event data specific to the site visit, such as a product category viewed or the date of the last visit.
* **[Audiences]()**  
An audience is a group of visitors that are identified by a shared set of attributes. Attributes assigned to an audience are used to identify distinct groups of visitors to your site. The more attributes you select for an audience, the more specific your audience becomes. Audiences are used to trigger connector actions. After an audience is created, that audience can be targeted with an email campaign, coupon, or other action.  
* **Perspectives**  
Perspectives are specific views of your audiences in Audience Discovery. For example, selecting the **Badge** perspective lets you view visitors from the perspective of the badges they are assigned, such as **Frequent Visitor**.

### Daily visitor query cap

The daily visitor query cap determines the sample size of visitors used to project results in Audience Sizing and Audience Discovery queries. The actual query runs on the total visitors matched, not just the capped visitors. 

The **Sample Size of Daily Visitors to Process** profile setting can only be modified by Tealium. To adjust this setting, contact your account representative.

![](/images/server-side/daily-visitor-query-cap-setting.jpg)

## Audience Discovery visualizations

Audience Discovery is a real-time visual representation of attributes that provides insights into the behavior of your visitors. A live sampling of data displays visitors and attributes that meet your search criteria.

Use the following interactive tools to define and filter your search. The presentation of matching visitors can help guide you to narrow or broaden your query to reach the visitor segment you want and create highly defined, targetable audiences.

![](/images/server-side/audience-discovery-ui-features.png)

|Image Label| Description|
|---| ---|
| 1 - Select an audience | Select an audience from the drop-down list and load that audience. The number of active queries per profile is limited to five. |
|2 - Current View| Click to view **Live** activity or **Historic** activity. |
| 3 - Select Perspectives | Click to search or select from all, **Visit**, or **Visitor-scoped** perspectives.|
| 4 - Hover to highlight perspective | Hover over any bar in the chart to highlight details about that perspective.|
| 5 - Explore the details of a perspective | Click a perspective to see additional details. &lt;ul&gt;&lt;li&gt;**Zoom In** provides a more detailed breakdown of the perspective. You can continue to explore additional layers by zooming into the results until exhausted.&lt;/li&gt;&lt;li&gt;**Cross Tab Report** provides a detailed breakdown of the perspective in the same bar chart format.&lt;/li&gt;&lt;li&gt;**View Attribute Definition** displays the attribute definition or definitions used to create the results displayed. Double-click the attribute to display the edit screen to edit the attribute on-the-fly or delete the attribute.&lt;/li&gt;&lt;/ul&gt; |
| 6 - View, edit, or add favorite numbers| Favorite numbers allow you to select specific metrics to display along the bottom of the screen. Only numeric values are allowed. From here, you can: &lt;ul&gt;&lt;li&gt;Click a **Favorite Number** that is already defined to view the properties.&lt;/li&gt;&lt;li&gt;Add a new favorite number and define the properties to display.&lt;/li&gt;&lt;li&gt;Delete an existing favorite number.&lt;/li&gt;&lt;li&gt;Pin (overlay) favorite number results on the primary graph.&lt;/li&gt;&lt;li&gt;For more information, see [Favorite numbers]().&lt;/li&gt;&lt;/ul&gt; |

## Test visitor stitching configurations

Visitor stitching is a form of identity resolution that works across platforms, devices, and browsers to associate activity to the same visitor. For visitor stitching to work properly, the selected visitor ID attribute must be unique for each visitor. You can use Audience Discovery to validate the uniqueness of visitor IDs before you enable visitor stitching.

Learn more about testing visitor stitching strategies with Audience Discovery in the [Visitor ID Part 1]() tutorial. For instructions on creating a visitor ID attribute, including verification with Audience Discovery, see [Create a visitor ID attribute]().

You can also use Audience Discovery to validate that values are correctly being assigned for badges or attributes with complex enrichments using this method. 
