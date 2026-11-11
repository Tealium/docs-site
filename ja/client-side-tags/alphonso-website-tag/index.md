---
title: Alphonsoウェブサイトタグ構成ガイド
description: この記事では、タグ管理アカウントでAlphonsoウェブサイトタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/alphonso-website-tag/
---## タグに関するヒント

* ［デフォルト構成を使用］オプションを選択すると、スニペットをページに直接配置した場合と同じようにタグが動作します。
* セッションID、UTMソース、UTMメディアは自動的に入力されます。これらのオプションを自身で管理するには、該当するオプションをオフにします。
* **［+ カスタム送信先を追加］**ボタンを使用して、カスタム値を追加します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **顧客ID**
  * Alphonsoから提供される値。
* **デフォルトのセッション管理を使用**
  * コードスニペットに含まれるAlphonsoのセッション管理を使用します。
  * **いいえ**に構成した場合は、セッションIDをマッピングする必要があります。
* **デフォルトのUTM解析を使用**
  * コードスニペットに含まれるAlphonsoのUTMパラメータ解析を使用します。
  * **いいえ**に構成した場合は、キャンペーンソースとキャンペーンメディアをマッピングする必要があります。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|説明|説明|
|---| ---|
|`cust`|  <ul><li>顧客ID</li></ul> |
|`ord`|  <ul><li>キャッシュバスター</li></ul> |
|`utm_src`|  <ul><li>キャンペーンソース</li></ul> |
|`utm_mdm`|  <ul><li>キャンペーンメディア</li></ul> |
|`url`|  <ul><li>ページURL</li></ul> |
|`title`|  <ul><li>ページタイトル</li></ul> |
|`session_id`|  <ul><li>セッションID</li></ul> |
|`sess_status`|  <ul><li>セッションステータス</li></ul> |
|`ref`|  <ul><li>参照元URL</li></ul> |
|`event_type`|  <ul><li>イベント名</li></ul> |
|`event_value`|  <ul><li>イベント値</li></ul> |
|`useDefaultSession`|  <ul><li>デフォルトのセッション管理を使用</li></ul> |
|`useDefaultUtm`|  <ul><li>デフォルトのUTM解析を使用</li></ul> |
|`useOnBeforeUnload`|  <ul><li>OnBeforeUnloadピクセルを使用</li></ul> |