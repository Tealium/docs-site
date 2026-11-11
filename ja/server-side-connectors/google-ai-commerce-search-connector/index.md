---
title: Google AI Commerce Search コネクタ構成ガイド
description: 旧称 Vertex AI Search for Commerce の AI Commerce Search は、e コマース体験向けに Google 品質の検索、閲覧、レコメンデーションを提供します。
url: https://docs.tealium.com/ja/server-side-connectors/google-ai-commerce-search-connector/
---
## API 情報

このコネクタは、次のベンダー API を使用します。

* API 名：Google API
* API バージョン：v2
* API エンドポイント：`https://retail.googleapis.com`
* ドキュメント：[AI Commerce Search](https://docs.cloud.google.com/gemini-enterprise-cx/ai-commerce-search/reference/rest)

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **Google Cloud Platform プロジェクト ID**：（必須）AI Commerce Search が有効になっている Google Cloud プロジェクト ID。
* **秘密鍵 JSON ファイル**：（必須）サービスアカウント用に生成された JSON キーを貼り付けます。サービスアカウントには、`retail.userEvents.create`および`retail.catalogs.list`権限が必要です。Google は、両方の権限を含む Retail Editor ロールの使用を推奨しています。

コネクタを構成したら、**完了**をクリックします。

## アクション

| アクション名 | ビジタープロファイル | イベントデータ |
| --- | :---: | :---: |
| ユーザーイベントを書き込む | ✗ | ✓ |

アクションの名前を入力し、アクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションを構成する方法について説明します。

### ユーザーイベントを書き込む

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| カタログ | ユーザーイベントを記録する AI Commerce Search カタログを選択します。 |
| イベントタイプ | AI Commerce Search に送信するユーザーイベントのタイプを選択します。これにより、イベントの解釈方法とペイロードで必須となるフィールドが決まります。<ul><li>`add-to-cart`</li><li>`remove-from-cart`</li><li>`category-page-view`</li><li>`detail-page-view`</li><li>`home-page-view`</li><li>`purchase-complete`</li><li>`search`</li><li>`shopping-cart-page-view`</li></ul>|

#### イベントデータ

| パラメータ | 説明 |
| --- | --- |
| 属性 | レコメンデーションモデルに含める追加のユーザーイベント機能をマッピングします。 |
| テンプレート変数 | <ul><li>（任意）テンプレートのデータ入力としてテンプレート変数を指定します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数には、ドット表記で名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から構築されます。</li></ul> |
| テンプレート | <ul><li>（任意）URL、URL パラメータ、ヘッダー、または本文データで参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、サポートされているフィールドに二重波括弧で名前を指定して挿入します。例：`{{SomeTemplateName}}`</li><li>OAuth を使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されたトークンを参照します。</li></ul> |