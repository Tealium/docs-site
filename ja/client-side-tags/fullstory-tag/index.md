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

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[タグの概要]()記事を参照してください。

タグを追加するときには、次の構成を行います：

* **Org ID**
  * あなたのFullStory Org ID
* **Namespace**
  * あなたのFullStory JavaScriptネームスペース

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
|`fs_debug`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;FullStoryデバッグを有効にする&lt;/li&gt;&lt;li&gt;値は**true**または**false**。&lt;/li&gt;&lt;/ul&gt; |
|`get_fs_session_id`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;FullStoryセッションIDを取得する&lt;/li&gt;&lt;li&gt;値は**true**または**false**。&lt;/li&gt;&lt;/ul&gt; |
|`get_tealium_session_id`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;TealiumセッションIDを取得する&lt;/li&gt;&lt;li&gt;値は**true**または**false**。&lt;/li&gt;&lt;/ul&gt; |
|`get_tealium_visitor_id`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;Tealium訪問IDを取得する&lt;/li&gt;&lt;li&gt;値は**true**または**false**。&lt;/li&gt;&lt;/ul&gt; |
|`fs_consent`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザートラッキングの同意&lt;/li&gt;&lt;li&gt;値は**true**または**false**。&lt;/li&gt;&lt;/ul&gt; |
|`fs_script`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;スクリプトURL&lt;/li&gt;&lt;/ul&gt; |

### ユーザーパラメータ

|変数| 説明|
|---| ---|
|`uid`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーID&lt;/li&gt;&lt;/ul&gt; |
|`uservars.displayName`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザー表示名&lt;/li&gt;&lt;/ul&gt; |
|`uservars.email`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ユーザーのメール&lt;/li&gt;&lt;/ul&gt; |
|`uservars.custom`|  &lt;ul&gt;&lt;li&gt;カスタムユーザーVar&lt;/li&gt;&lt;/ul&gt; |

### イベント

|変数| 説明|
|---| ---|
|`fs_event_name`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;イベント名&lt;/li&gt;&lt;/ul&gt; |
|`fs_event_source`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;イベントソース&lt;/li&gt;&lt;/ul&gt; |
|`s_event.custom`|  &lt;ul&gt;&lt;li&gt;個々のカスタムイベントパラメータ&lt;/li&gt;&lt;/ul&gt; |
|`fs_event_object`|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;フルイベントオブジェクト&lt;/li&gt;&lt;/ul&gt; |

### ページイベント

|変数| 説明|
|---| ---|
|`fs_page.pageName`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ページ名&lt;/li&gt;&lt;/ul&gt; |
|`fs_page.category`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ページカテゴリ&lt;/li&gt;&lt;/ul&gt; |
|`fs_page.title`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ページタイトル&lt;/li&gt;&lt;/ul&gt; |
|`fs_page.url`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ページURL&lt;/li&gt;&lt;/ul&gt; |
|`fs_page.image_url`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;li&gt;ページ画像URL&lt;/li&gt;&lt;/ul&gt; |
|`fs_page.custom`|  &lt;ul&gt;&lt;li&gt;個々のカスタムページパラメータ&lt;/li&gt;&lt;/ul&gt; |
|`fs_page_object`|  &lt;ul&gt;&lt;li&gt;オブジェクト&lt;/li&gt;&lt;li&gt;フルページオブジェクト&lt;/li&gt;&lt;/ul&gt; |

