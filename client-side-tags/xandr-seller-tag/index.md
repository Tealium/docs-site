---
title: Xandr Seller Tag Setup Guide
description: This article describes how to set up the Xandr Seller tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/xandr-seller-tag/
---Xandr Seller Tag (AST) is a single tag that handles multiple placements per page & supports different ad formats.

## Tag tips

* Use the mapping toolbox to map ad sizes and to target div ids and inventory codes.
* Use the Content Modification extension to add a new Ad Target Div.
* Ad Size format example: **[[300,250],[728,90]]**

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Member ID**  
Your Xandr supplied member ID.
* **endpoint**  
The Impression Bus endpoint to which ad requests are made.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Page Level Options

|Variable| Description|
|---| ---|
|Member ID (setPageOpts.member)| [Number]|
|keywords (setPageOpts.keywords)| [Object]|
|keywords custom (setPageOpts.keywords.custom)| [String]|
|disablePsa (setPageOpts.disablePsa)| [Boolean]|
|enableSafeFrame (setPageOpts.enableSafeFrame)| [Boolean]|
|user (setPageOpts.user)| [Object]|
|age (setPageOpts.user.age)| [Number]|
|externalUid (setPageOpts.user.externalUid)| [String]|
|segments (setPageOpts.user.segments)| [Array of Numbers]|
|gender (setPageOpts.user.gender)| [String]|
|dnt (setPageOpts.user.dnt)| [Boolean]|
|language (setPageOpts.user.language)| [String]|

### Define Tag

|Variable| Description|
|---| ---|
|tagId [Number]| tagId|
|sizes [Array of Numbers]| sizes|
|sizeMapping [Array of Objects]| sizeMapping|
|targetId [String]| targetId|
|forceCreativeId [Number]| forceCreativeId|
|allowSmallerSizes [Boolean]| allowSmallerSizes|
|allowedFormats [Array of Strings]| allowedFormats|
|position [String]| position|
|disablePsa [Boolean]| disablePsa|
|nobidIfUnsold [Boolean]| nobidIfUnsold|
|keywords [Object]| keywords|
|keywords.custom [string]| keywords.custom|
|trafficSourceCode [String]| trafficSourceCode|
|privateSizes [Array of Numbers]| privateSizes|
|supplyType [String]| supplyType|
|pubClick [String]| pubClick|
|reserve [Number]| reserve|
|extInvCode [String]| extInvCode|
|native [Object]| native|
|externalImpId [String]| externalImpId|
|enableSafeFrame [Boolean]| enableSafeFrame|
|Member ID (Override) [Number]| member|
|allowExpansionByPush [Boolean]| setSafeFrameConfig.allowExpansionByPush|
|allowExpansionByOverlay [Boolean]| setSafeFrameConfig.allowExpansionByOverlay|
|rendererOptions [Object]| rendererOptions|
|- playerTechnology [Array]| rendererOptions.playerTechnology|
|- adText [String]| rendererOptions.adText|
|- showMute [Boolean]| rendererOptions.showMute|
|- showVolume [Boolean]| rendererOptions.showVolume|
|- showProgressBar [Boolean]| rendererOptions.showProgressBar|
|- allowFullscreen [Boolean]| rendererOptions.allowFullscreen|
|- skippable [Object]| rendererOptions.skippable|
|- videoThreshold [Number]| rendererOptions.skippable.videoThreshold|
|- videoOffset [Number]| rendererOptions.skippable.videoOffset|
|- skipLocation [String]| rendererOptions.skippable.skipLocation|
|- skipText [String]| rendererOptions.skippable.skipText|
|- skipButtonText [String]| rendererOptions.skippable.skipButtonText|

### Device Options

|Variable| Description|
|---| ---|
|appid (setPageOpts.app.appid)| [Object]|
|device (setPageOpts.device)| [Object]|
|deviceId (setPageOpts.device.deviceId)| [Object]|
|idfa (setPageOpts.device.deviceId.idfa)| [String]|
|aaid (setPageOpts.device.deviceId.aaid)| [String]|
|md5udid (setPageOpts.device.deviceId.md5udid)| [String]|
|sha1udid (setPageOpts.device.deviceId.sha1udid)| [String]|
|windowsadid (setPageOpts.device.deviceId.windowsadid)| [String]|
|deviceType (setPageOpts.device.deviceType)| [String]|
|useragent (setPageOpts.device.useragent)| [String]|
|geo (setPageOpts.device.geo)| [Object]|
|ip (setPageOpts.device.ip)| [String]|
|make (setPageOpts.device.make)| [String]|
|model (setPageOpts.device.model)| [String]|
|os (setPageOpts.device.os)| [String]|
|osVersion (setPageOpts.device.osVersion)| [String]|
|carrier (setPageOpts.device.carrier)| [String]|
|connectionType (setPageOpts.device.connectionType)| [Number]|
|mcc (setPageOpts.device.mcc)| [String]|
|mnc (setPageOpts.device.mnc)| [String]|
|devTime (setPageOpts.device.devTime)| [Number]|
