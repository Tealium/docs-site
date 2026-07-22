---
title: Acoustic Transact Connector Setup Guide
description: This article describes how to set up the Acoustic Transact (formerly Silverpop Transact) connector.
url: https://docs.tealium.com/server-side-connectors/acoustic-transact-connector/
---

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Transactional Email| ✓| ✗|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API OAuth2 Client ID**
  * Required
  * OAuth2 Client ID
  * Contact Acoustic Support for assistance.

* **API OAuth2 Client Secret**
  * Required
  * OAuth2 Client Secret
  * Contact Acoustic Support for assistance.

* **API OAuth2 Refresh Token**
  * Required
  * OAuth2 Client Refresh Token
  * Contact Acoustic Support for assistance.

* **Transact API Pod Number**
  * Required
  * Your transact server number, which usually matches your Acoustic Campaign Organization Pod number.
  * Hint: In the example `transact-campaign-us-X.goacoustic.com`, `X` is your pod number.
  * Contact Acoustic Support for assistance.

* **Transact API Region**
  * Required
  * Your server region.
  * Hint: In the example `transact-campaign-ZZ-5.goacoustic.com`, `ZZ` is your region.
  * If not provided, " `us`" region is used by default.
  * Contact Acoustic Support for assistance.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab to configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Transactional Email

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Campaign ID|  <ul><li>(Required) ID of the Transact Automated Message Group that is used for the mailing.</li></ul> |
|Recipient Email|  <ul><li>(Required) The email address to which the transactional email is sent.</li></ul> |
|Transaction ID|  <ul><li>(Optional) Used by the sender to uniquely identify a transaction.</li><li>The value that is specified is returned in the Response Document if used in the original request.</li></ul> |
|Save Column(s)|  <ul><li>(Optional) A list of column names from the recipient elements to save to the database in Acoustic Campaign.</li><li>The column names are case sensitive and must match what was specified in Acoustic Campaign.</li><li>If you do not use this element, Acoustic Campaign will not save any column names.</li></ul> |
|Content/Body Type|  <ul><li>(Required) Parameter to define if the content body is HTML only or TEXT only.</li></ul> |
|Content Personalization (Map TAG Value to TAG Name)|  <ul><li>(Required) At least one personalization block is required for providing the content for the email to be sent.</li><li>Each Personalization element contains one Name/Value pair.</li><li>Map **Tag Value** to **Tag Name** Where:  <ul><li>**Tag Name** specifies the name of the personalization string used in the body of the mailing template for the mailing, and</li><li>**Tag Value** specifies the value of the corresponding `TAG_NAME` element.</li></ul> </li><li>Tag Names must exactly match the fields used in Acoustic Campaign.</li><li>Boolean values (**true**, **false**) must be in lowercase.</li><li>The Transact server does not process any code (logic or transformation) placed in text or CDATA content, including anything inserted by Template fields.</li><li>If the text contains angle brackets ( `<` or `>`), you must enclose it within a CDATA section.</li></ul> |
