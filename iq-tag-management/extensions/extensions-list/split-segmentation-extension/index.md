---
title: Split Segmentation Extension
description: Use the Split Segmentation extension to randomly assign your visitors into segments. This can be used for A/B testing or sampling.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/split-segmentation-extension/
---
## Prerequisites

* utag v4.38 or later. For more information, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
* See [About Extensions]().

## How it works

The Split Segmentation extension randomly assign your visitors into segments by setting a cookie value based on a distribution. The cookie values can then be used in load rules or other extension conditions to create personalized experiences. You can also pass the segment names to a vendor tag to measure campaign effectiveness or A/B test results.

Each segment is defined by a name and a distribution. The total sum of the groups must equal 100%.

* **A control segment and a small test segment**:  
Segment Label: Control Group (90%)  
Segment Label: Test Group (10%)
* **A 50/50 split segment**:  
Segment Label: Group A (50%)  
Segment Label: Group B (50%)

## Using the extension

Before you begin, familiarize yourself with [how extensions work]().

Once the extension is added, the following configuration options are available:

* **Destination Cookie**: Select the cookie variable to receive the output. If the cookie variable doesn&#39;t exist yet, create it by clicking the **&#43;** button to the right.
* **Cookie domain**: Leave this field blank to auto-detect the domain.
* **Duration**: Select the duration from the drop-down menu.
    * **Session**: The segment cookie lasts until the current session expires.
    * **Visitor**: The expiry of the cookie depends on whether or not it is placed in the `utag_main` cookie. The Split Segmentation cookie values not in the `utag_main` cookie have an expiry of 2099. Cookie values placed in the `utag_main` share its expiry. So, for `utag.js` versions 4.27 and later, that expiry is 1 year. For versions before 4.27, the expiry is 2099.
* **Segment Label**: Enter a label and select the percentage of visitors that are to be placed in that segment.
    * Click the **&#43;** button to add a segment, and the **-** button to remove one. Regardless of the number of segments you add, the sum total must be equal to 100%.

## Example

This example creates three groups to segment the users. To differentiate the groups, a variable called `_group` is created to contain a value that is unique to each group. Different analytics tags are run depending on the group.

1. Set the scope to Pre Loader.
1. Add a new cookie variable by clicking the **&#43;** button next to the **Destination Cookie** drop-down list.  
Enter `_group` for the variable name, and `Split segmentation cookie` for the **Description**.
1. Click **Apply** and the new variable is now selected.  
    ![](/images/iq-tag-management/no-title-560i505e1db17cc44218.png)
1. Leave the **Cookie Domain** field blank as we are using the default domain.
1. Set the **Duration** to **Visitor**.
1. Create three groups and label them `Group A`, `Group B`, and `Group C`.  
Click the **&#43;** button to add the additional groups. The label for each group is stored in the `_group` variable.
1. Divide the visitors equally among these groups, so select 33% for each, except for Group B, which we select 34% so that the total sum equals 100%.  
    ![](/images/iq-tag-management/no-title-561ibcf8c96a47cdf8ff.png)

### Configuring load rules

In this scenario, we want to run a different analytics tag for each group. For Group A, we want to run Google Analytics. For Group B, we want to run SiteCatalyst. For Group C, we want to run IBM Digital Analytics. To do this, we must create a load rule for each of the three situations.

The first load rule states if either the domain or `page_name` value contains `tealium` and the cookie value `_group` equals (ignoring case) `Group A`, then this load rule applies.


[
  [
    {
      &#34;input&#34;: &#34;domain (dom)&#34;,
      &#34;operator&#34;: &#34;contains&#34;,
      &#34;filter&#34;: &#34;tealium&#34;
    },
    {
      &#34;input&#34;: &#34;_group (cp)&#34;,
      &#34;operator&#34;: &#34;equals (ignore case)&#34;,
      &#34;filter&#34;: &#34;Group A&#34;
    }
  ],
  [
    {
      &#34;input&#34;: &#34;page_name (js)&#34;,
      &#34;operator&#34;: &#34;contains&#34;,
      &#34;filter&#34;: &#34;tealium&#34;
    },
    {
      &#34;input&#34;: &#34;_group (cp)&#34;,
      &#34;operator&#34;: &#34;equals (ignore case)&#34;,
      &#34;filter&#34;: &#34;Group A&#34;
    }
  ]  
]


The other two load rules follow almost identical logic, except for the value that `_group` contains, which is `Group B` and `Group C`, respectively.


[
  [
    {
      &#34;input&#34;: &#34;domain (dom)&#34;,
      &#34;operator&#34;: &#34;contains&#34;,
      &#34;filter&#34;: &#34;tealium&#34;
    },
    {
      &#34;input&#34;: &#34;_group (cp)&#34;,
      &#34;operator&#34;: &#34;equals (ignore case)&#34;,
      &#34;filter&#34;: &#34;Group B&#34;
    }
  ],
  [
    {
      &#34;input&#34;: &#34;page_name (js)&#34;,
      &#34;operator&#34;: &#34;contains&#34;,
      &#34;filter&#34;: &#34;tealium&#34;
    },
    {
      &#34;input&#34;: &#34;_group (cp)&#34;,
      &#34;operator&#34;: &#34;equals (ignore case)&#34;,
      &#34;filter&#34;: &#34;Group B&#34;
    }
  ]  
]



[
  [
    {
      &#34;input&#34;: &#34;domain (dom)&#34;,
      &#34;operator&#34;: &#34;contains&#34;,
      &#34;filter&#34;: &#34;tealium&#34;
    },
    {
      &#34;input&#34;: &#34;_group (cp)&#34;,
      &#34;operator&#34;: &#34;equals (ignore case)&#34;,
      &#34;filter&#34;: &#34;Group C&#34;
    }
  ],
  [
    {
      &#34;input&#34;: &#34;page_name (js)&#34;,
      &#34;operator&#34;: &#34;contains&#34;,
      &#34;filter&#34;: &#34;tealium&#34;
    },
    {
      &#34;input&#34;: &#34;_group (cp)&#34;,
      &#34;operator&#34;: &#34;equals (ignore case)&#34;,
      &#34;filter&#34;: &#34;Group C&#34;
    }
  ]  
]


To use these load rules, apply them to the appropriate tags. In this example, the Group A load rule applies to Google Analytics, the Group B Load Rule applies to SiteCatalyst, and the Group C load rule applies to IBM Digital Analytics.

![](/images/iq-tag-management/no-title-565i08f4725670c58bec.png)

When visitors in Group A come to the page, Google Analytics runs. When visitors in Group B come to the page, SiteCatalyst runs. When visitors in Group C come to the page, IBM Digital Analytics runs.
