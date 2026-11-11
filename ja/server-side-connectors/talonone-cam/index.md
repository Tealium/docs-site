---
title: Talon.One Campaign Audience Managerコネクタ構成ガイド
description: この記事では、Talon.One Campaign Audience Managerコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/talonone-cam/
---
## API情報

このコネクタでは、次のベンダーAPIを使用します。

* API名：サードパーティAPI
* APIバージョン：v1
* APIエンドポイント：`https://integration.talon.one/cdp/`
* ドキュメント：[Talon.OneサードパーティAPI：顧客データプラットフォーム](https://docs.talon.one/third-party-api#tag/Customer-data-platforms)

## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| 顧客プロファイルを更新 | ✓ | ✗ |

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の構成を構成します。

### APIキー

（必須）Campaign Managerソフトウェア内で生成されたAPIキー。

Campaign ManagerでAPIキーを生成するには、次の手順を実行します。

1. Campaign Managerにログインし、任意の**アプリケーション*を開くか、新しく作成します。
1. **Settings > Developer settings**に移動します。
1. **Create API Key**をクリックします。
1. キーのタイトルを入力します。
1. **Do you want to use this API Key with a 3rd party service?**で、**Yes**を選択します。
1. 連携するプラットフォームを選択します。
1. キーの有効期限を構成します。
1. **Create API Key**をクリックします。

### Management APIキー

（必須）Management APIキーを使用すると、キーを作成した管理者が選択したエンドポイントにアクセスできます。

Management APIキーを生成するには、次の手順を実行します。

1. Campaign Managerにログインします。
1. **Account > Management API keys**に移動します。
1. **Create Key**をクリックします。
1. キーの名前を入力します。
1. キーの有効期限を構成します。
1. キーからアクセスできるように、**`/v1/audiences` (GET)**および**`/v1/attributes` (POST, GET)**エンドポイントを選択します。
1. **Create Key**をクリックします。

### ベースURL

（必須）Talon.OneデプロイメントのベースURL。URLにHTTP(S)プロトコルを含めないでください。例：`mycompany.europe-west1.talon.one`。

## アクション構成 — パラメータとオプション

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### アクション — 顧客プロファイルを更新

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| 顧客プロファイルID | 顧客プロファイルの連携ID。これは訪問に適用される一意の識別子です。Tealium内で関連付けられた訪問IDを使用してください。メールアドレスは使用しないことを推奨します。このフィールドがマッピングされていない場合、Tealium訪問IDに自動的にマッピングされます。 |
| ルールエンジンを実行 | ルールエンジンを実行するかどうかを指定します。<ul><li>`true`の場合、ルールが実行され、その効果が適用されます。オーディエンスの変更も適用されます。</li><li>`false`の場合、ルールは実行されず、応答時間が短縮されます。また、オーディエンスの変更は適用されません。</li></ul> |
| 顧客プロファイル属性 | 任意の属性を任意の値に構成します。<ul><li>新しい属性は自動的に作成されます。</li><li>カスタム属性と有効な組み込み属性が表示されます。その他の組み込み属性は、最初に属性ライブラリで有効にする必要があります。</li></ul> |
| 追加するオーディエンス | 顧客が参加するオーディエンスのID。 |
| 削除するオーディエンス | 顧客が離脱するオーディエンスのID。 |
| テンプレート変数 | **テンプレート**のデータ入力としてテンプレート変数を指定します。<ul><li>ネストされたテンプレート変数の名前には、ドット記法を使用します（例：`items.name`）。</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から構築されます。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li></ul> |
| テンプレート | **顧客パラメータ**および**顧客プロファイル属性**セクションで参照するテンプレートを指定します。テンプレートは、サポート対象のフィールドに二重中括弧で名前を指定して挿入します。例：`{{SomeTemplateName}}`。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。 |