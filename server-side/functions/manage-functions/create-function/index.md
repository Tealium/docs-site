---
title: Create a function
description: This article provides instructions for creating data transformation functions and event or visitor functions.
url: https://docs.tealium.com/server-side/functions/manage-functions/create-function/
---
## Create a data transformation function

Follow these steps to create a data transformation function:

1. Click **&#43; Add Function**.
1. Enter a name for the function.
1. For the trigger, select **Data Transformation**, then click **Continue**.  
1. Enter a **Trigger Name**.
1. In **Selector**, enter a JSONPath expression (see [JSONPath](https://github.com/json-path/JsonPath)). For example, `$.datasourceId` or `$.data.udo.tealium_event`. The selector is limited to 128 characters.
1. Select an **Operator**, and enter a **Value**.  
The **Value** is limited to 128 characters.
1. Click **&#43; Add Condition** to add an additional `AND` condition.  
A block of `AND` conditions is limited to 10 conditions.
1. Click **&#43; OR** to add a block of `OR` conditions.  
The number of `OR` condition blocks is limited to `10`.
1. Click **Continue**.  
Commented example code is displayed. You can modify this code, or replace it with your own function code.
1. After testing the function, click the **Configuration** tab, change the **Status** to ON, and click **Done**.  
For more information on testing functions, see [Test Functions]().
1. Save and publish.

The function is not saved and cannot be triggered until you save and publish. If you edit a function later on, make sure you save and publish for the changes to take effect.

When you save and publish after creating a data transformation function, it can take up to 300 seconds for the change to take effect.

### Example of conditions for a data transformation function

To run a campaign for users whose purchase is more than $1000 and whose cart includes personal electronics products, the following conditions could be used:


[
  [
    {
      &#34;input&#34;: &#34;$.dataSourceId&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;aq68ur&#34;
    },
    {
      &#34;input&#34;: &#34;$.data.udo.campaign&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;cdfc5a72&#34;
    },
    {
      &#34;input&#34;: &#34;$.data.udo.product[?(@.category == \&#34;Personal Electronics\&#34;)]&#34;,
      &#34;operator&#34;: &#34;is not empty&#34;
    },
    {
      &#34;input&#34;: &#34;$.data.udo.order_total&#34;,
      &#34;operator&#34;: &#34;greater than&#34;,
      &#34;filter&#34;: &#34;1000&#34;
    },
    {
      &#34;input&#34;: &#34;$.data.udo.tealium_event&#34;,
      &#34;operator&#34;: &#34;equals&#34;,
      &#34;filter&#34;: &#34;purchase&#34;
    }
  ] 
]


## Create an event, visitor, or data record function

1. Click **&#43; Add Function**.
1. Enter a name for the function.
1. Select a trigger: **Processed Event**, **Processed Visitor**, or **Processed Data Record**, then click **Continue**.
1. Configure the function, as follows:
    * If you select the **Processed Event** trigger, select an **Event Feed**.
    * If you select the **Processed Visitor** trigger, select an **Audience**.
    * If you select the **Processed Data Record** trigger, select a **Segment**.
1. Click **Continue**.
    * Commented example code is displayed. You can modify this code, or replace it with your own function code.
1. After testing the function, click the **Configuration** tab, change the **Status** to ON, and click **Done**.  
    * For more information on testing functions, see [Test Functions]().
1. Save and publish.

The function is not saved and cannot be triggered until you save and publish. If you edit a function later on, make sure you save and publish for the changes to take effect.
