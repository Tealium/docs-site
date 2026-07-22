---
title: Oracle Infinity Analytics コネクタ構成ガイド
description: この記事では、Oracle Infinity Analyticsコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/oracle-infinity-analytics-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Oracle Infinity Analytics Data Collection API
* APIバージョン：v3
* APIエンドポイント：`https://dc.oracleinfinity.io`
* ドキュメンテーション：[Oracle Infinity Analytics Data Collection API](https://docs.oracle.com/en/cloud/saas/marketing/infinity-user/Help/data_collection/dcapi.htm)

### コネクタアクション

| **アクション名** | **AudienceStream** | **EventStream** |
|:----------------|:-------------------|:----------------|
| イベント送信      | ✓                  | ✓               |

### 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **アカウントGUID**
  * **Oracle Infinity**ユーザーインターフェースに表示されるアカウントGUID。
  * 詳細については、[Oracle Infinity Analytics Data collection API documentation](https://docs.oracle.com/en/cloud/saas/marketing/infinity-user/Help/data_collection/dcapi.htm)を参照してください。

### アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

#### アクション - イベント送信

##### パラメータ

| **パラメータ**                | **説明**                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|:-----------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| URI Stem                     | <ul><li>必須</li><li>URLのホストとポートの後、クエリストリングの前に表示されるURIステム。</li><li>通常はユーザーがアクセスした要求ファイルやページ。</li></ul>                                                                                                                                                                                                                              |
| イベントの種類                | <ul><li>必須</li><li>追跡するイベントの種類を示す数値識別子を指定します。これはイベントレベルのフィルタリングとレポートに使用されます。</li></ul>                                                                                                                                                                                                                                                                                           |
| ビジターID                   | <ul><li>必須</li><li>ビジターIDとして使用され、ファーストパーティクッキーに保存されるランダムな値。</li></ul>                                                                                                                                                                                                                                                                                                                                           |
| Unix Time Stamp              | <ul><li>ビジターIDとして使用され、ファーストパーティクッキーに保存されるランダムな値。</li></ul>                                                                                                                                                                                                                                                                                                                                                            |
| 訪問したドメイン               | <ul><li>ウェブサイトから送信された場合は必須。</li><li>訪問したドメイン、例えば `http://www.example.com`。</li></ul>                                                                                                                                                                                                                                                                                                                                   |
| カスタムビジターID            | <ul><li>他のシステムで訪問に割り当てることができる一意のカスタムビジターIDを識別します。</li><li>これはOracle Infinityタグによって送信される自動生成されたビジターIDパラメータとは別のものです。</li><li>カスタム値を送信しない場合、このパラメータは"ヒット"に存在しません。</li></ul>                                                                                                     |
| カスタムイベントデータ（アドバンス） | <ul><li>データ収集に渡すことができる可能性のあるパラメータの説明については、[parameter reference](https://docs.oracle.com/en/cloud/saas/marketing/infinity-user/Help/parameters/reference.htm)を参照してください。</li><li>送信されるイベントに追加するキー値ペアを指定します。</li><li>キー値ペアはチェックやフォーマットなしで"そのまま"追加されます。</li><li>配列要素はセミコロン(`;`)で結合されます。</li></ul> |
