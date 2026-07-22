---
title: Xandrセラータグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでXandrセラータグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/xandr-seller-tag/
---Xandr Seller Tag (AST)は、ページごとに複数の配置を処理し、さまざまな広告形式をサポートする単一のタグです。

## タグのヒント

* マッピングツールボックスを使用して広告サイズをマップし、div idとインベントリーコードをターゲットにします。
* Content Modification拡張機能を使用して新しいAd Target Divを追加します。
* 広告サイズの形式の例: **[[300,250],[728,90]]**

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。タグの追加方法については、[Tag Overview](https://docs.tealium.com/about-tags/)の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **Member ID**  
Xandrから提供されるメンバーID。
* **endpoint**  
広告リクエストが行われるImpression Busエンドポイント。

## データマッピング

マッピングは、[data layer variable](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### ページレベルのオプション

|変数| 説明|
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

### タグの定義

|変数| 説明|
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

### デバイスオプション

|変数| 説明|
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

