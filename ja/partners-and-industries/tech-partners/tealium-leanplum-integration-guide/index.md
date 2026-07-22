---
title: Tealium + Leanplum 統合ガイド
description: この記事では、TealiumとLeanplumを最大限に活用する方法について説明します。
url: https://docs.tealium.com/ja/partners-and-industries/tech-partners/tealium-leanplum-integration-guide/
---Leanplumコネクタを活用して、TealiumからLeanplumへユーザー属性データを渡し、リアルタイムのメッセージをトリガーします。

## 前提条件 

* **Tealium** - EventStreamおよび/またはAudienceStream
* **Leanplum** - Leanplumアカウント


## 仕組み

Leanplumは、データをユーザーのニーズと欲求の理解に変換することで、先見の明を持つブランドが顧客のリアルタイムのニーズを満たすのに役立ちます。エンゲージメントキャンペーンを最適化し、複数のコミュニケーションチャネルを使用することで、Leanplumプラットフォームはタイムリーで、テスト済みで、関連性のある統一された体験を提供し、顧客のロイヤルティを築き、ビジネスの成長を促進します。

詳細については、[Tealium + Leanplum Technology Partnership Overview](https://tealium.com/technology-partner/leanplum/)をご覧ください。



<blockquote>
Leanplumコネクタを構成する際には、各アクションで使用されるエンドポイントとAPIバージョンを指定する必要があります。
</blockquote>


## APIバージョン

* Leanplum APIバージョンはすべてのアクションに対して1.0.6です。

## 利用可能なエンドポイント

* ユーザー属性の追跡 ([setUserAttributes API](https://docs.leanplum.com/reference#post_api-action-setuserattributes))
* イベントの追跡 ([track API](https://docs.leanplum.com/reference#post_api-action-track))
* メッセージの送信 ([sendMessage API](https://docs.leanplum.com/reference#post_api-action-sendmessage))

## 追加のリソース

* [Leanplum](https://www.leanplum.com/)
* [Tealium and Leanplum Partner Brief](https://tealium.com/assets/pdf/Partner_Brief_Leanplum-Tealium.pdf)
* [Leanplum Connector Setup Guide](https://docs.tealium.com/leanplum-connector/)
