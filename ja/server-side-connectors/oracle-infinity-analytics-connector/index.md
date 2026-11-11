---
title: Oracle Infinity Analytics コネクタ構成ガイド
description: この記事では、Oracle Infinity Analytics コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/oracle-infinity-analytics-connector/
---
## API 情報

このコネクタは、次のベンダー API を使用します。

* API 名：Oracle Infinity Analytics Data Collection API
* API バージョン：v3
* API エンドポイント：`https://dc.oracleinfinity.io`
* ドキュメント：[Oracle Infinity Analytics Data Collection API](https://docs.oracle.com/en/cloud/saas/marketing/infinity-user/Help/data_collection/dcapi.htm)

### コネクタアクション

| **アクション名** | **訪問プロファイル** | **イベントデータ** |
|:----------------|:-------------------|:----------------|
| イベントを送信      | ✓                  | ✓               |

### 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **アカウント GUID**
  * **Oracle Infinity** ユーザーインターフェイスに表示されるアカウント GUID。
  * 詳細については、[Oracle Infinity Analytics Data Collection API ドキュメント](https://docs.oracle.com/en/cloud/saas/marketing/infinity-user/Help/data_collection/dcapi.htm)を参照してください。

### アクション構成 — パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

#### アクション — イベントを送信

##### パラメータ

| **パラメータ**                | **説明**                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|:-----------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| URI ステム                     | <ul><li>（必須）URI ステムは、URL のホストとポートの後、クエリ文字列の前にある部分です。</li><li>通常は、ユーザーがアクセスしたファイルまたはページです。</li></ul>                                                                                                                                                                                                                              |
| イベントの種類                | <ul><li>（必須）追跡するイベントの種類を表す数値識別子を指定します。この識別子は、イベントレベルのフィルタリングとレポートに使用されます。</li></ul>                                                                                                                                                                                                                                                                                           |
| 訪問 ID                   | <ul><li>（必須）訪問 ID として使用され、ファーストパーティ Cookie に保存されるランダムな値です。</li></ul>                                                                                                                                                                                                                                                                                                                                           |
| Unix タイムスタンプ              | <ul><li>訪問 ID として使用され、ファーストパーティ Cookie に保存されるランダムな値です。</li></ul>                                                                                                                                                                                                                                                                                                                                                            |
| 訪問先ドメイン               | <ul><li>Web サイトから送信する場合は必須です。</li><li>`http://www.example.com` などの訪問先ドメインです。</li></ul>                                                                                                                                                                                                                                                                                                                                   |
| カスタム訪問 ID            | <ul><li>他のシステムで訪問に割り当てることができる、オプションの一意なカスタム訪問 ID を識別します。</li><li>これは、Oracle Infinity タグによって送信される、自動生成された訪問 ID パラメータとは別のものです。</li><li>カスタム値を送信しない場合、このパラメータは「ヒット」に含まれません。</li></ul>                                                                                                     |
| カスタムイベントデータ（詳細構成） | <ul><li>データ収集に渡すことができるパラメータの説明については、[パラメータリファレンス](https://docs.oracle.com/en/cloud/saas/marketing/infinity-user/Help/parameters/reference.htm)を参照してください。</li><li>送信するイベントに追加するキーと値のペアを指定します。</li><li>キーと値のペアは、チェックや書式構成を行わず「そのまま」追加されます。</li><li>配列要素はセミコロン（`;`）区切りで結合されます。</li></ul> |