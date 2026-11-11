---
title: Tealium Configuration MCP について
description: Tealium Configuration MCP は、自然言語を使用してサーバーサイドプロファイルを調査・構成するための AI ネイティブなインターフェイスです。
url: https://docs.tealium.com/ja/server-side/config-mcp/about-config-mcp/
---

<blockquote>
Tealium Configuration MCP は、一部のお客様のみご利用いただけます。この機能の利用に関心がある場合は、[サポートにお問い合わせください](https://docs.tealium.com/support/)。
</blockquote>


Tealium Configuration MCP は、AI クライアントをサーバーサイドプロファイルに接続します。これにより、Tealium UI を操作する代わりに、自然言語を使用して構成の調査、変更、および新しいバージョンのコミットを行えます。

オーディエンスの作成、依存関係の把握、未使用の構成の特定など、ビジネス目標を記述すると、Tealium Configuration MCP がその目標を必要なプロファイル構成に変換します。

Tealium Configuration MCP は、AI が生成した変更をプロファイルのドラフトリビジョンとしてステージングします。パブリッシュするには、Tealium UI で別途レビューおよび操作を行う必要があります。

## 要件

この機能を利用するには、以下が必要です。

* **有料の Claude プラン：** Claude Pro、Max、Team、または Enterprise プランが必要です。無料プランではカスタムコネクタを追加できません。

Tealium Configuration MCP は、プライベートクラウドアカウントでは利用できません。

アカウントで Tealium Configuration MCP を有効にするには、[サポートにお問い合わせください](https://docs.tealium.com/support/)。

## 仕組み

Tealium Configuration MCP は、独立したコマンドの集まりではなく、ガイド付きのステートフルなセッションとして機能します。Tealium Configuration MCP はセッションの状態を管理し、プロファイルのドラフトを維持するとともに、変更を検証して適用するタイミングを制御します。質問するか、加えたい変更について説明すると、Tealium Configuration MCP が必要な手順を実行します。

各セッションでは、以下のワークフローを使用します。

1. **バージョンを選択します。** チャットセッションの開始時に、エージェントが作業対象とするプロファイルバージョン（**最新のパブリッシュ済みバージョン**、**最新の保存済みバージョン**、または特定のリビジョン）を尋ねます。一時的なドラフトコピーが作成されます。セッション中のすべての変更は、そのドラフトに適用されます。
1. **調査します。** プロファイルについて質問するか、変更を依頼します。エージェントは、既存の構成の説明、依存関係の追跡、および希望する変更の計画作成を行えます。Tealium Configuration MCP が処理を進める前に、計画を確認してください。
1. **パッチを適用します。** 計画を確認すると、Tealium Configuration MCP は変更を順次パッチとしてドラフトに適用し、プロファイルの整合性を継続的に検証しながら、競合の自動解決を試みます。
1. **コミットします。** すべての変更が完了すると、エージェントが概要を提示します。概要を確認してコミットします。
1. **UI でレビューします。** Tealium UI で新しく保存されたバージョンを開いて変更を確認し、組織の承認プロセスを完了した後、手動でパブリッシュします。


<blockquote>
Tealium Configuration MCP がプロファイルの変更をパブリッシュすることはありません。保存されたすべてのバージョンは、Tealium UI で手動でパブリッシュする必要があります。
</blockquote>


## ユースケース

Tealium Configuration MCP は、[サポート対象オブジェクト](#supported-objects)の範囲内で、通常 Tealium UI から実行するほとんどの構成タスクに対応しています。一般的なユースケースは次のとおりです。

**既存の構成を調査する**

プロファイルの要約、エンティティの検索、ルールとロジックの説明、および構成間の接続関係の確認を行います。

```wrap
Provide a summary of attributes available in my Tealium profile. Group them by their scope (event/visit/visitor).
```

```wrap
Summarize the rules behind audience A, so I better understand when a user joins or leaves.
```

```wrap
Which connectors are being used most across my configured actions, and what use cases do they support?
```

**依存関係とリネージを追跡する**

特定の属性を参照するエンリッチメント、オーディエンス、ルール、コネクタ、アクションなど、エンティティの上流および下流の参照関係を特定します。

```wrap
Are attributes used by audience A used by any other audiences?
```

```wrap
What is the downstream impact if I change the enrichment of attribute X?
```

```wrap
Which of my active audiences are not wired to any actions or connectors?
```

**個別のエンティティを作成する**

属性、オーディエンス、ルール、イベント仕様、その他の利用可能なエンティティなど、サポート対象のプロファイルオブジェクトを追加します。

```wrap
Create a new basic webhook action for the VIP audience. The webhook URL is https://webhook.site/a1b2c3d4-1234-5678-abcd-ef1234567890. The method is POST. Include the entire visitor payload. Trigger when visitors join the audience.
```

```wrap
Create a visitor tally that counts how many different product IDs the user purchases, when tealium_event is 'purchase'.
```

**相互接続されたワークフローを作成する**

ビジネスユースケースを記述し、その実装に必要な一連の関連エンティティと参照を作成します。

```wrap
Develop a use case in Tealium to understand the intent of a user who is browsing the e-commerce site attached to the profile. Add users into five distinct audiences that can be targeted in paid media.
```

```wrap
As a <industry> company, recommend additional use cases to configure in my Tealium profile.
```

**構成を変更する**

自然言語を使用して、サポート対象ワークフローのロジック、条件、または関係を更新します。

```wrap
Add a condition to the 'High Value Customers' audience so that only visitors who have made a purchase in the last 30 days are included.
```

```wrap
Exclude visitors who have already converted from the 'Prospecting' audience.
```

```wrap
Change the frequency cap on the Send Campaign Message Braze action from once per day to once per week.
```

**プロファイルの健全性を維持する**

孤立している、または使用されていないエンティティを見つけ、クリーンアップまたは削除の候補を特定します。

```wrap
Which of my attributes are currently unused, not referenced in any audience rules or enrichments?
```

```wrap
Give me an overall health summary of my Tealium profile, covering audiences, attributes, and connectors.
```

```wrap
What are the top three gaps or improvements you'd recommend based on my current profile configuration?
```

## サポート対象オブジェクト

Tealium Configuration MCP は、以下のプロファイルオブジェクトをサポートしています。

**データソース**

* タグ管理、Android、iOS、HTTP API、HTTP API - Advanced、ファイルインポート

**イベント**

* イベントフィード、イベント仕様、イベント属性（ユニバーサルデータオブジェクトのみ）、イベント属性のエンリッチメント

**訪問とオーディエンス**

* 訪問属性、訪問属性、訪問／訪問属性のエンリッチメント、オーディエンス（セグメントを除く）

**コネクタ**

* Adobe Campaign Classic、Adobe Analytics 1.4、Amplitude、AudienceStore、Braze、Databricks、Facebook Audiences、Facebook Conversions、Google Ads Customer Match (Tealium-Provided Credentials)、Google Ads Enhanced Conversions for Web、Google Analytics 4 Measurement Protocol、Google Cloud Pub/Sub (Service Account)、Google Display & Video 360 Customer Match、Google Sheets、Pinterest Conversions、Reddit Conversions、Snapchat Conversions、Snowflake Streaming、TikTok Events、Webhook

**サーバーサイドツール**

* ルール、ラベル
### オーディエンス編集の互換性

Tealium Configuration MCPでは、既存のオーディエンスを調査し、セグメントを使用しないオーディエンスを作成または変更できます。一部の既存オーディエンスはTealium Configuration MCPで表示できますが、現在のAudiences UIで公開されるまでは条件を変更できません。

オーディエンスを編集可能にするには、**Activate > Audiences**でそのオーディエンスを開き、何も変更せずに保存して公開します。公開すると、オーディエンスは現在の構成形式に自動的にアップグレードされます。公開後、新しいMCPセッションを開始します。次回のツール呼び出し時に、Tealium Configuration MCPは新しく公開されたバージョンが利用可能であることを通知しますが、現在のセッションのドラフトには古いバージョンのオーディエンスが引き続き保持されます。このアップグレードは恒久的なものであり、元に戻すことはできません。

**サポート対象外**

Tealium Configuration MCPでは、以下はサポートされていません。

* クラウドデータソース、Data Cloud Activation、セグメント、セグメントを含むオーディエンス、オーディエンスへのデータ投入、オーディエンス検出、オーディエンスサイズ算出、オーディエンスジョブ
* Tealium Insights、Context API、Functions、DataAccess、Data Connect、Predict
* タグ管理（クライアント側）、同意オーケストレーション

## 制限事項

**セッションごとに1つのプロファイル：** 各セッションは1つのプロファイルに接続します。プロファイルを切り替えるには、User Preferencesを更新し、Tealium Configuration MCPに再接続します。プロファイルを変更すると、現在のセッションは無効になります。

**コネクタの認証情報は作成不可：** Tealium Configuration MCPでは、送信コネクタの認証情報を作成できません。既存のコネクタを再利用し、それらに対して新しいコネクタアクションを作成できます。または、不完全な状態で新しいコネクタを作成し、Tealium UIで認証情報を手動で追加します。

**シークレットにはアクセス不可：** アクセストークンやパスワードなど、プロファイルに保存されている認証情報は、エージェントに届く前に除外されます。Tealium Configuration MCPでは、それらを取得または表示できません。

**公開不可：** 変更を反映するには、Tealium UIで手動で公開する必要があります。

**Tealium UIとTealium Configuration MCPによる同時編集：** セッションがアクティブな間にTealium UIで新しいバージョンが公開された場合、次回MCPツールが呼び出しを行ったときにエージェントから通知されます。セッションを継続し、後でマージ競合を手動で解決するか、現在のセッションを破棄して、公開された最新バージョンから新しいセッションを開始できます。

**セッションの有効期限：** セッションは、4日間操作がないと期限切れになります。長期間セッションを離れる前に、変更をコミットしてください。戻った後、新しいセッションを開始し、コミットしたバージョンを`Latest Saved`として読み込みます。

**トークン使用量：** 大規模または複雑なプロファイルでは、セッションごとにより多くのトークンが必要です。Claude Pro、Max、Team、またはEnterpriseプランが必要です。

**サポートされているAIクライアント：** Tealium Configuration MCPは、Claude（claude.ai、Claude Desktop、Claude Code CLI）で動作します。