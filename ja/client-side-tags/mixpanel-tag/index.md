---
title: Mixpanelタグ構成ガイド
description: この記事では、Mixpanelタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/mixpanel-tag/
---
## タグのヒント

* マッピングを使用して：
  * 標準トークン値を動的に上書きする
  * イベントトリガーを構成する
  * 必須およびオプションのイベントパラメータを送信する

* 詳細情報については、[Mixpanel実装ガイド](https://developer.mixpanel.com/docs/javascript-full-api-reference)を参照してください。

## タグ構成

まず、Tealiumのタグマーケットプレイスに移動し、Mixpanelタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、次の構成を行います：

* **トークン**
  * 英数字の値

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

## 標準

|変数| 説明|
|---| ---|
|トークン| 英数字のトークン|

### イベント

イベントをマップするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

|変数| 説明|
|---| ---|
|`add_group`| グループ追加|
|`alias`| エイリアス|
|`clear_opt_in_out_tracking`| オプトイン・オプトアウトトラッキングのクリア|
|`disable`| 無効化|
|`get_config`| コンフィグ取得|
|`get_distinct_id`| ディスティンクトID取得|
|`get_group`| グループ取得|
|`get_property`| プロパティ取得|
|`has_opted_in_tracking`| オプトイントラッキング有|
|`has_opted_out_tracking`| オプトアウトトラッキング有|
|`identify`| 識別|
|`init`| 初期化|
|`opt_in_tracking`| オプトイントラッキング|
|`opt_out_tracking`| オプトアウトトラッキング|
|`push`| プッシュ|
|`register`| 登録|
|`register_once`| 一度だけ登録|
|`remove_group`| グループ削除|
|`reset`| リセット|
|`set_config`| コンフィグ構成|
|`set_group`| グループ構成|
|`time_event`| タイムイベント|
|`track`| トラック|
|`track_forms`| フォームトラッキング|
|`track_links`| リンクトラッキング|
|`track_with_groups`| グループと一緒にトラッキング|
|`unregister`| 登録解除|

### Peopleイベント

イベントをマップするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

|変数| 説明|
|---| ---|
|`people.append`| 追加|
|`people.clear_charges`| チャージクリア|
|`people.delete_user`| ユーザー削除|
|`people.increment`| インクリメント|
|`people.remove`| 削除|
|`people.set`| 構成|
|`people.set_once`| 一度だけ構成|
|`people.track_charge`| チャージトラッキング|
|`people.union`| ユニオン|
|`people.unset`| アンセット|

### Groupイベント

イベントをマップするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

|変数| 説明|
|---| ---|
|`group.remove`| 削除|
|`group.set`| 構成|
|`group.set_once`| 一度だけ構成|
|`group.union`| ユニオン|
|`group.unset`| アンセット|
