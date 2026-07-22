---
title: LiveRamp Realtime Identity Link Pixelタグの構成ガイド（廃止）
description: この記事では、LiveRamp Realtime Identity Link Pixelタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/liveramp-realtime-identity-link-pixel-tag/
---

<blockquote>
LiveRamp Realtime Identity Link Pixelタグは廃止され、サポートされていません。
</blockquote>


## タグのヒント

* 以下のサーバーサイド属性をTealiumに戻します：
  * `RampID`

* LiveRamp Realtime Identity Link Pixelは、Tealium Visitor IDをLiveRamp User IDに関連付けます。

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、LiveRamp Realtime IdentityLink Pixelタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **Tealiumアカウント**
  * 任意。
  * あなたのTealiumアカウント名。
  * 空白の場合、Tealiumアカウント名は現在のTiQアカウント名で自動的に入力されます。

* **Tealiumプロファイル**
  * 任意。
  * あなたのTealiumプロファイル名。
  * 空白の場合、Tealiumプロファイル名は現在のTiQプロファイル名で自動的に入力されます。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|変数| 説明|
|---| ---|
|`tealium_account`| Tealiumアカウント|
|`tealium_profile`| Tealiumプロファイル|
