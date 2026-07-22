---
title: 匿名ID、ユーザー識別子、訪問ID属性
description: この記事では、アイデンティティ解決に関与する主要なコンポーネント：匿名ID、ユーザー識別子、訪問ID属性について定義します。
url: https://docs.tealium.com/ja/server-side/visitor-stitching/anonymous-user-visitor-id-attributes/
---
## 匿名ID

<div style="float: right">
    ![](https://docs.tealium.com/images/server-side/icon-user-anonymous.png)
</div>

匿名IDは、サイトを訪れるたびやアプリを使用するたびに訪問に一意かつ匿名の値が割り当てられるものです。この値はTealium Collectによって生成され、`utag_main_v_id`という名前のファーストパーティクッキーに保存され、Tealium EventStream API Hubでは`tealium_visitor_id`として受け取られます。Tealiumの匿名IDは、同じブラウザやアプリからの複数の訪問を追跡しますが、異なるブラウザやデバイス間では追跡しません。

ウェブデータについては、ほとんどの場合、この匿名IDは、それを必要とするビジネスで同じブラウザ内のドメイン間で訪問を追跡するために使用できるサードパーティクッキー`TAPID`（Tealium EventStream属性`tealium_thirdparty_visitor_id`）としても保存されます。

各匿名IDは、Tealium AudienceStream CDPで新しい訪問プロファイルを生成し、共有ユーザー識別子を使用して別のプロファイルと組み合わせることができます。これを訪問のスティッチングと呼びます。

## ユーザー識別子

<div style="float: right">
   ![](https://docs.tealium.com/images/server-side/icon-user-identifiers-circle.png)
</div>

ユーザー識別子は、デバイス、プラットフォーム、ブラウザ間で既知のユーザーを一意に識別するTealiumインストールで使用されるデータレイヤー変数またはイベント、訪問、訪問属性です。

ユーザー識別子は以下のいずれかとして構成できます：

* iQタグ管理のデータレイヤー変数
* EventStreamのイベント属性
* AudienceStreamの訪問または訪問文字列属性

ユーザー識別子の値は、各訪問に一意であるべきですが、運転免許証番号、銀行口座番号、またはメールアドレスなどの個人を特定する情報（PII）を含むべきではありません。良いユーザー識別子は一意であり、PIIを含みません。PIIを含むユーザー識別子はハッシュ化するべきです。良い例としては、`email_address_hash`、`member_id`、`customer_id`があります。

例えば、メールアドレスをユーザー識別子として使用する場合、その値をハッシュ化された文字列に変換して、元のデータを隠しながら一意の値を保持します。

ユーザー識別子は、AudienceStreamの[訪問ID属性](#visitor-id-attributes)を構成するために使用されます。

ユーザー識別子についての詳細は、[ユーザー識別子の選択に関するベストプラクティス]()を参照してください。

## 訪問ID属性

訪問ID属性は、AudienceStreamでの特別な属性タイプで、その値は[ユーザー識別子](#user-identifiers)から取得され、訪問のスティッチングに使用されます。ユーザー識別子が複数のセッションで提供されると、AudienceStreamは訪問のスティッチングと呼ばれるプロセスを使用して、それらの訪問プロファイルからの訪問属性を一つのプロファイルに結合します。

訪問ID属性はAudienceStreamによって自動的に作成されません。AudienceStreamで訪問ID属性を作成し、それらを構成するユーザー識別子を選択する必要があります。詳細については、[訪問ID属性]()を参照してください。


<blockquote>
訪問ID属性が構成されると、その値は変更できません。
</blockquote>


ユーザー識別子`email_address_hash`（イベント属性）によって構成される訪問ID属性`Hashed Email`の例：

![](https://docs.tealium.com/images/server-side/email-addr-hash-vistor-id-attr.png)