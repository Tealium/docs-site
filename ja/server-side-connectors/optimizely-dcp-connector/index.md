---
title: Optimizely DCP コネクタ構成ガイド
description: この記事では、Optimizely Dynamic Customer Profiles コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/optimizely-dcp-connector/
---
## API 情報

このコネクタは、次のベンダー API を使用します。

* API 名: Optimizely Dynamic Customer Profiles API
* API バージョン: v2
* API エンドポイント: `https://vis.optimizely.com/api/customer_profile`
* ドキュメント: [Optimizely Dynamic Customer Profiles API](https://docs.developers.optimizely.com/web-experimentation/docs/dcp#write-customer-profile)

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|顧客プロファイルを更新| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **API キー**: API キーを生成するには、[Optimizely Tokens API](http://app.optimizely.com/tokens) にアクセスしてください。詳細については、[Optimizely のドキュメント](http://developers.optimizely.com/classic/token)を参照してください。

## アクション構成 - パラメータとオプション

**続行**をクリックして、コネクタのアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - 顧客プロファイルを更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
| DCP サービス ID | DCP サービス ID の詳細については、[Optimizely：Dynamic Customer Profiles を使用したオーディエンスの作成](https://support.optimizely.com/hc/en-us/articles/4410289305357-Create-audiences-with-Dynamic-Customer-Profiles)を参照してください。 |
| DCP データソース ID | DCP データソース ID の詳細については、[Optimizely：Dynamic Customer Profiles を使用したオーディエンスの作成](https://help.optimizely.com/Target_Your_Visitors/Personalization%3A_Create_Audiences_with_Dynamic_Customer_Profiles)を参照してください。 |
| Optimizely 顧客 ID | Optimizely 顧客 ID の詳細については、[Optimizely：Dynamic Customer Profiles を使用したオーディエンスの作成](https://help.optimizely.com/Target_Your_Visitors/Personalization%3A_Create_Audiences_with_Dynamic_Customer_Profiles)を参照してください。ファーストパーティ Cookie に含まれる Optimizely エンドユーザー ID を使用することをお勧めします。 |
| 顧客プロファイル属性 | 顧客プロファイル属性は、データソース内における顧客プロファイルの一要素を表します。指定した属性値は、以前に指定された既存の値を上書きします。キーが登録済みの属性名に対応していない場合、または値が属性のデータ型や形式に準拠していない場合、書き込みは失敗します。 |