---
title: データコネクト統合について
url: https://docs.tealium.com/ja/server-side/data-connect/manage-data-connect-integrations/about-integrations/
---

<blockquote>
データコネクトを有効にしてレシピの作成と管理を開始するには、[サポートにお問い合わせください](https://docs.tealium.com/support/)。
</blockquote>


データコネクトはWorkatoを使用して、データをTealiumに取り込む方法とタイミングをカスタマイズできる自動化されたローコードの統合を作成します。

カスタム[レシピ](https://docs.tealium.com/workato-glossary/)を使用して、ソースデータの特定のスケジュール、[トリガー](https://docs.tealium.com/workato-glossary/)、[アクション](https://docs.tealium.com/workato-glossary/)、エラーハンドリングを選択できます。

## 前提条件

* Tealiumのレシピに関する[Workatoの用語](https://docs.tealium.com/workato-glossary/)を学びます。
* [Workatoのドキュメンテーション](https://docs.workato.com/recipes/building-recipes.html)を読んでレシピ設計について学びます。
* [Workatoのチュートリアル](https://docs.workato.com/getting-started/build-first-recipe.html)を使用して最初のレシピを作成します。
* Workatoのレシピについてより深く学びたいですか？[Workatoの認定](https://docs.workato.com/training/automation-institute.html#what-is-automation-institute)にサインアップします。
* [データコネクトレシピのベストプラクティス](https://docs.tealium.com/data-connect-recipe-best-practices/)について理解します。

## 許可するIPアドレス

あなたのセキュリティ要件やサードパーティのアプリケーションによっては、データコネクトのIPアドレスを許可リストに追加する必要があるかもしれません。データコネクトに関連するIPアドレスの詳細については、Workatoのドキュメンテーションの[Traffic from Workato](https://docs.workato.com/security/ip-allowlists.html#traffic-from-workato)を参照してください。

## レシピの作成

データコネクトでの任意のレシピの作成は、基本的に以下のワークフローに従います：

1. [Tealium Connectデータソースの設定](https://docs.tealium.com/tealium-connect-data-source/)。
1. [イベント仕様の作成](https://docs.tealium.com/tealium-connect-event-spec/)。
1. [AudienceStreamの訪問者ID属性のためのエンリッチメントの設定](https://docs.tealium.com/tealium-connect-visitor-id-attr-enrichment/)。
1. [レシピの作成](https://docs.tealium.com/create-recipe-data-connect/)。
1. [トリガーの選択](https://docs.tealium.com/create-recipe-data-connect/#step-1-select-a-trigger)。
1. [アクションの設定](https://docs.tealium.com/create-recipe-data-connect/#step-2-configure-an-action)。
1. [エラーハンドリングの設定](https://docs.tealium.com/create-recipe-data-connect/#step-3-configure-error-handling)。
