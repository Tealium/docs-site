---
title: Bold360（旧 BoldChat）タグ構成ガイド
description: この記事では、タグ管理アカウントで Bold360（旧 BoldChat）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/bold360-formerly-boldchat-tag/
---
## タグに関するヒント

* 構成値は、Bold360 で **Setup &gt; HTML &gt; Generate Visitor Monitor HTML** の順にクリックすると確認できます。
* E-Commerce 拡張機能からの注文 ID（`_corder`）がある場合、コンバージョントラッキングイベントが自動的に送信されます。
* Conversion Ref に値をマッピングした場合も、コンバージョントラッキングがトリガーされます。
* 追加の訪問情報を送信するには、マッピングツールボックスを使用します。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の項目を構成します。

* **アカウント ID**
* **Web サイト ID**
  * 任意
  * Visitor Monitor HTML で指定されている場合にのみ追加します。

* **招待定義 ID**
  * プロアクティブ招待を使用しない場合は空欄のままにするか、マッピングを使用して動的な招待 ID を構成します。

* **コンバージョンコード ID**
  * コンバージョンコード ID は、Conversion Tracking HTML に記載されています。
  * この値は、コンバージョンイベントの場合にのみ送信されます。

* **フローティングチャットボタン定義 ID**

## データマッピング

データマッピングでは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

|変数|説明|
|---|---|
|`AccountID`| <ul><li>アカウント ID</li></ul> |
|`WebsiteDefID`| <ul><li>Web サイト定義 ID</li></ul> |
|`InvitationDefID`| <ul><li>プロアクティブ招待定義 ID</li></ul> |
|`FloatingChatButtonDefID`| <ul><li>フローティングチャットボタン定義 ID</li></ul> |
|`VisitName`| <ul><li>訪問名</li></ul> |
|`VisitPhone`| <ul><li>訪問の電話番号</li></ul> |
|`VisitEmail`| <ul><li>訪問のメールアドレス</li></ul> |
|`VisitRef`| <ul><li>訪問 ID</li></ul> |
|`VisitInfo`| <ul><li>訪問情報</li></ul> |
|`CustomUrl`| <ul><li>カスタム URL</li></ul> |
|`WindowParameters`| <ul><li>ウィンドウパラメーター</li></ul> |
|`ConversionCodeID`| <ul><li>コンバージョンコード ID</li></ul> |
|`ConversionRef`| <ul><li>コンバージョン ID または注文 ID</li></ul> |
|`ConversionAmount`| <ul><li>コンバージョン金額</li></ul> |
|`ConversionInfo`| <ul><li>コンバージョン情報</li></ul> |