---
title: Migrate Google Ads Customer Match actions to the Google Data Manager API
description: This article explains the new Google Ads Customer Match actions that use the Google Data Manager API, why we are introducing them, and how to migrate from the existing Google Ads API–based actions.
url: https://docs.tealium.com/server-side-connectors/google-ads-customer-match-data-manager-api-migration/
---
## What’s changing

We are introducing two new actions for the [Google Ads Customer Match connector](https://docs.tealium.com/google-ads-customer-match-connector/) that use the Google Data Manager API:

* Add User to List (Data Manager API)  
* Remove User from List (Data Manager API)

These actions are designed to closely mirror the existing Add User to List and Remove User from List actions in the connector UI, but they send audience updates through Google’s Data Manager API instead of the legacy Google Ads API.

In addition, the connector configuration now includes a linking step that establishes a product link between your Google Ads account and Tealium. This link is required before you use the new Data Manager API actions.

## Why we are introducing Data Manager API actions

The Google Data Manager API is the strategic path forward for Customer Match data ingestion.

Moving the connector to this API provides the following benefits:

* Uses a formal product link between your Google Ads customer account and Tealium, so Tealium can act as an approved data partner on your behalf.  
* Removes dependence on user-level OAuth tokens for ongoing audience updates, enabling Tealium to manage ingestion using its data partner integration once the product link is in place.  
* Aligns with the Google requirements for Customer Match regarding consent, terms of service, and data formatting (including normalization and hashing of identifiers).  
* Positions your configuration for better long-term stability as Google evolves the Google Ads and Data Manager APIs.

## Deprecation of existing Google Ads API actions

The existing Google Ads API Customer Match actions in the [Google Ads Customer Match connector](https://docs.tealium.com/google-ads-customer-match-connector/) will be deprecated in a future release.

Until then, note the following:

* The existing actions continue to work.  
* We strongly recommend migrating to the new Data Manager API actions as soon as practical to minimize future changes.  
* We will communicate timelines and any breaking changes through standard release channels before removing the legacy actions.

## About the new Data Manager API actions

The new actions appear with your existing Google Ads Customer Match actions in the [Google Ads Customer Match connector](https://docs.tealium.com/google-ads-customer-match-connector/):

* Add User to List (Data Manager API)  
* Remove User from List (Data Manager API)

Key points:

* **UI layout**: The configuration screens for these actions closely follow the existing Google Ads Customer Match actions, so most of your mappings and settings will look familiar.  
* **Consent and terms**: Data Manager requires explicit consent and Customer Match terms of service to be provided with each ingestion call. The connector ensures that required consent and terms fields are present in the payload.  
* **Identifier formatting**: Map plain-text or pre-hashed identifiers (such as email, phone, and postal address). When you choose fields labeled **apply SHA256 hash**, Tealium performs the normalization (trim, lowercase, hash) required by Google. When you choose fields labeled **already SHA256 hashed**, you are responsible for providing data that already meets Google’s formatting requirements.  
* **List key types**: Lists created and managed using the Data Manager API use a list key type such as `CONTACT_ID` (email/phone/address), `USER_ID` (first-party IDs), or `MOBILE_ID` (device IDs). Your action configuration must map identifiers compatible with the list’s key type.

The **Manager Customer ID** override and other Ads API–specific sections are not used by Data Manager API actions. Configuration related to Data Manager is handled through the product link and the selected list and identifiers.

## Before you migrate

Review and complete these prerequisites before switching actions.

### Step 1: Re-authenticate the connector to include Data Manager API access

If you already have a Google Ads Customer Match connector configured in Tealium, you must re-authenticate the connector so that the Google OAuth token includes the Data Manager API scope.

To re-authenticate:

1. Open your existing [Google Ads Customer Match connector](https://docs.tealium.com/google-ads-customer-match-connector/).  
1. Use the authentication controls (**Sign in With Google** button) to sign in again with your Google account.  
1. During this process, the connector requests access that includes `https://www.googleapis.com/auth/datamanager` in addition to the existing Google Ads permissions.

This step is required before you can create the product link and use the Google Data Manager API actions.

### Step 2: Link your Google Ads customer ID to Tealium (product linking)

After re-authenticating, you must create a product link between your Google Ads customer account and Tealium.

The product link is created at the Google Ads customer account level (the owning account of the user lists) and is a prerequisite for using all Google Data Manager API actions.

If the product linking fails (for example, the link already exists or the user does not have permission), review the error message in the UI and adjust your Google Ads permissions or account selection accordingly.

To link your Google Ads customer ID to Tealium:

1. In the connector configuration, locate the section labeled **Link Customer ID to Tealium**.  
1. Enter the Google Ads customer ID used for Customer Match in this connector.  
1. Click the button labeled **Create Product Link** (or equivalent).  
1. Wait for the confirmation message in the Tealium UI indicating that the link was created successfully.

After successful linking, Tealium can submit updates to your Google Ads account using the Google Data Manager API as an approved data partner.

## How to migrate from existing Google Ads API actions

The goal is to move each existing Google Ads Customer Match action to its Google Data Manager API equivalent with minimal changes in behavior.

### Step 1: Re-authenticate and link

For each account profile where you use the [Google Ads Customer Match connector](https://docs.tealium.com/google-ads-customer-match-connector/):

1. Re-authenticate the connector so that it includes the Google Data Manager API scope.  
1. Use the **Link Customer ID to Tealium** section to create the product link for the Google Ads customer ID used by each connector action. If you are using the customer ID override feature in your action, repeat the linking process here for each list-owning customer account ID.

### Step 2: Move an existing action to the new Google Data Manager API

Either create a new action based on the existing one (recommended if you want to run both side-by-side during testing), or switch the existing action in place.

#### Option A - Copy an existing action to a new Google Data Manager API action

For each existing Google Ads API actions:

1. In the connector’s **Actions** tab, locate your existing Google Ads Customer Match action.  
1. Use the **Copy to new action** option to duplicate the configuration.  
1. In the new copy, change the action type to the Data Manager API action, for example, **Add User to List (Data Manager API)** or **Remove User from List (Data Manager API)**.  
1. Verify the following:  
   * The same user list is selected, or that any override fields are updated to use the correct list ID format for Data Manager.  
   * All required identifier mappings are present and match the list’s key type. For example, at least one of hashed email, hashed phone, or address fields for `CONTACT_ID` lists; a first-party user ID for `USER_ID` lists; or a mobile device ID for `MOBILE_ID` lists.  
1. Save the new Data Manager API action.

This approach lets you reuse your existing trigger conditions and most field mappings while switching to the new API.

#### Option B - Switch an action to the new Data Manager API action type

If you would rather not make a copy, but switch an action to the new API:

1. In the connector actions tab, locate your existing Google Ads Customer Match action.  
1. Use the **Change Action Type** option from the upper right menu to switch the action type of the action.  
1. Select the Data Manager API variant of the action.  
1. Verify the selected user list and mappings were persisted.  
1. Save the Data Manager API action.

### Step 3: Test and validate

Regardless of whether you copied an action (Option A) or switched it in place (Option B):

1. Trigger events that fire the new Data Manager API action.  
1. Verify in Google Ads that the target Customer Match list begins receiving users as expected (for add actions) or sees users removed as expected (for remove actions).  
1. Check Tealium connector logs for any errors related to Data Manager (for example, invalid identifiers, consent issues, or list configuration problems) and adjust mappings as needed.

### Step 4: Clean up legacy actions (if applicable)

If you created a copy of the action and have validated the new Data Manager API action:

1. Return to the connector’s **Actions** tab.  
1. Disable or remove the old Google Ads Customer Match action to avoid duplicate updates.

If you switched an action in place using Option B, no additional cleanup is required for that action.

After you complete these steps, your Google Ads Customer Match configuration is fully migrated to use the Google Data Manager API in Tealium.

## FAQ

**Do I need to recreate my Google Ads Customer Match lists?**  
No. The new actions can work with existing Google Ads Customer Match lists, provided those lists are compatible with the Google Data Manager API and their key types match the identifiers you send. You can also use the list management operations in the connector (where available) to create or manage lists directly through the Google Data Manager API.

**What happens if I do not migrate?**  
In the near term, your existing Google Ads API–based actions continue to function. However, because these actions are planned for deprecation, you may eventually lose the ability to manage Google Ads Customer Match audiences through them once they are removed or as Google evolves the underlying Ads API. Migrating now minimizes future disruption and aligns your configuration with the recommended path using Google Data Manager.

**Do I still control consent and data governance?**  
Yes. You remain responsible for collecting and managing end-user consent and ensuring data is shared with Google in compliance with applicable laws and Google policies. From a consent perspective, the new Google Data Manager API actions behave the same as the existing actions: the connector always sends `GRANTED` for both Google consent fields in the request payload and relies on your upstream consent and audience logic to ensure only users with appropriate consent are sent to Google.
