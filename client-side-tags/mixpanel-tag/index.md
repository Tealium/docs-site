---
title: Mixpanel Tag Setup Guide
description: This article describes how to set up the Mixpanel tag.
url: https://docs.tealium.com/client-side-tags/mixpanel-tag/
---
## Tag tips

* Use mapping to:
  * Dynamically override the standard token value
  * Configure event triggers
  * Send required and optional event parameters

* For more information, see the [Mixpanel Implementation Guide](https://docs.mixpanel.com/docs/tracking-methods/integrations/tealium).

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Token**
  * An alphanumeric value

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

## Standard

|Variable| Description|
|---| ---|
|Token| Alphanumeric token|

### Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/tag-management/data-mappings/manage/).

|Variable| Description|
|---| ---|
|`add_group`| Add Group|
|`alias`| Alias|
|`clear_opt_in_out_tracking`| Clear Opt in Opt out Tracking|
|`disable`| Disable|
|`get_config`| Get Config|
|`get_distinct_id`| Get Distinct ID|
|`get_group`| Get Group|
|`get_property`| Get Property|
|`has_opted_in_tracking`| Has Opted in Tracking|
|`has_opted_out_tracking`| Has Opted out Tracking|
|`identify`| Identify|
|`init`| Init|
|`opt_in_tracking`| Opt in Tracking|
|`opt_out_tracking`| Opt out Tracking|
|`push`| Push|
|`register`| Register|
|`register_once`| Register Once|
|`remove_group`| Remove Group|
|`reset`| Reset|
|`set_config`| Set Config|
|`set_group`| Set Group|
|`time_event`| Time Event|
|`track`| Track|
|`track_forms`| Track Forms|
|`track_links`| Track Links|
|`track_with_groups`| Track with Groups|
|`unregister`| Unregister|

### People Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/tag-management/data-mappings/manage/).

|Variable| Description|
|---| ---|
|`people.append`| Append|
|`people.clear_charges`| Clear Charges|
|`people.delete_user`| Delete User|
|`people.increment`| Increment|
|`people.remove`| Remove|
|`people.set`| Set|
|`people.set_once`| Set Once|
|`people.track_charge`| Track Charge|
|`people.union`| Union|
|`people.unset`| Unset|

### Group Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/tag-management/data-mappings/manage/).

|Variable| Description|
|---| ---|
|`group.remove`| Remove|
|`group.set`| Set|
|`group.set_once`| Set Once|
|`group.union`| Union|
|`group.unset`| Unset|
