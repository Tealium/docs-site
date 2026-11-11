---
title: Xandr Sellerタグ構成ガイド
description: この記事では、タグ管理アカウントでXandr Sellerタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/xandr-seller-tag/
---Xandr Seller Tag（AST）は、ページごとに複数のプレースメントを処理し、さまざまな広告フォーマットをサポートする単一のタグです。

## タグに関するヒント

* マッピングツールボックスを使用して、広告サイズをマッピングし、div IDとインベントリコードをターゲットに構成します。
* Content Modification拡張機能を使用して、新しい広告ターゲットdivを追加します。
* 広告サイズのフォーマット例：**[[300,250],[728,90]]**

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **Member ID**  
Xandrから提供されたメンバーID。
* **endpoint**  
広告リクエストの送信先となるImpression Busエンドポイント。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### ページレベルのオプション

|変数|説明|
|---|---|
|Member ID (setPageOpts.member)|[数値]|
|keywords (setPageOpts.keywords)|[オブジェクト]|
|keywords custom (setPageOpts.keywords.custom)|[文字列]|
|disablePsa (setPageOpts.disablePsa)|[ブール値]|
|enableSafeFrame (setPageOpts.enableSafeFrame)|[ブール値]|
|user (setPageOpts.user)|[オブジェクト]|
|age (setPageOpts.user.age)|[数値]|
|externalUid (setPageOpts.user.externalUid)|[文字列]|
|segments (setPageOpts.user.segments)|[数値の配列]|
|gender (setPageOpts.user.gender)|[文字列]|
|dnt (setPageOpts.user.dnt)|[ブール値]|
|language (setPageOpts.user.language)|[文字列]|

### タグの定義

|変数|説明|
|---|---|
|tagId [数値]|tagId|
|sizes [数値の配列]|sizes|
|sizeMapping [オブジェクトの配列]|sizeMapping|
|targetId [文字列]|targetId|
|forceCreativeId [数値]|forceCreativeId|
|allowSmallerSizes [ブール値]|allowSmallerSizes|
|allowedFormats [文字列の配列]|allowedFormats|
|position [文字列]|position|
|disablePsa [ブール値]|disablePsa|
|nobidIfUnsold [ブール値]|nobidIfUnsold|
|keywords [オブジェクト]|keywords|
|keywords.custom [文字列]|keywords.custom|
|trafficSourceCode [文字列]|trafficSourceCode|
|privateSizes [数値の配列]|privateSizes|
|supplyType [文字列]|supplyType|
|pubClick [文字列]|pubClick|
|reserve [数値]|reserve|
|extInvCode [文字列]|extInvCode|
|native [オブジェクト]|native|
|externalImpId [文字列]|externalImpId|
|enableSafeFrame [ブール値]|enableSafeFrame|
|Member ID (Override) [数値]|member|
|allowExpansionByPush [ブール値]|setSafeFrameConfig.allowExpansionByPush|
|allowExpansionByOverlay [ブール値]|setSafeFrameConfig.allowExpansionByOverlay|
|rendererOptions [オブジェクト]|rendererOptions|
|- playerTechnology [配列]|rendererOptions.playerTechnology|
|- adText [文字列]|rendererOptions.adText|
|- showMute [ブール値]|rendererOptions.showMute|
|- showVolume [ブール値]|rendererOptions.showVolume|
|- showProgressBar [ブール値]|rendererOptions.showProgressBar|
|- allowFullscreen [ブール値]|rendererOptions.allowFullscreen|
|- skippable [オブジェクト]|rendererOptions.skippable|
|- videoThreshold [数値]|rendererOptions.skippable.videoThreshold|
|- videoOffset [数値]|rendererOptions.skippable.videoOffset|
|- skipLocation [文字列]|rendererOptions.skippable.skipLocation|
|- skipText [文字列]|rendererOptions.skippable.skipText|
|- skipButtonText [文字列]|rendererOptions.skippable.skipButtonText|

### デバイスオプション

|変数|説明|
|---|---|
|appid (setPageOpts.app.appid)|[オブジェクト]|
|device (setPageOpts.device)|[オブジェクト]|
|deviceId (setPageOpts.device.deviceId)|[オブジェクト]|
|idfa (setPageOpts.device.deviceId.idfa)|[文字列]|
|aaid (setPageOpts.device.deviceId.aaid)|[文字列]|
|md5udid (setPageOpts.device.deviceId.md5udid)|[文字列]|
|sha1udid (setPageOpts.device.deviceId.sha1udid)|[文字列]|
|windowsadid (setPageOpts.device.deviceId.windowsadid)|[文字列]|
|deviceType (setPageOpts.device.deviceType)|[文字列]|
|useragent (setPageOpts.device.useragent)|[文字列]|
|geo (setPageOpts.device.geo)|[オブジェクト]|
|ip (setPageOpts.device.ip)|[文字列]|
|make (setPageOpts.device.make)|[文字列]|
|model (setPageOpts.device.model)|[文字列]|
|os (setPageOpts.device.os)|[文字列]|
|osVersion (setPageOpts.device.osVersion)|[文字列]|
|carrier (setPageOpts.device.carrier)|[文字列]|
|connectionType (setPageOpts.device.connectionType)|[数値]|
|mcc (setPageOpts.device.mcc)|[文字列]|
|mnc (setPageOpts.device.mnc)|[文字列]|
|devTime (setPageOpts.device.devTime)|[数値]|