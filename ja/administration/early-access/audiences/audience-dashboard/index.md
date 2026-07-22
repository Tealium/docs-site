---
title: オーディエンスダッシュボード
description: この記事ではオーディエンスダッシュボードについての情報を提供します。
url: https://docs.tealium.com/ja/administration/early-access/audiences/audience-dashboard/
---

<blockquote>
オーディエンスダッシュボードはEarly Access中で、選ばれた顧客のみが利用可能です。この機能を試してみたい場合は、Tealiumアカウントマネージャーに連絡してください。
</blockquote>


オーディエンスダッシュボードは、時間を追ってオーディエンスサイズを監視し、成長しているトップオーディエンスと減少しているトップオーディエンスを特定し、参加と離脱の活動を追跡するための事前構築されたビジュアルを提供します。

## 要件

オーディエンスダッシュボードを使用するには、プロファイルでオーディエンスダッシュボード機能を有効にする必要があります。この機能を有効にするには、Tealiumアカウントマネージャーに連絡してください。

オーディエンスダッシュボードは、`ap-southeast-1`（香港）リージョンでは利用できません。

## ダッシュボードの生成

オーディエンスダッシュボードを生成するには：

1. **Analyze > Insights > Templates**に移動します。
1. **Audience dashboard**テンプレートを見つけて、**View Details**をクリックします。
1. **Generate Dashboard**をクリックします。

オーディエンスダッシュボードを生成した後、データが表示されるまで最大2時間かかる場合があります。ダッシュボードは1時間ごとに更新されます。

プロファイルでオーディエンスダッシュボード機能を無効にすると、ダッシュボードと関連データセットは30日後に削除される予定です。データを保持するには、この期間内に機能を再度有効にしてください。

## ダッシュボードへのアクセス

オーディエンスダッシュボードにアクセスするには、**Analyze > Audience Dashboard**または**Activate > Audiences**に移動し、**View Dashboard**リンクをクリックします。

ダッシュボードの管理についての詳細は、[Manage dashboards]()を参照してください。

## ダッシュボードフィルター

ダッシュボードのすべてのビジュアルに適用されるフィルターは以下の通りです：

* **Label**: ラベルによるオーディエンスのフィルタリング。複数選択が可能です。
* **Is Audience Active**: アクティブなオーディエンス、非アクティブなオーディエンス、または両方をフィルタリングします。複数選択が可能です。

## 事前構築されたビジュアル

オーディエンスダッシュボードテンプレートには、オーディエンスデータを監視するための以下の事前定義されたビジュアルが含まれています。

### オーディエンス概要

オーディエンス概要タイルは、プロファイル内のオーディエンスを要約するKPIタイルを表示します：

* **Total Audiences**: プロファイルで定義されたすべてのオーディエンスの総数。
* **Active Audiences**: 少なくとも1つのアクティブなコネクタアクションを持つオーディエンスの数。
* **Inactive Audiences**: アクティブなコネクタアクションがないオーディエンスの数。

![](https://docs.tealium.com/images/server-side/data-insights/audience-dashboard-kpi.png)

### トップオーディエンスの変化

トップオーディエンスの変化は、過去30日間のメンバーシップ変更でトップのオーディエンスを示します。各テーブルには、オーディエンスID、オーディエンス名、現在のオーディエンスサイズ、パーセンテージ変更、および絶対変更が含まれます。

* **Top Audiences Increases Last 30 Days**: 最も高いパーセンテージで成長しているオーディエンス。
* **Top Audiences Declines Last 30 Days**: 最も大きなパーセンテージで減少しているオーディエンス。

![](https://docs.tealium.com/images/server-side/data-insights/audience-dashboard-top-changes.png)

### オーディエンスサイズ

オーディエンスサイズタイルは、各オーディエンスの現在のサイズを示す横棒グラフです。オーディエンスサイズは時点のスナップショットであり、日付範囲フィルタが変更されても更新されません。時系列ビューについては、[Details](#details)セクションの**Audience Size**を参照してください。

![](https://docs.tealium.com/images/server-side/data-insights/audience-dashboard-audiences-size.png)

### 詳細

詳細セクションでは、個々のオーディエンスの時系列データを表示します。このセクションのチャート全体でデータをフィルタするためにこれらのコントロールを使用します：

* **Audience Name**: 特定のオーディエンスを選択するか、すべてのオーディエンスを表示します。
* **Aggregation**: 日、週、月、四半期、または年単位でデータをグループ化します。
* **Date range**: デフォルトは過去30日です。

選択したコントロールに基づいて更新される以下のチャート：

* **Audience Size**: 選択した日付範囲にわたるオーディエンスサイズを示す折れ線グラフ。
* **Joined vs. Left**: 選択した日付範囲にわたる参加数と結合した離脱、削除、パージ、およびステッチ数を示す棒グラフ。

**Audience Size**

![](https://docs.tealium.com/images/server-side/data-insights/audience-dashboard-audience-size.png)

**Joined vs. Left**

![](https://docs.tealium.com/images/server-side/data-insights/audience-dashboard-joined-vs-left.png)
