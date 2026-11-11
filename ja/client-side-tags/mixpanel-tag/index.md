---
title: Mixpanelタグ構成ガイド
description: この記事では、Mixpanelタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/mixpanel-tag/
---
## タグに関するヒント

* マッピングを使用して、以下を行います。
  * 標準のトークン値を動的に上書きする
  * イベントトリガーを構成する
  * 必須および任意のイベントパラメータを送信する

* 詳細については、[Mixpanel実装ガイド](https://docs.mixpanel.com/docs/tracking-methods/integrations/tealium)を参照してください。

## タグの構成

タグマーケットプレイスに移動し、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を構成します。

* **トークン**
  * 英数字の値

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下のとおりです。

## 標準

|変数|説明|
|---|---|
|トークン|英数字のトークン|

### イベント

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を参照してください。

|変数|説明|
|---|---|
|`add_group`|グループを追加|
|`alias`|エイリアス|
|`clear_opt_in_out_tracking`|オプトイン／オプトアウトトラッキングをクリア|
|`disable`|無効化|
|`get_config`|構成を取得|
|`get_distinct_id`|一意のIDを取得|
|`get_group`|グループを取得|
|`get_property`|プロパティを取得|
|`has_opted_in_tracking`|トラッキングにオプトイン済みか確認|
|`has_opted_out_tracking`|トラッキングからオプトアウト済みか確認|
|`identify`|識別|
|`init`|初期化|
|`opt_in_tracking`|トラッキングにオプトイン|
|`opt_out_tracking`|トラッキングからオプトアウト|
|`push`|プッシュ|
|`register`|登録|
|`register_once`|1回のみ登録|
|`remove_group`|グループを削除|
|`reset`|リセット|
|`set_config`|構成を指定|
|`set_group`|グループを指定|
|`time_event`|イベント時間を計測|
|`track`|トラッキング|
|`track_forms`|フォームをトラッキング|
|`track_links`|リンクをトラッキング|
|`track_with_groups`|グループとともにトラッキング|
|`unregister`|登録解除|

### Peopleイベント

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を参照してください。

|変数|説明|
|---|---|
|`people.append`|追加|
|`people.clear_charges`|課金情報をクリア|
|`people.delete_user`|ユーザーを削除|
|`people.increment`|増加|
|`people.remove`|削除|
|`people.set`|構成|
|`people.set_once`|1回のみ構成|
|`people.track_charge`|課金をトラッキング|
|`people.union`|結合|
|`people.unset`|構成解除|

### グループイベント

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を参照してください。

|変数|説明|
|---|---|
|`group.remove`|削除|
|`group.set`|構成|
|`group.set_once`|1回のみ構成|
|`group.union`|結合|
|`group.unset`|構成解除|