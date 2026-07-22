---
title: StackAdapt イベントコネクタ構成ガイド
description: この記事では、StackAdapt イベントコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/stackadapt-events-connector/
---
## API 情報

このコネクタは以下のベンダー API を使用します：

* API 名：StackAdapt API
* API エンドポイント：`https://tags.srv.stackadapt.com`
* ドキュメント：[StackAdapt API](https://docs.stackadapt.com)

## 構成

コネクタマーケットプレイスにアクセスして新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の構成を構成します：
* **Pixel ID**  
StackAdapt ユニバーサルピクセル ID。

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| イベント送信 | ✗ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### イベント送信

#### パラメータ

| **パラメータ** | **説明** |
| --- | --- |
| イベント引数 | イベントアクションを指定する `JSON` オブジェクト。ピクセルルールのマッチングやデータパスバックに使用できます。データパスバックは、キャンペーン収益や注文IDなどの補足データをStackAdaptに送信するプロセスです。 |
| ページタイトル | ページのタイトル。 |
| URL | 対象ウェブサイトの `URL`。 |
| ユーザーエージェント | イベントをトリガーしたユーザーのウェブブラウザユーザーエージェント。ユーザープロファイルに必要です。 |
| ユーザー IP | イベントをトリガーしたユーザーの `IP` アドレス。 |
| テンプレート変数 | テンプレートでのデータ入力用にテンプレート変数を提供します。詳細については、[テンプレート変数ガイド](https://docs.tealium.com/connector-template-variables/)を参照してください。ドット表記を使用してネストされたテンプレート変数を名付けます。例えば、`items.name`。ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます。 |
| テンプレート | URL、URLパラメータ、ヘッダー、またはボディデータで参照されるテンプレートを提供します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。テンプレートは、サポートされるフィールドに名前で二重中括弧で挿入されます。例えば、`{{SomeTemplateName}}`。OAuthを使用する場合、テンプレート変数 `{{webhook_access_token}}` は認証リクエストによって返されるトークンを指します。