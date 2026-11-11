---
title: 匿名ID、ユーザー識別子、訪問ID属性
description: この記事では、ID解決に関わる主要な構成要素である匿名ID、ユーザー識別子、訪問ID属性について説明します。
url: https://docs.tealium.com/ja/server-side/visitor-stitching/anonymous-user-visitor-id-attributes/
---
## 匿名ID

<div style="float: right">
    ![](https://docs.tealium.com/images/server-side/icon-user-anonymous.png)
</div>

匿名IDは、サイトへの訪問時またはアプリの使用時に訪問へ割り当てられる、一意の匿名値です。この値はTealium Collectによって生成され、`utag_main_v_id`という名前のファーストパーティCookieに保存されます。また、Event Streaming API Hubでは`tealium_visitor_id`として受信されます。Tealiumの匿名IDは、同じブラウザーまたはアプリからの複数回の訪問にわたって訪問を追跡しますが、異なるブラウザーやデバイス間では追跡しません。

Webデータの場合、ほとんどのケースで、この匿名IDはサードパーティCookieの`TAPID`（Event Streaming属性の`tealium_thirdparty_visitor_id`）としても保存されます。このCookieは、必要とする企業が同じブラウザー内でドメインをまたいで訪問を追跡するために使用できます。

匿名IDごとにCustomer Data Platform（CDP）で新しい訪問プロファイルが生成されます。このプロファイルは、訪問ステッチと呼ばれるプロセスで、共通のユーザー識別子を使用して別のプロファイルと統合できます。

## ユーザー識別子

<div style="float: right">
   ![](https://docs.tealium.com/images/server-side/icon-user-identifiers-circle.png)
</div>

ユーザー識別子は、Tealium環境に構成されたデータレイヤー変数、またはイベント、訪問、訪問の各属性であり、デバイス、プラットフォーム、ブラウザーをまたいで既知のユーザーを一意に識別します。

ユーザー識別子は、次のいずれかとして構成できます。

* Tag Managementのデータレイヤー変数
* Event Streamingのイベント属性
* Customer Data Platform（CDP）の訪問または訪問文字列属性

ユーザー識別子の値は訪問ごとに一意である必要がありますが、運転免許証番号、銀行口座番号、メールアドレスなどの個人識別情報（PII）を含めないでください。適切なユーザー識別子は一意であり、PIIを含みます。PIIを含むユーザー識別子はハッシュ化する必要があります。適切な例として、`email_address_hash`、`member_id`、`customer_id`があります。

たとえば、メールアドレスをユーザー識別子として使用するには、一意の値を維持しながら元のデータを隠すため、その値をハッシュ化された文字列に変換します。

ユーザー識別子は、CDPの[訪問ID属性](#visitor-id-attributes)に値を構成するために使用されます。

ユーザー識別子の詳細については、[ユーザー識別子を選択するためのベストプラクティス]()を参照してください。

## 訪問ID属性

訪問ID属性はCDPの特殊な属性タイプで、[ユーザー識別子](#user-identifiers)から値を取得し、訪問ステッチで使用されます。複数のセッションにわたってユーザー識別子が提供されると、CDPは訪問ステッチと呼ばれるプロセスを使用して、それらの訪問プロファイルの訪問属性を1つのプロファイルに統合します。

訪問ID属性は、CDPによって自動的には作成されません。CDPで訪問ID属性を作成し、値を構成するユーザー識別子を選択する必要があります。詳細については、[訪問ID属性]()を参照してください。


<blockquote>
訪問ID属性を構成すると、その値は変更できません。
</blockquote>


ユーザー識別子`email_address_hash`（イベント属性）によって値が構成される、`Hashed Email`という名前の訪問ID属性の例：

![](https://docs.tealium.com/images/server-side/email-addr-hash-vistor-id-attr.png)