---
title: Data Connectについて
description: この記事では、Tealium Data Connectの概要について説明します。
url: https://docs.tealium.com/ja/server-side/data-connect/about/
---

<blockquote>
Data Connectは、Tealiumのお客様向けのアドオン機能です。すでにTealiumをご利用の場合は、デモおよびData Connectの詳細について、[サポートにお問い合わせください](https://docs.tealium.com/support/)。新規のお客様は、[デモをリクエストしてください](https://tealium.com/products-real-time-data-collection-and-quality/tealium-data-connect/)。
</blockquote>


Tealium Data Connectは、SaaSアプリケーション、CRM、データウェアハウスから価値のあるデータをTealiumにインポートするための、高速かつ効率的でスケーラブルなアーキテクチャを提供します。Data Connectを使用すると、エンタープライズシステムのデータをCustomer Data Platform（CDP）またはEvent Streaming API Hubに統合し、データのエンリッチメント、リアルタイムのパーソナライゼーション、およびアクティベーションに活用できます。

Data Connectでは、データワークフローを自動化、スケジュール、エンリッチメントし、次のような新しい方法でデータを活用できます。

* パーソナライゼーションの向上による顧客エンゲージメントのエンリッチメント
* 類似オーディエンスのターゲティング
* 有望なリードのターゲティング
* 顧客レコードのオプトイン／オプトアウト情報の更新

## 要件

* Event StreamingまたはCustomer Data Platform（CDP）


<blockquote>
Data Connectでは、ブラウザーでサードパーティCookieを有効にする必要がある、サードパーティのiPaaSテクノロジーを使用します。
</blockquote>


## 仕組み

Data Connectは、サードパーティのiPaaSテクノロジーである[Workato](https://www.workato.com/)を使用して、一般的に使用されているシステムとの統合を提供します。Workatoの統合は、アプリ接続と、そのアプリからデータを抽出するためのルールおよびデータマッピングロジックを含むレシピで構成されます。

次の図は、社内システムからTealiumへのデータフローを示しています。

![](https://docs.tealium.com/images/server-side/dc-events-workflow.png)

まず、Tealiumに接続するアプリを選択します。Data ConnectのWorkatoソリューションを使用すると、イベントデータをTealiumに送信する方法とタイミングをカスタマイズできます。Workatoからデータを受信するために、Data Connectでは、Data Connect専用に設計された高度なTealium Collect HTTP APIロジックを備えたTealium Connectデータソースを使用します。これらのイベントは、Event Streaming、CDP、およびFunctionsの属性エンリッチメントやコネクタで使用できます。

Workato統合の詳細については、[Data Connect統合について](https://docs.tealium.com/about-data-connect-integrations/)を参照してください。

## 主なメリット

Tealium Data Connectの主なメリットは次のとおりです。

* **ローコード統合ですぐに利用を開始**  
Data ConnectのWorkato統合を使用すると、ほとんど、またはまったくコードを記述せずにコネクタを簡単に構成し、レシピを構築できます。
* **スケジュールまたは自動でデータをインポート**    
指定したスケジュールで、またはソースデータが変更されたときに自動的にバッチでデータをインポートするWorkatoレシピを使用し、既存のデータセットに基づいて新規イベントをインポートできます。
* **カスタマイズされた自動ワークフローを使用** 
Data ConnectのWorkatoレシピでは、使用するトリガーの種類、呼び出すアプリとアクション、およびビジネスユースケースに応じたエラー処理の構成方法を選択できます。
* **他のシステムの履歴コンテキストでリアルタイムデータとインサイトを補完**  
Snowflake、Salesforce、HubSpotなどのシステムから価値のあるデータをインポートし、Tealiumで活用できるようにします。データウェアハウス、CRMシステム、クラウドアプリケーションなどのデータソースへ、より簡単にアクセスできます。
* **データ変換をワークフローに直接追加**  
レシピを使用すると、自動ワークフローにデータ変換を追加し、Tealiumへのデータインポート処理をより効率化できます。

## 次のステップ

Data Connectを使い始める準備はできましたか？

* Tealiumでレシピを使用するための[Workatoの用語](https://docs.tealium.com/workato-glossary/)を確認します。
* レシピの設計については、[Workatoのドキュメント](https://docs.workato.com/recipes/building-recipes.html)を参照してください。
* [Workatoのチュートリアル](https://docs.workato.com/getting-started/build-first-recipe.html)を使用して、最初のレシピを作成します。
* Workatoレシピについて、さらに詳しいトレーニングを受けたい場合は、[Workato認定資格](https://docs.workato.com/training/automation-institute.html#what-is-automation-institute)にお申し込みください。

準備ができたら、Tealiumでのレシピ作成の詳細について、[Data Connect統合について](https://docs.tealium.com/about-data-connect-integrations/)を参照してください。