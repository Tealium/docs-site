---
title: Alphonsoウェブサイトタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAlphonsoウェブサイトタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/alphonso-website-tag/
---## タグのヒント

* デフォルトの構成オプションを使用すると、タグはページに直接スニペットを配置するのと同じように動作します。
* セッションID、UTMソース、UTMメディアは自動的に入力されます。これらのオプションを自分で管理するには、これらのオプションをオフにします。
* **+ カスタムデスティネーションを追加** ボタンを使用してカスタム値を追加します。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[タグの概要](https://docs.tealium.com/about-tags/)の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **顧客ID**
  * Alphonsoから提供される値。
* **デフォルトのセッション管理を使用する**
  * コードスニペットに含まれるAlphonsoのセッション管理を使用します。
  * **いいえ**に構成した場合、セッションIDをマップする必要があります。
* **デフォルトのUTM解析を使用する**
  * コードスニペットに含まれるAlphonsoのUTMパラメータ解析を使用します。
  * **いいえ**に構成した場合、キャンペーンソースとキャンペーンメディアをマップする必要があります。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

|説明| 説明|
|---| ---|
|`cust`|  <ul><li>顧客ID</li></ul> |
|`ord`|  <ul><li>キャッシュバスター</li></ul> |
|`utm_src`|  <ul><li>キャンペーンソース</li></ul> |
|`utm_mdm`|  <ul><li>キャンペーンメディア</li></ul> |
|`url`|  <ul><li>ページURL</li></ul> |
|`title`|  <ul><li>ページタイトル</li></ul> |
|`session_id`|  <ul><li>セッションID</li></ul> |
|`sess_status`|  <ul><li>セッションステータス</li></ul> |
|`ref`|  <ul><li>リファラーURL</li></ul> |
|`event_type`|  <ul><li>イベント名</li></ul> |
|`event_value`|  <ul><li>イベント値</li></ul> |
|`useDefaultSession`|  <ul><li>デフォルトのセッション管理を使用する</li></ul> |
|`useDefaultUtm`|  <ul><li>デフォルトのUTM解析を使用する</li></ul> |
|`useOnBeforeUnload`|  <ul><li>OnBeforeUnloadピクセルを使用する</li></ul> |

