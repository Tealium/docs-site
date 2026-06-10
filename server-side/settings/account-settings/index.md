---
title: Server-side account settings
description: The following article describes all Customer Data Hub profile settings.
url: https://docs.tealium.com/server-side/settings/account-settings/
---
To view your profile settings, log in to your account and click your initials in the upper-right corner of the screen. Then, select **Settings** from the drop-down list.

After you change editable settings, click **Save**, followed by **Save/Publish**, to apply the changes.

Read-only (non-editable) settings can only be changed by Tealium Support or the Account Manager.

## General settings

* **Enable Concurrency** (Read Only): Allow account admins to toggle Server-Side Concurrency at the profile level.
* **Activate AudienceStream** (Read Only): Enable/disable all AudienceStream features for the current profile.
* **AudienceStream Event Filter** (Read Only): Enter the **Event Attribute** name and value (case insensitive). Only events matching this condition are sent to AudienceStream. Leaving these fields empty sends all events to AudienceStream.
    While the filter only accepts a single attribute name and value, the event filter is applied after server-side enrichments are applied, which allows for more complex filtering based on a custom attribute using enrichments and rules.
* **Visitor Stitching** (Read Only): Enable to merge visitor profiles across platforms, devices, and browsers when they originate from the same visitor. Default value is **ON**.
* **Profile Retention Time** (Read Only): Set the retention time for visitor profiles. A visitor&#39;s last event determines the retention start time, in days.
* **Display/UI Time Zone** (Read Only): Select the time zone to display for actions on the connectors dashboard, the AudienceStream dashboard, and the Tealium Insights dashboards.
    * Options are **Greenwich Mean Time (GMT)** or **Local Time**.
    * Selecting **Local Time** displays the browser time for the user currently logged in.
* **Enable Rule Dependency Checking**: Ensure that attribute dependencies on rules are captured and executed in the correct order. Default value is **ON**.
    We recommend that you set this option to **On**. If this setting is set to **Off**, rules are not taken into consideration when calculating execution order and, if there are rule dependencies, enrichments are not guaranteed to execute in the correct order.
* **Enable Visitor IP Attribute** (Read Only): Make the visitor’s IP address available as an attribute named **Client IP**. This attribute can be mapped in connectors and used in enrichments and rules.
    * Data layer enrichment key: `client_ip`.
    * Available in AudienceStore as `current_visit.last_event.client_ip`.
    * Default value is **OFF**.
    The Client IP attribute is not visible in **Live Events** or **Trace**. To see the values of this attribute in **Live Events** or **Trace**, enrich a separate attribute with the Client IP attribute.
* **Enrichment Order Respects UI Order**: Enable this option to update the way enrichments are ordered to respect the order that they appear in the user interface.
    * Default value is **ON**.
* **Usage Report Start Date** (Read Only): Set the date to use as the default start date for usage reports.

## DataAccess

* **Event Data Storage** (Read Only): Enable Event Data Storage on the account.
    * A signed contract is required before enabling Event Data Storage.
* **Audience Data Storage** (Read Only) Enable Audience Data Storage on the account.
    * A signed contract is required before enabling Audience Data Storage
* **Enable Spectrum** (Read Only): Enable Spectrum on the account.
    * Before enabling Spectrum for existing customers who have been using DataAccess, a data migration is needed to ensure all existing and new data are written to the correct location. 
    * To request this feature, open a ticket with Tealium Support.
    * Default value is **OFF**.
* **EventStore Retention Time** (Read Only): Determines how long EventStore data is retained.
    * Default value is **390 days** (13 months).
* **EventDB Retention Time** (Read Only): Determines how long EventDB data is retained.
    * Default value is **90 Days**.

## EventStream connectors

* **Activate EventStream Connectors** (Read Only): Enable/disable EventStream connectors for events features for the current profile.
    * Default value is **ON**.

## Region

* **Region** (Read Only): The region is the authority storage location for your data. Typically, you should choose a geographic location closest to a high percentage of your customers.
    * Some clients have legal restrictions that require their data be stored in a specific geographic location.
    * If you are unsure which is the best region for this profile, select **Oregon** and request an Optimal Authority Region report from Customer Success Leadership. They will provide the region recommendation after collecting a few days of data.
    Any data collected in an incorrect region may be discarded.

## Daily visitor query cap

* **Sample Size of Daily Visitors to Process** (Read Only): Determines the sample size of visitors used to project results in **Audience Sizing** and **Audience Discovery** queries.
    * Audience Sizing jobs run on total visitors matched, not just those from the sample. For more information, see [Audience Sizing]().
    * Default value is **100000**.

## Predict

* **Enable Predict Premium** (Read Only): Enable Predict Premium plan for the profile.
    * When enabling or disabling this feature, adjust **Max Number of Model Trainings** and **Max Number of Concurrently Deployed Models** to reflect the current contract.

## Consent Enforcement

* **Legacy Consent Enforcement**: When enabled, apply the [legacy consent category enforcement rules]() to the current profile:
    * Event actions are blocked unless they satisfy the legacy consent conditions, which rely on the predefined consent categories.
    * Enabled by default for existing profiles, disabled for newly-created profiles or 
profiles that use [consent orchestration]().
    * If consent orchestration is deactivated, legacy enforcement settings remain unchanged, allowing for continuity in operations unless manually adjusted.

 This setting cannot be turned on while consent orchestration has active purpose groups. 