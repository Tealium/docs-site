---
title: Hosted Data Layer Extension
description: The Hosted Data Layer extension is a component of the hosted data layer feature. The extension is used to configure which variables from the on-page data layer are used to fetch hosted data layer objects.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/hosted-data-layer-extension/
---
## Prerequisites

* [About Extensions]()
* [About Hosted Data Layer]()

## Requirements

* Version 4.43, or greater, of the Universal Tag (`utag.js`) is required. For more information, see [Upgrade to the latest utag.js.]()
* Lookup variables - Lookup variables are the link between the on-page data layer and the hosted data layer objects that contain supplemental data.   
The values of the lookup variables become the names of the hosted data layer objects.

## How it works

This section describes how the hosted data layer extension works as `utag.js` loads on a page:

1. The hosted data layer extension executes early and halts` utag.js` for a duration up to the specified value in the timeout setting.  
While paused, `utag.js` does not evaluate tags, load rules, or extensions.
1. Then the hosted data layer extension scans the on-page data layer (`utag_data`) for the specified lookup variables.
1. If the lookup variable exists, the extension queries Tealium&#39;s servers for the matching hosted data layer object with the same name as the lookup value.
1. If the `.js` file exists on the Tealium&#39;s servers, the extension fetches the `.js` file.  
The lookup is deemed successful.
1. If a hosted data layer object is found on Tealium&#39;s servers, the extension merges that data into the on-page data layer.  
Duplicate variables are handled according to the following setting of the **Overwrite on merge** setting:
    * **Overwrite on merge: Yes**: Variables in the on-page data layer are overwritten by variables from the incoming object.
    * **Overwrite on merge: No**: Variables in the on-page data layer are preserved.
1. `utag.js` continues operation when merging is complete or the timeout has expired, whichever occurs first.
1. Load rules and extensions are evaluated and tags are fired accordingly.

## Configuration

Use the following steps to configure the extension:

1. Go to the **Extensions Marketplace** and add the Hosted Data Layer extension from the **Standard** tab.  
For detailed instructions, see [How to add an Extension]().
1. In the **Title** field, enter a descriptive title.
1. The **Scope and Execution** field is set by default to ensure that the extension can run for all tags prior to the evaluation of the load rules.
1. Click **&#43;Add Variable**.
1. Select the appropriate variable from the drop-down list.
1. Repeat these steps for each addition until complete. 
    The extension performs the lookup in a sequential order. In the following example configuration, `page_name` is looked up first, followed by the `product_sku` then `customer_zip`. 
    ![](/images/iq-tag-management/configuration.png)
1. The **Overwrite on Merge** setting defaults to **Yes**. If a key exists both in the incoming and recipient data layers, the incoming key-value overwrites the existing instance by default. If you prefer to preserve the existing key-value instance, toggle this setting to **NO**.
1. The default **Timeout** (seconds) setting is 30 seconds. You may change this setting depending on the time estimated to complete the merge.
1. When complete, click **Save &amp; Publish** to save and publish the profile.

## FAQ

#### What happens if the hosted hosted data layer object is not found?

The lookup can fail for two reasons: either the name of the hosted data layer object is defined incorrectly or it is not defined at all. Regardless of the reason, the extension receives an empty object and there is no enrichment.

Ensure that the value of the lookup variable in the on-page data layer matches the name of the hosted data layer object uploaded to Tealium. Use the hosted data layer API to verify that the expected hosted data layer objects are uploaded to Tealium.

#### What happens if the lookup variable is not in the on-page data layer?

The extension releases the halt on `utag.js` and it runs as usual. There is no lookup and the on-page data layer remains unchanged.

The following example shows how the data layer looks before and after merging:

| Original Data  | Incoming Variables  |
|:---------------|:--------------------|
| `{ &#34;product_category&#34; : &#34;shoes&#34;     &#34;product_sku&#34;      : &#34;GEN-PRD-BLU&#34; }` | `{     &#34;product_category&#34;   : &#34;boots&#34;     &#34;has_instore_pickup&#34; : &#34;1&#34; } ` |

| After Merging: Overwrite YES| After Merging: Overwrite NO|
|:-----------------------------|:--------------------------|
| `{    &#34;product_category&#34;   : &#34;boots&#34;    &#34;product_sku&#34;        : &#34;GEN-PRD-BLU&#34;    &#34;has_instore_pickup&#34; : &#34;1&#34;  } ` | `{     &#34;product_category&#34;   : &#34;shoes&#34;     &#34;product_sku&#34;        : &#34;GEN-PRD-BLU&#34;     &#34;has_instore_pickup&#34; : &#34;1&#34;    }` |

#### Can I use this extension without the API component?

No. You must upload data layer objects prior to using this extension.

#### Can I change the scope of the extension?

No. The scope and the execution drop-down list is predefined to ensure that the extension can automatically run before all load rules and tags are processed.

#### Does this extension affect page loading?

Running this extension introduces a slight slow down in tag firing since the hosted data layer objects must be returned before the operation can complete.

#### Is it possible to chain together lookup variables (for example, use a variable from a hosted data layer object as a lookup variable)

No. The lookup variables must exist in the on-page data layer at the start of the extensions. They cannot be populated by a previous lookup variable (hosted data layer object).

#### Does enrichment work with event tracking or subsequent calls to utag.view, utag.link, or in a single-page application environment?

No. The extension is designed to run once per page load.

#### Can this extension be used in mobile installations?

Yes. To learn about the Hosted Data Layer feature for mobile, see [Hosted Data Layer](/platforms/getting-started-mobile/hosted-data-layer/).

#### What happens if the extension fails to find the target data layer object?

The extension receives an empty object and `utag.js` automatically resumes. No merging occurs.

#### What version of utag.js is required for this feature?

You must use version 4.43, or greater. The hosted data layer extension is optimized for the most recent version of `utag.js`.
