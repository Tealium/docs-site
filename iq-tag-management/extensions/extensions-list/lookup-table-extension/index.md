---
title: Lookup Table Extension
description: This article is about the Lookup Table extension and how to configure it. The Lookup Table extension is used to map the value from one data layer variable to set the value in another variable.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/lookup-table-extension/
---
## Prerequisites

* Universal Tag (`utag.js`) 4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).

## How it works

The Lookup Table extension provides a way to set the value of one data layer variable based on the value of another variable using a list of lookup values. For example, if you need to set category names but the data layer only provides values for category IDs, the Lookup Table extension provides a mapping of category ID to category name. A sample mapping could be category ID `35` mapped to category name `iQ Tag Management` and category ID `38` mapped to category name `Mobile`.

When configuring the Lookup Table extension, set the **Lookup Value In** field to the lookup variable, which is the source variable from the data layer. Then set the **Destination** field to the variable you want to set based on the lookup entry.

The **Variable Type** field specifies the data type of the lookup variable (`String` or `Array`). The lookup variable is compared to the lookup match values based on the **Match Type**. The match type may be set to **Exact** to use an exact, case-sensitive comparison, set to **Contains** to use a substring [contiguous sequence of characters within a string] comparison, or set to a [regular expression](http://w3schools.com/js/js_regexp.asp) pattern (for advanced users).

The lookup table is configured by adding lookup values and output values entries in the **Lookup Match** field and the **Output** field.  From the example above, the lookup value `35` would appear in the **Lookup Match** field, and the output value `iQ Tag Management` would appear in the **Output** field.

If the value of the lookup variable matches an entry, then the **Destination** variable is set to the **Output** value.

If the value of the lookup variable does not match an entry, then the output value is set according to the default value specified by the **Default Output** field. For example, if this is set to `Unknown`, then when no match is found for the lookup variable, the output variable is set to `Unknown` in the data layer.

Additional conditions may be applied to the extension by modifying the **Conditions** setting.

## Using the extension

Before you begin, familiarize yourself with [how extensions work]().

To use the Lookup Table extension, set up the following configurations:

* **Lookup Value in**: Select the source lookup variable from the data layer that contains the value you want to look up.
* **Destination**: Select the variable to set to the associated output value. Click the **&#43;** button to create new variable.
* **Variable Type**: Select the data type (string or array) of the lookup variable&#39;s value. If you select array, any output goes into the same array index as its corresponding lookup match.
* **Match Type**: All lookups are done using the selected match type.
    * **Exact**: Matches the value of the lookup variable exactly (case sensitive).
    * **Contains**: Matches a substring (a contiguous sequence of characters within a string) value of the lookup variable.
    * **RegExp**: Matches regular expressions to the value of the lookup variable. Escape characters are escaped with two backslashes `\\`. The ignore case flag, `i`, is automatically applied.

* **Lookup Match**: Enter the value of the lookup variable. Do not use quotation marks in the value.
* **Output**: Enter the value to be set for the destination variable when a lookup match is found. Do not enter quotation marks in the value.
* **Note**: (Optional) Add notes related to each lookup match and output value. The content of the note is not passed to the destination.
* **Default Output**: Enter the default value for the destination variable, for the case where the lookup match is not found. Select the **Disable Default** checkbox to disable the default value.

### Import from CSV

Manually entering the mapping data between the lookup variable values and the output values is time-consuming if there are many lookup values. Another option is the **Import from CVS** feature, which lets you paste or enter data formatted as comma-separated values (CSV) in a text area box. The data is entered in the following format, where each value is separated by a comma:

```
Lookup Value, Output Value, Note
```

The `Note` value is optional and may be left blank.

The following example adds 5 lookup/output values pairs to the mapping:

```
38, Mobile, forums
35, iQ Tag Management, forums
46, AudienceStream, forums
34, DataAccess, forums
48, Digital Strategy, forums
```

When you have completed entering the mappings for the lookup table, click the **Replace** button to replace all existing mappings with the new ones from the **CVS** text area, or click **Append** to add these new mappings and keep all original mappings in the lookup table.

### Export to CSV

The **Export to CVS** button exports the lookup table mapping data to a file called `lookup.csv`. The file is automatically downloaded to your computer, and may be opened with either Excel or any text editor software.

The lookup table mapping data is exported as comma-separated values (CSV), where each row is one entry in the format:

```
Lookup Value, Output Value, Note
```

At least one mapping row must be present to perform a successful export. If the optional **Note** field is blank, then only the **Lookup Value** , and **Output Value** appears for that row. If all the fields are blank, data is not exported. The following example shows the contents of the `lookup.csv` file, when exporting the mapping from the Import to CVS example shown above:

```
38, Mobile, forums
35, iQ Tag Management, forums
46, AudienceStream, forums
34, DataAccess, forums
48, Digital Strategy, forums
```

## Example: Mapping category IDs to names

The Lookup Table extension lets you match a data layer variable such as `category_id` to another variable such as `category_name`, as shown in the following example:

1. Select the lookup variable `category_id` from the **Lookup Value in** drop-down menu.
1. Select the readable value variable `category_name` from the **Destination** drop-down menu. If the variable is not found in the drop-down menu, click **&#43;** to add the variable.
1. In the **Default Output** field, enter `none`. The value of `category_name` is set to `none` when the `category_id` value is not found on the lookup table mapping.
1. Select **String** for **Variable Type**, since the variable `category_id` contains only one ID per category.
1. Select **Exact** for **Match Type** if you know the exact category IDs.
1. Repeat the following steps to create a lookup/output value mapping for each lookup variable, mapping each category ID to a readable category name value:
    1. Enter a category ID in the **Lookup Match** field, such as `38`.
    1. Enter a category name in the **Output** field, such as `Mobile`.
    1. (Optional) Add relevant notes in the **Note** field.
    1. Click the **&#43;** button to add another lookup/output value.

![](/images/iq-tag-management/screen-shot-2020-03-12-at-10.23.12-am.png)

When the Lookup Table extension runs, if one of the lookups matches the output value of the `category_id` variable, then the `category_name` variable is populated with the value set in the Output. For example, if `category_id` is `46`, then `category_name` is set to `AudienceStream`.

## FAQ

#### What happens if the lookup variable matches multiple values in the table?

A: Lookups are performed in the order they appear in the extension and the first match wins.

#### Is the match type &#34;Exact&#34; case sensitive?

A: Yes. The `Exact` match option is case sensitive.
