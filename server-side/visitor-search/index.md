---
title: Visitor Search (formerly Visitor lookup tool)
description: This article explains the visitor search tool, which is a graphical interface of the visitor privacy API. A visitor search uses a visitor ID attribute and a search value to locate a visitor record in the system.
url: https://docs.tealium.com/server-side/visitor-search/
---
When a record is located, all the known attributes for that visitor are displayed for review. Visitor records can then be deleted. The interface also offers a REST API screen for demonstrating how the API works.

## Search

To find a visitor record, [visitor stitching]() must be enabled and you need a known value for one of the visitor ID attributes defined in your account.

Use the following steps to perform a visitor search:

1. Go to **Govern &gt; Visitor Search**.
1. Select an attribute from the drop-down list.
1. Enter a known value for the selected attribute.
1. Click **Search**.  
If the visitor record exists, the results appear.

![](/images/server-side/whiteui-audiencestream-visitorlookuptool.png)

### View a visitor record

When a visitor record is located, the information is displayed in two panels: the attribute filter panel on the left and the main JSON object panel.

#### JSON object

The main panel displays the raw JSON object of the visitor record. Each attribute data type is represented as keys in the object. For more information about the fields available in the visitor object, see [Visitor Privacy API objects](/api/v3/visitor-privacy/objects/).

![](/images/server-side/whiteui-audiencestream-visitorlookuptool-jsonoject.png)

#### Attribute filter

The left panel provides an attribute filter to adjust the list of attributes that are displayed. Use the **Filter by** menu to choose between displaying **All Attributes** or **Assigned** attributes. When choosing **Assigned**, only attributes that have an assigned value for the currently located visitor profile appear. Click the heading for each attribute type to expand its list of attributes.

| Filter by All Attributes |  Filter by Assigned Attributes |
|---| ---|
| ![](/images/server-side/whiteui-audiencestream-visitorlookuptool-filter-audience-by-all-attributes.png) | ![](/images/server-side/whiteui-audiencestream-visitorlookuptool-filter-by-assigned-attributes.png)|

### Deleting a visitor

When a visitor record is located, you have the option to delete it. This process may take longer than 24 hours to complete, and the action cannot be undone.

Deleting a visitor record permanently removes its data from all components of the Customer Data Hub.

When you click **Delete Visitor**, a request is logged to our system to delete the visitor record and a transaction ID is returned to log the request. The delete request enters a queue for processing. If you search for the same visitor again and the record is not found, you will know the delete process has completed.

 When a visitor record is deleted, it does not trigger the &#34;Left Audience&#34; action in connectors. Connector actions for audiences are executed only when rules are re-evaluated and a visitor&#39;s status transitions from being included in the audience to being excluded. 

The transaction ID can be used in the [Visitor Privacy API](/api/v3/visitor-privacy/endpoints/) to check the status of the request.

## REST API

The **REST API** tab provides an interface to the [Visitor Privacy API](/api/v3/visitor-privacy/endpoints/). The API calls are pre-formatted for you as examples of how to implement the same functionality in your application. Select the API call you want to make and adjust the placeholder values in the request URL.

Each API call is available in the **Request Types** drop-down list. Select a request type to view the details of that API call.

![](/images/server-side/whiteui-audiencestream-visitorlookuptool-select-rest-api-request-type.png)

