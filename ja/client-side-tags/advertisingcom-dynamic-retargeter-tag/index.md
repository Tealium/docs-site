---
title: Advertising.com Dynamic Retargeterタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでAdvertising.com Dynamic Retargeterタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/advertisingcom-dynamic-retargeter-tag/
---
## タグ仕様

**名前**: Advertising.com Dynamic Retargeter (ADR)

**ベンダー**: AOL

**タイプ**: リターゲティング広告

## 要件

**サービス**: Ad Desk

**構成**:

* パートナーID

## Tealium iQでのタグ構成

### 1. タグの追加

Tealium iQのタグマーケットプレイスは、さまざまなタグを提供しています。詳細については、[タグの管理]()を参照してください。

### 2. タグの構成

![](/images/client-side-tags/no-title-1785ida9f0d6d5fac589d.png)

1. **タイトル** (必須): タグインスタンスを識別するための記述的なタイトルを入力します。
1. **パートナーID** (必須): Advertising.comからAd Desk経由で割り当てられたパートナーIDを入力します。
1. **ページタイプ** (オプション): ドロップダウンリストから、訪問の閲覧活動をキャプチャしたいページを選択します。以下に、ドロップダウンで利用可能なページタイプのリストを示します。
  * ホームページ (`hp`): サイトのホームページ。
  * ランディングページ (`lp`): 訪問がサイトに着陸した際に最初に表示されるページ。
  * 検索結果 (`sp`): このページは、訪問の検索アクションに応じて生成されます。
  * カテゴリ (`cp`): このページでは、カテゴリにグループ化されたすべての製品が表示されます。例：`www.example.com/Furniture`。
  * 製品 (`pp`): このページは、サイト上の特定の製品に専念しています。例：`www.example.com/ABCMicrowave`。
  * ショッピングカート (`ct`): このページでは、訪問のショッピングカート情報が表示されます。
  * 注文確認 (`cfp`): このページでは、最終的な購入/注文の詳細が表示されます。

ページタイプの選択を上書きするオプションがあります。また、マッピングを通じて動的に構成することも可能です。

### 3. ロードルールの適用

[ロードルール]()は、このタグのインスタンスをいつ、どこでロードするかを決定します。**すべてのページでロード**ルールは、デフォルトのロードルールです。このタグを特定のページでロードするには、関連する条件を持つ新しいロードルールを作成します。

**ベストプラクティス**: Advertising.comは、このタグを製品ページ、カートページ、確認ページにロードすることを規定しています。これを行うには、関連するロードルール条件を構成する必要があります。しかし、標準的な推奨事項は、サイトのすべてのページでこのタグをロードすることです。これにより、訪問のショッピングの好みについてより深い洞察を得ることができ、その情報を後でリターゲティングに活用することができます。

### 4. マッピングの構成

[マッピング](/ja/iq-tag-management/data-mappings/manage/)は、データレイヤーのデータソースからベンダータグの対応する宛先変数にデータを送信するシンプルなプロセスです。このタグの動的マッピングの構成方法については、[Advertising.com Dynamic Retargeter: マッピング]()の記事を参照してください。

### ベンダー文書

* [Advertising.com Dynamic Retargeterについて](https://www.advertising.com/advertiser/dynamic-retargeter)
* [Advertising.comのサポートと文書](http://help.advertising.com)
* [BuysightがAdvertising.com Dynamic Retargeterにブランド変更](https://www.advertising.com/tags/dynamic-retargeter)

[マッピングの構成方法](/ja/iq-tag-management/data-mappings/manage/)

[ロードルールの構成方法]()