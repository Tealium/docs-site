---
title: AudienceOne Discovery Tag Setup Guide
description: This article describes how to set up the AudienceOne Discovery tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/audienceone-discovery-tag/
---
## Tag Tips

* Sends the following server-side attributes back to Tealium:
  * `event_name` = `aoneready`
  * `aone_tuuid`
  * `aone_home_zip`
  * `aone_work_zip`
  * `aone_demographic`
  * `aone_interest`

* If left blank, Tealium Account and Tealium Profile will be automatically populated with your current TiQ account and profile.

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the AudienceOne Discovery Tag tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Account ID**
  * Your AudienceOnce Account ID.

* **Tealium Account**
  * (Optional) Your Tealium account.

* **Tealium Profile**
  * (Optional) Your Tealium profile.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable          | Description                       |
|:------------------|:----------------------------------|
| `account_id`      | &lt;ul&gt;&lt;li&gt;Account ID&lt;/li&gt;&lt;/ul&gt;      |
| `tealium_account` | &lt;ul&gt;&lt;li&gt;Tealium Account&lt;/li&gt;&lt;/ul&gt; |
| `tealium_profile` | &lt;ul&gt;&lt;li&gt;Tealium Profile&lt;/li&gt;&lt;/ul&gt; |
