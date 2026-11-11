---
title: StackAdapt Eventsコネクタ構成ガイド
description: この記事では、StackAdapt Eventsコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/stackadapt-events-connector/
---
## API情報

このコネクタは、次のベンダーAPIを使用します。

* API名：StackAdapt API
* APIエンドポイント：`https://tags.srv.stackadapt.com`
* ドキュメント：[StackAdapt API](https://docs.stackadapt.com)

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の項目を構成します。
* **ピクセルID**  

コネクタを構成したら、**完了**をクリックします。
StackAdapt Universal Pixel IDです。

## アクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
| イベントを送信 | ✗ | ✓ |

アクションの名前を入力し、ドロップダウンメニューからアクションタイプを選択します。

次のセクションでは、各アクションのパラメーターとオプションを構成する方法について説明します。

### イベントを送信

#### パラメーター

| **パラメーター** | **説明** |
| --- | --- |
| イベント引数 | イベントアクションを指定する`JSON`オブジェクト。ピクセルルールの照合やデータのポストバックに使用できます。データのポストバックとは、キャンペーン収益や注文IDなどの補足データをStackAdaptに送信するプロセスです。 |
| ページタイトル | ページのタイトル。 |
| URL | 対象Webサイトの`URL`。 |
| ユーザーエージェント | ピクセルサーバーに送信されるイベントをトリガーしたユーザーのWebブラウザーのユーザーエージェント。ユーザープロファイルに必要です。 |
| ユーザーIP | ピクセルサーバーに送信されるイベントをトリガーしたユーザーの`IP`アドレス。 |
| テンプレート変数 | テンプレートのデータ入力としてテンプレート変数を指定します。詳細については、[テンプレート変数ガイド](https://docs.tealium.com/connector-template-variables/)を参照してください。ネストされたテンプレート変数には、ドット表記を使用して名前を付けます。例：`items.name`。ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。 |
| テンプレート | URL、URLパラメーター、ヘッダー、または本文データで参照するテンプレートを指定します。詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。テンプレートは、サポートされているフィールドに二重波括弧で名前を指定して挿入します。例：`{{SomeTemplateName}}`。OAuthを使用する場合、テンプレート変数`{{webhook_access_token}}`は認証リクエストによって返されたトークンを参照します。 |