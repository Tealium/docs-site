---
title: FullStoryタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでFullStoryタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/fullstory-tag/
---## タグのヒント

* 高度な構成で、バンドルフラグを**はい**に構成し、待機フラグを**いいえ**に構成して、FullStoryができるだけ早く録画を開始するようにします。
* マッピングを使用して：
  * 識別されたユーザーのユーザーIDを送信します（`FS.identify`）。
  * 追加のユーザーパラメータを送信します（`FS.identify`と`FS.setUserVars`）。
  * パラメータ付きのイベントを送信します（`FS.event`）。
  * イベントソースを上書きします（デフォルトは`tealium`）。
  * FullStoryのデバッグを有効にします。
  * データレイヤーにFullStoryセッションIDを追加するのを停止します。
  * `FS.identify`と`FS.setUserVars`メソッドにTealiumセッションIDを送信するのを停止します。
  * `FS.identify`と`FS.setUserVars`メソッドにTealium訪問IDを送信するのを停止します。
* イベント名変数に値が存在するときにイベントが送信されます。
* フルイベントオブジェクトが存在する場合、個々のカスタムイベントパラメータは送信されません。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[タグの概要](https://docs.tealium.com/about-tags/)記事を参照してください。

タグを追加するときには、次の構成を行います：

* **Org ID**
  * あなたのFullStory Org ID
* **Namespace**
  * あなたのFullStory JavaScriptネームスペース

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
|`fs_debug`|  <ul><li>文字列</li><li>FullStoryデバッグを有効にする</li><li>値は**true**または**false**。</li></ul> |
|`get_fs_session_id`|  <ul><li>文字列</li><li>FullStoryセッションIDを取得する</li><li>値は**true**または**false**。</li></ul> |
|`get_tealium_session_id`|  <ul><li>文字列</li><li>TealiumセッションIDを取得する</li><li>値は**true**または**false**。</li></ul> |
|`get_tealium_visitor_id`|  <ul><li>文字列</li><li>Tealium訪問IDを取得する</li><li>値は**true**または**false**。</li></ul> |
|`fs_consent`|  <ul><li>文字列</li><li>ユーザートラッキングの同意</li><li>値は**true**または**false**。</li></ul> |
|`fs_script`|  <ul><li>文字列</li><li>スクリプトURL</li></ul> |

### ユーザーパラメータ

|変数| 説明|
|---| ---|
|`uid`|  <ul><li>文字列</li><li>ユーザーID</li></ul> |
|`uservars.displayName`|  <ul><li>文字列</li><li>ユーザー表示名</li></ul> |
|`uservars.email`|  <ul><li>文字列</li><li>ユーザーのメール</li></ul> |
|`uservars.custom`|  <ul><li>カスタムユーザーVar</li></ul> |

### イベント

|変数| 説明|
|---| ---|
|`fs_event_name`|  <ul><li>文字列</li><li>イベント名</li></ul> |
|`fs_event_source`|  <ul><li>文字列</li><li>イベントソース</li></ul> |
|`s_event.custom`|  <ul><li>個々のカスタムイベントパラメータ</li></ul> |
|`fs_event_object`|  <ul><li>オブジェクト</li><li>フルイベントオブジェクト</li></ul> |

### ページイベント

|変数| 説明|
|---| ---|
|`fs_page.pageName`|  <ul><li>文字列</li><li>ページ名</li></ul> |
|`fs_page.category`|  <ul><li>文字列</li><li>ページカテゴリ</li></ul> |
|`fs_page.title`|  <ul><li>文字列</li><li>ページタイトル</li></ul> |
|`fs_page.url`|  <ul><li>文字列</li><li>ページURL</li></ul> |
|`fs_page.image_url`|  <ul><li>文字列</li><li>ページ画像URL</li></ul> |
|`fs_page.custom`|  <ul><li>個々のカスタムページパラメータ</li></ul> |
|`fs_page_object`|  <ul><li>オブジェクト</li><li>フルページオブジェクト</li></ul> |

