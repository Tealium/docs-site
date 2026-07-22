---
title: Content Modification Extension
description: This article is about the Content Modification extension and how to configure it. Use the Content Modification extension to change the content of an HTML element. This is used to show A/B content based on a condition.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/content-modification-extension/
---
## Prerequisites

* Before you start, see [About Extensions]().

## How it works

The Content Modification extension adds new content, or changes the existing content of an HTML element. For example, if you needed to update your website by adding an advertisement banner, use the Content Modification extension to add the new banner at a specified location on your site.

This extension works by identifying a target element in the page, selecting the position of the new element, the new HTML element to insert, and the content will be modified based on any conditions set (if any).

The target element can be selected either by [DOM ID]() or [XPath](). Use [Tealium Web Companion]() to find the respective identifer value of the target element by using the **On-Page Selecter Element** tool.

The new content is inserted based on its relative position to the target element. There are several options:

* **Before Node**: The new content is applied before the specified element.
* **After Node**: The new content is applied after the specified element.
* **Beginning of Node**: The new content is inserted at the beginning of the specified element.
* **End of Node**: The new content is inserted at the end of the specified element.
* **Replace Node Content**: The new content replaces the specified element's content.
* **Replace Node**: The new content replaces the specified element completely.

In the **Content** text area, copy and paste the standard HTML code of the new content. Do not use single quotes. We recommend you provide an ID, otherwise the new content is inserted without an ID. For example: `<div id="myNewId">My New Content</div>`

Set the **Condition** to control when the extension executes. For example, to control the display of an advertisement banner when the visitor is on the shopping cart page and also belongs to a specific test group.

Use this approach to compare the performance of an A/B test by duplicating the extension with slightly different content and conditions for each test group. Then use Google Analytics to analyze the impact of the A/B test on each test group.

Learn more about [A/B Testing using the Content Modification extension](https://education.tealium.com/learner/courseinfo/id:375) (requires a Tealium Education account).

## Using the extension

Once the extension is added, the following configuration options are available:

* **Element Type**: The type of element to be modified
    * **DOM ID**: (default) The unique ID value of the selected element in the HTML document.
    * **XPath**: The location pathname of the selected element in relation to the root element or root node.
* **Identifier**: The DOM ID or XPath value of the targeted content to be modified.  
  Example ID: `myDomId`  
  Example xpath: `/html/body/div/examplecontent`
* **Position**: Select the position of the new content, relative to the target node.  
The following positions are available:
    * Before Node
    * After Node
    * Beginning of Node
    * End of Node
    * Replace Node Content
    * Replace Node
* **Content**: Enter the new content in standard HTML format. Do not use single quotes.
* To add a condition, click the **Add Condition** button. Conditions allow you to determine when to perform the content modification.
    * Click the **+** button inside the Condition box to add another AND condition.
    * To add an OR condition, click the **+** button outside the Condition box.

### Scoping to footer (deprecated)

The footer scope functionality is deprecated. Older extensions scoped to footer still function properly, but the footer scope is no longer available as a selection. Scoping the Content Modifcation extension to footer required inserting another script within the footer tags or at the bottom of the body tag on your page. The following is an example of the script in a page's code:

```html
     <script type="text/javascript" src="//tags.tiqcdn.com/utag/account/profile/environment/utag.footer.js"></script>
     </body>
</html>

```

### Node positions

The following is an in-depth look at node position. The example is based on a web page that contains the following target element in the source:

```html
<div id="myDomId">Target Node</div>
```

Since the target element has an `id` attribute, this example will use the **DOM ID** option for **Element Type**.

![](https://docs.tealium.com/images/iq-tag-management/iq-extension-content-modification.png)

To provide additional technical detail about the JavaScript that executes as a result of this extension, the following statements are assumed:

* `d = document.getElementById('myDomId');`
* `n = document.createElement('div');`
* `n.innerHTML = 'My New Content';`

This table shows the effect of each node position option in relation to the target element:

| **Node Postion**     | **Result After Insertion** | **Code Applied**  |
| -------------------- | -------------------------- | ----------------- |
| Before Node          | ``` <div>My New Content</div> <div id="myDomId">Target Node</div> ```       | `d.parentElement.insertBefore(n, d)`              |
| After Node           | ``` <div id="myDomId">Target Node</div> <div>My New Content</div> ```       | `d.parentElement.insertBefore(n, d.nextSibling);` |
| Beginning of Node    | ``` <div id="myDomId">   <div>My New Content</div>   Target Node </div> ``` | `d.insertBefore(n, d.firstChild);`                |
| End of Node          | ``` <div id="myDomId">   Target Node   <div>My New Content</div> </div> ``` | `d.appendChild(n);`                               |
| Replace Node Content | ``` <div id="myDomId">My New Content</div> ```                       | `d.innerHTML='My New Content';` |


Learn more about the JavaScript methods used by the Content Modification extension:

* [insertBefore](http://www.w3schools.com/jsref/met_node_insertbefore.asp)
* [appendChild](http://www.w3schools.com/jsref/met_node_appendchild.asp) 
* [nextSibling](http://www.w3schools.com/jsref/prop_node_nextsibling.asp) 
* [firstChild](http://www.w3schools.com/jsref/prop_node_firstchild.asp) 
* [innerHTML](http://www.w3schools.com/jsref/prop_html_innerhtml.asp) 

## FAQ

#### Can you use a jQuery selector or does it have to be an ID of an element?

The Content Modification extension does not use jQuery, it uses native JavaScript functions to get the target node, either by DOM ID or Xpath. However, if you have jQuery on your site and want to take advantage of its advanced selector capabilities, you can use it to add a DOM ID to your target element. To do this, use a JavaScript Code extension scoped to Pre Loader to add the `id` attribute to your target element. This lets you use that DOM ID in the Content Modification extension.

Example JavaScript Code extension:

```js
jQuery(".my-custom-selector").get(0).setAttribute("id", "myDomId");
```
