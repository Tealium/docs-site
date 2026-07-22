---
title: Join Data Values Extension
description: The Join Data Values extension combines multiple text values into a single text value using a separator character called a delimiter.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/join-data-values-extension/
---
## Prerequisites

* [How Extensions Work]()

## How it works

The Join Data Values extension combines two or more text values into a single text value using an optional delimiter. The delimiter is a single character such as `/`, `-`, or `:` that will separate each joined value in the final value. A default value can be set to be used in place of any variable that does not have a value when the extension runs. The joined value can come from either the data layer or a text value you enter. This extension supports conditions.

This extension uses the JavaScript `join()` method to concatenated multiple variables with the delimiter character.


<blockquote>
Avoid delimiter characters that could also appear in the joined values.
</blockquote>


## Using the extension

Once the extension is added, the following configuration options are available:

* **Destination**: The variable to store the joined values.  
Choose an existing variable from the drop-down list or create a new one by clicking the **+** button.
* **Delimiter**: The character to separate each variable in the final text value.  
Enter a single character, such as `/`, `-`, or `:`.
* **Leading Delimiter**: (Default: **No**). Determines if the delimiter will also be applied at the beginning of the joined values.
* **Default Value**: The default value to use in place of a joined variable that does not contain a value. For example, `unset` or `blank`.
* **Join**: The list of variables to join into a single value.  
    * Click the **+** button to add another variable.  
    * Click the **-** button to remove a variable.  
    
<blockquote>
Select the option **Text Value** to enter a custom text value.
</blockquote>

* **Sample**: A sample value to validate the correct delimiter and variables.
* **Condition**: Click **Add Condition** to set a condition to determine when this extension will run.

## Examples

### Dates

Join separate date variables to create a standard date string. Use a different delimiter or order of variables to create the date format you want.

* **Input Variables**:  `year="2020" month="12" day="31"`
* **Delimiter**: `-`
* **Joined Value**:  `date="2020-12-31"`

### Page hierarchy

Create a structured page hierarchy value by combining `site_section`, `page_category`, and other page level variables.

* **Input Variables**:  `site_region="en-us" site_section="Electronics" category_name="Tablets" `
* **Delimiter**: `:`
* **Joined Value**:  `page_hier="en-us:Electronics:Tablets"`
