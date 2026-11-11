---
title: FullStoryタグ構成ガイド
description: この記事では、タグ管理アカウントでFullStoryタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/fullstory-tag/
---## タグ構成のヒント

* FullStoryができるだけ早く記録を開始できるように、詳細構成でBundle Flagを**Yes**、Wait Flagを**No**に構成します。
* マッピングを使用して、以下を行います。
  * 識別済みユーザーのユーザーIDを送信する（`FS.identify`）。
  * 追加のユーザーパラメータを送信する（`FS.identify`および`FS.setUserVars`）。
  * パラメータを含むイベントを送信する（`FS.event`）。
  * イベントソースを上書きする（デフォルトは`tealium`）。
  * FullStoryのデバッグを有効にする。
  * FullStoryセッションIDをデータレイヤーに追加しないようにする。
  * TealiumセッションIDを`FS.identify`メソッドおよび`FS.setUserVars`メソッドに送信しないようにする。
  * Tealium訪問IDを`FS.identify `メソッドおよび`FS.setUserVars`メソッドに送信しないようにする。
* イベント名変数に値が存在する場合、イベントが送信されます。
* 完全なイベントオブジェクトが存在する場合、個別のカスタムイベントパラメータは送信されません。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、以下の構成を構成します。

* **Org ID**
  * FullStoryの組織ID
* **Namespace**
  * FullStoryのJavaScript名前空間

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### 標準

|変数|説明|
|---|---|
|`fs_debug`| <ul><li>文字列</li><li>FullStoryのデバッグを有効にする</li><li>値は**true**または**false**です。</li></ul> |
|`get_fs_session_id`| <ul><li>文字列</li><li>FullStoryセッションIDを取得する</li><li>値は**true**または**false**です。</li></ul> |
|`get_tealium_session_id`| <ul><li>文字列</li><li>TealiumセッションIDを取得する</li><li>値は**true**または**false**です。</li></ul> |
|`get_tealium_visitor_id`| <ul><li>文字列</li><li>Tealium訪問IDを取得する</li><li>値は**true**または**false**です。</li></ul> |
|`fs_consent`| <ul><li>文字列</li><li>ユーザートラッキングへの同意</li><li>値は**true**または**false**です。</li></ul> |
|`fs_script`| <ul><li>文字列</li><li>スクリプトURL</li></ul> |

### ユーザーパラメータ

|変数|説明|
|---|---|
|`uid`| <ul><li>文字列</li><li>ユーザーID</li></ul> |
|`uservars.displayName`| <ul><li>文字列</li><li>ユーザー表示名</li></ul> |
|`uservars.email`| <ul><li>文字列</li><li>ユーザーのメールアドレス</li></ul> |
|`uservars.custom`| <ul><li>カスタムユーザー変数</li></ul> |

### イベント

|変数|説明|
|---|---|
|`fs_event_name`| <ul><li>文字列</li><li>イベント名</li></ul> |
|`fs_event_source`| <ul><li>文字列</li><li>イベントソース</li></ul> |
|`s_event.custom`| <ul><li>個別のカスタムイベントパラメータ</li></ul> |
|`fs_event_object`| <ul><li>オブジェクト</li><li>完全なイベントオブジェクト</li></ul> |

### ページイベント

|変数|説明|
|---|---|
|`fs_page.pageName`| <ul><li>文字列</li><li>ページ名</li></ul> |
|`fs_page.category`| <ul><li>文字列</li><li>ページカテゴリー</li></ul> |
|`fs_page.title`| <ul><li>文字列</li><li>ページタイトル</li></ul> |
|`fs_page.url`| <ul><li>文字列</li><li>ページURL</li></ul> |
|`fs_page.image_url`| <ul><li>文字列</li><li>ページ画像URL</li></ul> |
|`fs_page.custom`| <ul><li>個別のカスタムページパラメータ</li></ul> |
|`fs_page_object`| <ul><li>オブジェクト</li><li>完全なページオブジェクト</li></ul> |