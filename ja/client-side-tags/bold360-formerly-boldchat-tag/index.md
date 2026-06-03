---
title: Bold360（旧BoldChat）タグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでBold360（旧BoldChat）タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/bold360-formerly-boldchat-tag/
---
## タグのヒント

* 構成値は、Bold360に移動して**構成 &amp;gt; HTML &amp;gt; ビジターモニターHTMLを生成**をクリックすることで見つけることができます。
* E-Commerce拡張からOrder ID（`_corder`）がある場合、Conversion Trackingイベントは自動的に送信されます。
* Conversion Refに値をマッピングすると、Conversion Trackingもトリガーされます。
* 追加の訪問情報を送信するためにマッピングツールボックスを使用します。

## タグの構成

まず、Tealiumのタグマーケットプレイスに移動し、Bold360（旧BoldChat）タグを追加します（[タグの追加方法]()について詳しくはこちら）。

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

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[Data Mappings](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは次のとおりです：

### 標準

|変数| 説明|
|---| ---|
|`AccountID`|  &lt;ul&gt;&lt;li&gt;アカウントID&lt;/li&gt;&lt;/ul&gt; |
|`WebsiteDefID`|  &lt;ul&gt;&lt;li&gt;ウェブサイト定義ID&lt;/li&gt;&lt;/ul&gt; |
|`InvitationDefID`|  &lt;ul&gt;&lt;li&gt;プロアクティブ招待定義ID&lt;/li&gt;&lt;/ul&gt; |
|`FloatingChatButtonDefID`|  &lt;ul&gt;&lt;li&gt;フローティングチャットボタン定義ID&lt;/li&gt;&lt;/ul&gt; |
|`VisitName`|  &lt;ul&gt;&lt;li&gt;訪問名&lt;/li&gt;&lt;/ul&gt; |
|`VisitPhone`|  &lt;ul&gt;&lt;li&gt;訪問電話番号&lt;/li&gt;&lt;/ul&gt; |
|`VisitEmail`|  &lt;ul&gt;&lt;li&gt;訪問メール&lt;/li&gt;&lt;/ul&gt; |
|`VisitRef`|  &lt;ul&gt;&lt;li&gt;訪問ID&lt;/li&gt;&lt;/ul&gt; |
|`VisitInfo`|  &lt;ul&gt;&lt;li&gt;訪問情報&lt;/li&gt;&lt;/ul&gt; |
|`CustomUrl`|  &lt;ul&gt;&lt;li&gt;カスタムURL&lt;/li&gt;&lt;/ul&gt; |
|`WindowParameters`|  &lt;ul&gt;&lt;li&gt;ウィンドウパラメータ&lt;/li&gt;&lt;/ul&gt; |
|`ConversionCodeID`|  &lt;ul&gt;&lt;li&gt;コンバージョンコードID&lt;/li&gt;&lt;/ul&gt; |
|`ConversionRef`|  &lt;ul&gt;&lt;li&gt;コンバージョンIDまたはオーダーID&lt;/li&gt;&lt;/ul&gt; |
|`ConversionAmount`|  &lt;ul&gt;&lt;li&gt;コンバージョン金額&lt;/li&gt;&lt;/ul&gt; |
|`ConversionInfo`|  &lt;ul&gt;&lt;li&gt;コンバージョン情報&lt;/li&gt;&lt;/ul&gt; |
