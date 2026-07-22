---
title: Manage event attributes
description: This article describes how to manage event attributes.
url: https://docs.tealium.com/server-side/attributes/manage-es-attributes/
---
Go to **Govern > Event Attributes** to view your event attributes. Optionally filter your view by clicking on any of the available options on the left side of the table. Click an attribute to view its details.

![](https://docs.tealium.com/images/server-side/ea-filter-es-attributes.png)

## Add an attribute

Use the following steps to add an event attribute:

1. Click **+ Add Attribute**.
1. In the **Add Attribute** dialog, select the attribute type and click **Continue**.
    * **Universal Variable**: This type is used anywhere a custom data point is needed, such as within your data layer or calculated in real time. These are the most common variables.
    * **JavaScript Page Variable**: This type automatically captures the value of a global JavaScript variable from within a browser installation.
    * **HTML Metadata**: This type automatically captures the value of a metadata tag from within a browser installation.
    * **First-Party Cookie**: This type automatically captures the value of a cookie variable from within a browser installation.
    * **Querystring Parameter**: This type automatically captures the value of the current page's URL querystring from within a browser installation.![](https://docs.tealium.com/images/server-side/ea-es-attribute-type.png)
1. Select a data type and click **Continue**. For more about data types, see [data-types](https://docs.tealium.com/data-types/).
1. (Required) In the **Title** field, enter a descriptive name.   
For event attributes, the **Title** can only contain letters, numbers, underscore, dollar sign, square brackets, and period. The name of an event attribute must match the name of the variable implemented. 
      ![](https://docs.tealium.com/images/server-side/ea-form-es-attributes.png)
1. In the **Notes** field, enter helpful notes that describe the purpose and/or mechanics of the attribute.
1. (Optional) Select **Restricted Data** if the visitor data includes PII data..
1. (Optional) Select **EventDB** to send the data to EventDB.
This step requires EventDB to be enabled in the profile.
1. The value for the new attribute should originate from your application, but you can alter the value by adding an attribute enrichment. Click **Continue** to go to the next section and add an enrichment. 

## Duplicate an Attribute

Use the following steps to duplicate an attribute:

1. Click the attribute you want to duplicate and then click the duplicate icon.  
      ![](https://docs.tealium.com/images/server-side/duplicate-es-attribute.png)
1. Edit if needed and then click **Save**.
1. Save and publish your profile to apply the changes.

## Edit an attribute


<blockquote>
Preloaded attributes cannot be modified, but you can duplicate them and modify the copy. The duplicate contains all of the enrichments and rules from the original.
</blockquote>


Use the following steps to edit an attribute:

1. Click the attribute you want to edit and click the pencil icon.  
      ![](https://docs.tealium.com/images/server-side/edit-es-attribute.png)
1. Make your changes and click **Save**.
1. Save and publish your profile to apply the changes.

## Delete an attribute

Use the following steps to delete (or remove) an attribute:

1. Click the attribute you want to delete.
1. Click the delete icon.  
      ![](https://docs.tealium.com/images/server-side/delete-es-attribute.png)  
If the attribute you attempt to delete is currently in use by a rule, an enrichment, or an audience, the following message is displayed:  
      ![](https://docs.tealium.com/images/server-side/attribute-delete-in-use.png)  
To delete the attribute, remove it from the rule, enrichment, or audience and try again.
1. In the **Delete Attribute** dialog, click **Delete** to delete the attribute.
1. Save and publish your profile to apply the changes.