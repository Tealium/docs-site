---
title: Data Connect インテグレーションについて
url: https://docs.tealium.com/ja/server-side/data-connect/manage-data-connect-integrations/about-integrations/
---

<blockquote>
Data Connect を有効にしてレシピの作成と管理を開始するには、[サポートにお問い合わせください](https://docs.tealium.com/support/)。
</blockquote>


Data Connect は Workato を使用して自動化されたローコードインテグレーションを作成し、データを Tealium に取り込む方法とタイミングをカスタマイズできるようにします。

カスタム[レシピ](https://docs.tealium.com/workato-glossary/)を使用すると、ソースデータに対する特定のスケジュール、[トリガー](https://docs.tealium.com/workato-glossary/)、[アクション](https://docs.tealium.com/workato-glossary/)、およびエラー処理を選択できます。

## 前提条件

* Tealium のレシピで使用する [Workato の用語](https://docs.tealium.com/workato-glossary/)を学習します。
* レシピ設計について学ぶには、[Workato のドキュメント](https://docs.workato.com/recipes/building-recipes.html)を参照してください。
* 最初のレシピを作成するには、[Workato のチュートリアル](https://docs.workato.com/getting-started/build-first-recipe.html)を使用してください。
* Workato のレシピについて、より詳細なトレーニングを受けたい場合は、[Workato 認定資格](https://docs.workato.com/training/automation-institute.html#what-is-automation-institute)にお申し込みください。
* [Data Connect レシピのベストプラクティス](https://docs.tealium.com/data-connect-recipe-best-practices/)を確認してください。

## 許可する IP アドレス

セキュリティ要件やサードパーティアプリによっては、Data Connect の IP アドレスを許可リストに追加する必要があります。Data Connect に関連付けられた IP アドレスの詳細については、Workato のドキュメントにある [Workato からのトラフィック](https://docs.workato.com/security/ip-allowlists.html#traffic-from-workato)を参照してください。

## レシピの作成

Data Connect でのレシピ作成は、すべて同じ基本ワークフローに従います。

1. [Tealium Connect データソースを構成します](https://docs.tealium.com/tealium-connect-data-source/)。
1. [イベント仕様を作成します](https://docs.tealium.com/tealium-connect-event-spec/)。
1. [Customer Data Platform（CDP）で訪問 ID 属性のエンリッチメントを構成します](https://docs.tealium.com/tealium-connect-visitor-id-attr-enrichment/)。
1. [レシピを作成します](https://docs.tealium.com/create-recipe-data-connect/)。
1. [トリガーを選択します](https://docs.tealium.com/create-recipe-data-connect/#step-1-select-a-trigger)。
1. [アクションを構成します](https://docs.tealium.com/create-recipe-data-connect/#step-2-configure-an-action)。
1. [エラー処理を構成します](https://docs.tealium.com/create-recipe-data-connect/#step-3-configure-error-handling)。