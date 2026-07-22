---
title: Bold360（旧BoldChat）タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでBold360（旧BoldChat）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/bold360-formerly-boldchat-tag/
---
## タグのヒント

* 構成値は、Bold360に移動して**構成 &gt; HTML &gt; ビジターモニターHTMLを生成**をクリックすることで見つけることができます。
* E-Commerce拡張からOrder ID（`_corder`）がある場合、Conversion Trackingイベントは自動的に送信されます。
* Conversion Refに値をマッピングすると、Conversion Trackingもトリガーされます。
* 追加の訪問情報を送信するためにマッピングツールボックスを使用します。

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Bold360（旧BoldChat）タグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加した後、以下の構成を行います：

* **アカウントID**
* **ウェブサイトID**
  * 任意
  * Visitor Monitor HTMLで指定されている場合のみ追加します

* **招待定義ID**
  * プロアクティブな招待がない場合は空白にします、またはマッピングを使用して動的な招待IDを構成します。

* **コンバージョンコードID**
  * コンバージョンコードIDは、Conversion Tracking HTMLで見つけることができます。
  * この値はコンバージョンイベントのためだけに送信されます。

* **フローティングチャットボタン定義ID**

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
|`AccountID`|  <ul><li>アカウントID</li></ul> |
|`WebsiteDefID`|  <ul><li>ウェブサイト定義ID</li></ul> |
|`InvitationDefID`|  <ul><li>プロアクティブ招待定義ID</li></ul> |
|`FloatingChatButtonDefID`|  <ul><li>フローティングチャットボタン定義ID</li></ul> |
|`VisitName`|  <ul><li>訪問名</li></ul> |
|`VisitPhone`|  <ul><li>訪問電話番号</li></ul> |
|`VisitEmail`|  <ul><li>訪問メール</li></ul> |
|`VisitRef`|  <ul><li>訪問ID</li></ul> |
|`VisitInfo`|  <ul><li>訪問情報</li></ul> |
|`CustomUrl`|  <ul><li>カスタムURL</li></ul> |
|`WindowParameters`|  <ul><li>ウィンドウパラメータ</li></ul> |
|`ConversionCodeID`|  <ul><li>コンバージョンコードID</li></ul> |
|`ConversionRef`|  <ul><li>コンバージョンIDまたはオーダーID</li></ul> |
|`ConversionAmount`|  <ul><li>コンバージョン金額</li></ul> |
|`ConversionInfo`|  <ul><li>コンバージョン情報</li></ul> |
