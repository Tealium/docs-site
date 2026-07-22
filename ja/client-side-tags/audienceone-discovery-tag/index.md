---
title: AudienceOne Discoveryタグの構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAudienceOne Discoveryタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/audienceone-discovery-tag/
---
## タグのヒント

* 以下のサーバーサイド属性をTealiumに送信します：
  * `event_name` = `aoneready`
  * `aone_tuuid`
  * `aone_home_zip`
  * `aone_work_zip`
  * `aone_demographic`
  * `aone_interest`

* 空白の場合、TealiumアカウントとTealiumプロファイルは現在のTiQアカウントとプロファイルで自動的に入力されます。

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、AudienceOne Discovery Tagタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加した後、以下の構成を行います：

* **アカウントID**
  * あなたのAudienceOnceアカウントID。

* **Tealiumアカウント**
  * 任意。
  * あなたのTealiumアカウント。

* **Tealiumプロファイル**
  * 任意。
  * あなたのTealiumプロファイル。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは以下の通りです：

### 標準

| 変数              | 説明                             |
|:------------------|:----------------------------------|
| `account_id`      | <ul><li>アカウントID</li></ul>      |
| `tealium_account` | <ul><li>Tealiumアカウント</li></ul> |
| `tealium_profile` | <ul><li>Tealiumプロファイル</li></ul> |

