---
title: Workato用語集
description: この記事では、Workatoのインターフェースとドキュメンテーションで使用される用語について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/glossary/
---
**[アクション](https://docs.workato.com/workato-concepts.html#steps-and-actions)**: アクションは、ターゲットアプリで操作を実行します。たとえば、作成、更新、検索操作などです。各アクションには一連の入力フィールドが必要で、通常はデータを返します。例えば、出力データツリーなどです。

**[コネクション](https://docs.workato.com/connectors.html)**: レシピの構成要素です。コネクタは、特定のサードパーティアプリケーションの認証構成、トリガー、アクションで構成されています。ドキュメンテーションではこれらを「アプリ」と呼ぶことが多いです。

**[データピル](https://docs.workato.com/workato-concepts.html#datatree-and-datapills)**: データピルは、トリガーやアクションステップからの出力データです。これらは、レシピステップにビジネスロジックをマップするために使用できる変数です。

**[ジョブ](https://docs.workato.com/workato-concepts.html#jobs)**: トリガーイベントの処理と一連のアクションの実行を含むレシピのサブユニットです。

**[レシピ](https://docs.workato.com/workato-concepts.html#recipes)**: Workatoの自動化ワークフローです。レシピは、データソースからデータを引き出すアクションをトリガーしたり、エラーが発生したときにアクションを再試行したり、Tealiumにイベントを送信したりすることができます。Data Connectユーザーは、許可構成に応じてレシピを作成、編集、削除、実行することができます。

**[ステップ](https://docs.workato.com/recipes/steps.html#action-step)**: レシピステップは、アクションであったり、ビジネスロジックを記述するのに役立つ制御フローステートメントであったりします。Tealiumレシピのステップの例には、アクションステップ、リピートステップ、エラーハンドリングステップなどがあります。

**[タスク](https://docs.workato.com/recipes/tasks.html#tasks)**: 計算リソースが必要なレシピのサブユニットです。例えば、各コネクタアクション（バッチ処理、結果のメール送信、エラーハンドリングなど）は1つのタスクとしてカウントされます。レシピジョブは複数のタスクで構成されることがあり、タスクの数はレシピのロジックとトリガーイベントのデータによります。
 Data Connectが有効化された各Tealiumアカウントには、そのアカウント内のすべてのプロファイルに対するタスクの制限があります。Data Connectのタスク制限については、Tealiumのカスタマーサクセスマネージャーにお問い合わせください。

**[トリガー](https://docs.workato.com/workato-concepts.html#triggers)**: レシピで記述されたアクションを実行するために何を監視するかを決定します。トリガーはリアルタイムまたはスケジュールされたものであることがあります。

Workatoの用語についての詳細は、Workatoドキュメンテーションの[コンセプト](https://docs.workato.com/workato-concepts.html#recipes)を参照してください。
