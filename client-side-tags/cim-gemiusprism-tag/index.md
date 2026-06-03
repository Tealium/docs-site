---
title: CIM gemiusPrism Tag Setup Guide
description: This article describes how to set up the CIM gemiusPrism tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/cim-gemiusprism-tag/
---
## Tag tips

* lan
  * language of the page must be in all capitals.
  * Pre-defined values are **NL**/**FR**/**EN**/**GE**/**LU**//**OTHER**
* key
  * free keyword to describe the content of the site
* subs
  * subsection of the web site, not official CIM section
* free
  * free field
  * Example: Use to to add content type
* Each parameter name and parameter value can be together up to 50 characters long, including the equal sign (**=**).
* The total number of characters in parameter names and their values may be up to 200.
* The vertical bar (**|**) and the equal sign (**=**) symbols are not allowed in parameters.
* The slash (**/**) character can be used as a separator between levels of the structure and therefore cannot be used in the name of one node of the tree
* Letters with accent marks (á, ą, â, ă, ä, etc.) are not allowed and must be changed to Latin letters
* The following characters are not allowed in the values of parameters &#39;lan&#39; and &#39;key&#39;
  * \{ \} [ ] ()&#34; &#39; ~ \` ! @ # $ % ^ &amp; \* ? ; , : / | =

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Identifier**
  * Supplied by CIM gemiusPrism
* **Language**
  * The language of the page.
  * Example: NL.
  * You can dynamically override this value with a mapping.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`identifier`| Account Identifier|
|`lanuage`| Language|
|`key`| Keyword|
|`subs`| Subsection|
|`free`| Free field|
|`section`| Section|
