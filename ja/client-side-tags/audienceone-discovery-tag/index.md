---
title: AudienceOne Discoveryタグ構成ガイド
description: この記事では、タグ管理アカウントでAudienceOne Discoveryタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/audienceone-discovery-tag/
---
## タグに関するヒント

* 次のサーバーサイド属性をTealiumに返します。
  * `event_name` = `aoneready`
  * `aone_tuuid`
  * `aone_home_zip`
  * `aone_work_zip`
  * `aone_demographic`
  * `aone_interest`

* 空白のままにすると、現在のTiQアカウントとプロファイルがTealiumアカウントおよびTealiumプロファイルに自動的に入力されます。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を構成します。

* **アカウントID**
  * AudienceOnceアカウントID。

* **Tealiumアカウント**
  * （任意）Tealiumアカウント。

* **Tealiumプロファイル**
  * （任意）Tealiumプロファイル。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数              | 説明                                      |
|:------------------|:------------------------------------------|
| `account_id`      | <ul><li>アカウントID</li></ul>            |
| `tealium_account` | <ul><li>Tealiumアカウント</li></ul>       |
| `tealium_profile` | <ul><li>Tealiumプロファイル</li></ul>      |