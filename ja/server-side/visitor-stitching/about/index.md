---
title: 訪問スティッチングについて
description: 訪問スティッチングは、プラットフォーム、デバイス、ブラウザー間で活動を同じ訪問に関連付けるためのアイデンティティ解決の一形態です。この記事では、訪問スティッチングの仕組み、訪問ID属性の効果的な使用方法、およびベストプラクティスについて説明します。
url: https://docs.tealium.com/ja/server-side/visitor-stitching/about/
---
Tealium AudienceStream CDPをフル活用するためには、訪問を特定することが重要なステップです。ユーザーが登録したり購入を完了したりするなど、特定の訪問イベントが発生した場合、`email_address_hash` や `customer_id` などのイベント属性を使用してその訪問を一意に識別する機会があります。これらの識別属性が複数のセッションにわたってデータレイヤーで提供されると、AudienceStreamは訪問スティッチングと呼ばれるプロセスを使用して、それらのセッションから訪問属性を1つのマスター訪問プロファイルに結合することができます。


<blockquote>
アカウントマネージャーに連絡して、アカウントとプロファイルで訪問スティッチングを有効にしてもらってください。
</blockquote>


Tealiumのアイデンティティ解決プロセスでは、以下のような複数の属性が使用されます：

* **匿名識別子** &ndash; サイト訪問またはアプリ使用ごとにTealium Collectによって生成される匿名で一意の値。
* **ユーザー識別子** &ndash; デバイス、プラットフォーム、ブラウザー間でユーザーを一意に識別する識別子（例：メールアドレス）。
* **訪問ID属性** &ndash; セッションやデバイス間でユーザーを識別するために訪問スティッチングで使用される属性。訪問ID属性はユーザーIDから値を取得し、同じ訪問ID属性値を持つ訪問プロファイルを単一のプロファイルに結合するために使用されます。訪問スティッチングに使用する訪問ID属性を選択することは、AudienceStream構成の重要な部分です。詳細については、[訪問ID属性]()を参照してください。

詳細については、[匿名ID、ユーザーID、および訪問ID属性]()および[ユーザー識別子の選択に関するベストプラクティス]()を参照してください。

## アイデンティティ解決の仕組み

アイデンティティ解決は、ブラウザーやデバイス間で[user identifiers]()を収集し照合するプロセスであり、訪問のブランドとのエンゲージメントの統一されたビューを作成します。

たとえば、新しい訪問があなたのブランドとウェブサイトやアプリでやり取りすると、Tealium Collectは[anonymous ID]()を生成し、AudienceStreamに送信されたデータに含まれます。これにより、訪問属性を格納する新しい訪問プロファイル、AudienceStreamのレコードが作成されます。同じ訪問は、デバイスやブラウザーごとにAudienceStreamに複数のプロファイルを持つことがあり、時間が経つにつれてさらに多くのデータが蓄積されます。

訪問がメールアドレスなどのユーザー識別子を提供することで自身のアイデンティティを確認すると、Tealium Collectはこのユーザー識別子をAudienceStreamに送信して、既知の訪問であることを示します。ユーザー識別子はAudienceStreamの訪問ID属性に入力されます。特定の訪問ID属性がAudienceStreamのユーザーID属性から入力されると、訪問スティッチングが初めてトリガーされます。

