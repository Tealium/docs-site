---
title: Optimizely DCP コネクタ設定ガイド
description: この記事では、Optimizely Dynamic Customer Profilesコネクタの設定方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/optimizely-dcp-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Optimizely Dynamic Customer Profiles API
* APIバージョン：v2
* APIエンドポイント：`https://vis.optimizely.com/api/customer_profile`
* ドキュメンテーション：[Optimizely Dynamic Customer Profiles API](https://docs.developers.optimizely.com/web-experimentation/docs/dcp#write-customer-profile)

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|顧客プロファイルの更新| ✓| ✓|

## 設定の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[About Connectors]()を参照してください。

コネクタを追加した後、以下の設定を構成します：

* **APIキー**：[Optimizely Tokens API](http://app.optimizely.com/tokens)にアクセスしてAPIキーを生成するか、[Optimizely documentation](http://developers.optimizely.com/classic/token)を参照して詳細情報を得てください。

## アクション設定 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの設定方法について説明します。

### アクション - 顧客プロファイルの更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
| DCPサービスID | DCPサービスIDについての詳細は、[Optimizely: Create Audiences with Dynamic Customer Profiles](https://support.optimizely.com/hc/en-us/articles/4410289305357-Create-audiences-with-Dynamic-Customer-Profiles)を参照してください。 |
| DCPデータソースID | DCPデータソースIDについての詳細は、[Optimizely: Create Audiences with Dynamic Customer Profiles](https://help.optimizely.com/Target_Your_Visitors/Personalization%3A_Create_Audiences_with_Dynamic_Customer_Profiles)を参照してください。 |
| Optimizely顧客ID | Optimizely顧客IDについての詳細は、[Optimizely: Create Audiences with Dynamic Customer Profiles](https://help.optimizely.com/Target_Your_Visitors/Personalization%3A_Create_Audiences_with_Dynamic_Customer_Profiles)を参照してください。OptimizelyエンドユーザーIDを第一パーティクッキーから使用することを推奨します。 |
| 顧客プロファイル属性 | 顧客プロファイル属性は、データソース内の顧客プロファイルの一部を説明します。指定された属性値は、以前に指定された既存の値を上書きします。キーが登録された属性名に対応していない場合や、値が属性のデータ型/形式を尊重していない場合、書き込みは失敗します。 |