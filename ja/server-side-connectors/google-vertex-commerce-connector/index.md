---
title: Google Vertex AI Search for Commerce コネクタ構成ガイド
description: このコネクタを構成して、TealiumのイベントデータをGoogle Vertex AI Searchに送信し、パーソナライズされた直感的なショッピング体験を実現します。
url: https://docs.tealium.com/ja/server-side-connectors/google-vertex-commerce-connector/
---
## API情報

このコネクタは以下のベンダーAPIを使用します：

* API名：Google API
* APIバージョン：v2
* APIエンドポイント：`https://retail.googleapis.com`
* ドキュメント：[Vertex AI Search for commerce](https://cloud.google.com/solutions/vertex-ai-search-commerce)


## 構成

コネクタマーケットプレイスにアクセスし、新しいコネクタを追加します。コネクタの追加方法については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を行います：

* **Google Cloud PlatformプロジェクトID**：（必須）あなたのGoogle CloudプロジェクトID。プロジェクトはVertex Search AIを有効にしている必要があります。
* **プライベートキーJSONファイル**：（必須）サービスアカウント用に生成されたJSONキーを貼り付けます。サービスアカウントは`retail.userEvents.import`へのアクセスが必要です。GoogleはRetail Editorロールの使用を推奨します。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| ユーザーイベントの書き込み | ✗ | ✓ |

アクションの名前を入力し、アクションタイプを選択します。

以下のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### ユーザーイベントの書き込み

#### パラメータ

| パラメータ | 説明 |
| --- | --- |
| カタログ | Vertex AI Search for Commerceのカタログを選択し、ユーザーイベントが記録されます。 |
| イベントタイプ | Vertex AI Search for Commerceに送信するユーザーイベントのタイプを選択します。これにより、イベントの解釈方法とペイロードに必要なフィールドが決まります。<ul><li>`add-to-cart`</li><li>`remove-from-cart`</li><li>`category-page-view`</li><li>`detail-page-view`</li><li>`home-page-view`</li><li>`purchase-complete`</li><li>`search`</li><li>`shopping-cart-page-view`</li></ul>|

#### イベントデータ

| パラメータ | 説明 |
| --- | --- |
| 属性 | 推薦モデルに含める追加のユーザーイベント機能をマッピングします |
| テンプレート変数    | <ul><li>(オプション) テンプレートにデータ入力としてテンプレート変数を提供します。詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ドット表記を使用してネストされたテンプレート変数に名前を付けます。例：`items.name`</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。</li></ul>   |
| テンプレート             | <ul><li>(オプション) URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、サポートされるフィールドに名前で二重中括弧を使用して注入されます。例：`{{SomeTemplateName}}`。</li><li>OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されるトークンを指します。</li></ul> |
