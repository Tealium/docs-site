---
title: AudienceOne Discovery Tag Setup Guide
description: This article describes how to set up the AudienceOne Discovery tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/audienceone-discovery-tag/
---
## Tag tips

* Sends the following server-side attributes back to Tealium:
  * `event_name` = `aoneready`
  * `aone_tuuid`
  * `aone_home_zip`
  * `aone_work_zip`
  * `aone_demographic`
  * `aone_interest`

* If left blank, Tealium Account and Tealium Profile will be automatically populated with your current TiQ account and profile.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Account ID**
  * Your AudienceOnce Account ID.

* **Tealium Account**
  * (Optional) Your Tealium account.

* **Tealium Profile**
  * (Optional) Your Tealium profile.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable          | Description                       |
|:------------------|:----------------------------------|
| `account_id`      | <ul><li>Account ID</li></ul>      |
| `tealium_account` | <ul><li>Tealium Account</li></ul> |
| `tealium_profile` | <ul><li>Tealium Profile</li></ul> |