![](https://docs.tealium.com/images/server-side/multiplevisitstounifiedprofile.png)

### プロファイルがどのように結合されるか

訪問スティッチングは、単に2つ以上のプロファイルのデータを単一のプロファイルに結合することを超えます。できるだけ正確な統一プロファイルを作成するために、Tealiumの独自技術は、訪問の旅の順序に基づいて新しいプロファイルを構築するために、各ステッチされたプロファイルからデータを再生します。

ステッチされたプロファイルは削除されません。新しいプロファイルには、各ステッチされたプロファイルへのリンクを含む`replaces`配列が含まれています。各ステッチされたプロファイルには、新しいプロファイルへのリンクを含む`replaced by`属性が含まれています。ステッチされたプロファイルの匿名IDは依然として訪問の検索や削除に使用することができます。ステッチされたプロファイルの匿名IDを参照するイベントは、新しいプロファイルをエンリッチすることになります。`replaces`属性についての詳細は、[AudienceDB tables](https://docs.tealium.com/audiencedb-data-guide/#audiencedb-tables)および[Visitor record format](https://docs.tealium.com/audiencestore-data-guide/#visitor-record-format)を参照してください。

スティッチングはリアルタイムで行われ、新しく結合されたプロファイルはすぐに行動に移すことができます。これにより、パーソナライゼーション、リマーケティング、リターゲティングのアクションがより個人化され、効果的になります。

詳細については、[訪問スティッチングの例]()を参照してください。


<blockquote>
訪問プロファイルがステッチされた後は、それらを分離することはできません。
</blockquote>


### 訪問の切り替え

2人のユーザーが同じデバイスを共有している場合、両方のユーザーは同じ匿名IDを持っています。彼らが同じウェブサイトを訪れるが、異なるユーザー識別子（メールアドレスや顧客IDなど）を使用する場合、これを訪問の切り替えと呼びます。Tealiumサポートまたはプロフェッショナルサービスが訪問の切り替えを処理するソリューションの実装を支援することができます。詳細については、以下のTealiumナレッジベース記事を参照してください：

* [Anonymous User Tracking under ITP with Visitor Switching in AudienceStream](https://support.tealiumiq.com/en/support/solutions/articles/36000441645-anonymous-user-tracking-under-itp-with-visitor-switching-in-audiencestream)
* [Visitor Switching in iQ](https://support.tealiumiq.com/en/support/solutions/articles/36000419055-visitor-switching-in-iq)
* [Visitor Switching in Tealium Mobile SDKs](https://support.tealiumiq.com/en/support/solutions/articles/36000493080-visitor-switching-in-tealium-mobile-sdks)

## AudienceStreamが識別子を評価する方法

AudienceStreamがイベントを処理する際、匿名ID (`tealium_visitor_id`) は、ユーザー識別子や訪問ID属性よりも先に評価されます。唯一の例外は、ファイルインポートデータソースからのイベントの場合で、評価順序は訪問IDマッピングによって決定されます。

以下のシナリオは、匿名IDとユーザー識別子がAudienceStreamの訪問プロファイルにどのように影響するかを説明しています：

* **新しい匿名訪問** &ndash; 匿名IDが既存のプロファイルと一致しない場合、新しい訪問プロファイルが作成されます。

    ![](https://docs.tealium.com/images/server-side/icon-visitor-profile-unknown2.png)

* **更新された匿名訪問** &ndash; 匿名IDが訪問プロファイルと一致する場合、イベントは既存のプロファイルを豊かにします。

    ![](https://docs.tealium.com/images/server-side/anonuserenrichesprofile.png)

* **識別された訪問** &ndash; イベントに訪問ID属性をエンリッチするように構成されたユーザー識別子が含まれ、訪問ID属性がまだ入力されていない場合、ユーザー識別子は訪問ID属性を豊かにし、イベントは既存のプロファイルを豊かにします。
    ![](https://docs.tealium.com/images/server-side/useridtoknownuser.png)

* **匿名訪問が識別された訪問と一致する** &ndash; イベントに訪問ID属性をエンリッチするように構成されたユーザー識別子が含まれ、そのユーザー識別子が既存のプロファイルの訪問ID属性と一致する場合、2つのプロファイルは結合されます。

* **複数の識別子** &ndash; イベントに複数のユーザー識別子が含まれる場合、対応する訪問ID属性はOR条件として属性ID順に評価されます。これは、最初に作成された訪問ID属性が最初に評価されることを意味します。一部のエッジケースでは、評価の順序がプロファイルの結合方法に影響を与える可能性があります。特に、プロファイルが共通の匿名IDを持たない場合です。