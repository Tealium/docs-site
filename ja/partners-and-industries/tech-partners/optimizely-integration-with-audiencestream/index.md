---
title: AudienceStream CDP + Optimizely X
description: AudienceStreamとOptimizelyを統合して、Optimizely ClassicまたはOptimizely Xでターゲット指向の実験を構築するためのオーディエンスを使用します。
url: https://docs.tealium.com/ja/partners-and-industries/tech-partners/optimizely-integration-with-audiencestream/
---
## 必要条件

**Tealium Collectタグのデータエンリッチメント**を**頻繁**に構成します。詳細については、[Tealium Collect構成ガイド]()を参照してください。

統合が完了すると、オーディエンスは自動的にデータレイヤーエンリッチメントを介してOptimizelyに送信されます。

## Optimizely ClassicとAudienceStreamの統合

Optimizely ClassicとAudienceStreamを統合するには2つのステップがあります：

1. `utag.sync.js`をあなたのサイトに追加します。
1. Tealiumツール：Optimizely Helperを使用してAudienceStreamとOptimizelyを接続します。

### あなたのサイトにutag.sync.jsを追加する

Optimizelyを使用する必要があるすべてのHTMLページに`utag.sync.js`を含める必要があります。一貫性を保つために、すべてのページにそれを含めることをお勧めします。

`utag.sync.js`の構成方法の詳細については、[utag.sync.jsスクリプトの使用]()を参照してください。

### AudienceStreamとOptimizelyの接続

Optimizelyでオーディエンスを使用するには、AudienceStreamとOptimizelyを接続し、次にオーディエンスをOptimizelyプロジェクトにマッピングする必要があります。これらのタスクを完了するためにTealiumツール：Optimizely Helperを使用します。

詳細については、[Tealiumツール：Optimizely Helper]()を参照してください。

## Optimizely XとAudienceStreamの統合

Optimizelyダッシュボードを使用して、Optimizely XとAudienceStreamを統合します。

1. AudienceStreamでオーディエンスを作成した後、Optimizelyにログインし、**統合**をクリックします。
1. Tealiumを**オン**に構成します。
1. あなたのTealiumアカウントIDを入力します。
1. **概要**タブを選択し、次に**オーディエンス**をクリックします。
1. 条件の下で、**Tealium**をクリックします。
1. **Tealium Audience**または**Tealium Badge**をドラッグして、Tealiumオーディエンスに基づいたOptimizely Audience条件を作成します。  
    ![](/images/tech-partners/createaudience1.png)  
    ![](/images/tech-partners/createaudience2.png)
1. **Save Audience**をクリックします。

## オーディエンスベースの実験を作成する

OptimizelyがAudienceStreamと統合されると、マッピングされたオーディエンスがプロジェクトで利用可能になり、オーディエンスベースの実験を作成できます。

実験の新しいターゲットオーディエンスを選択するには：

1. 新しい実験を作成するか、既存の実験を編集し、**オーディエンス**をクリックします。
1. **保存されたオーディエンスを追加する**をクリックし、ターゲットとするオーディエンスを選択します。
1. 実験を保存します。

