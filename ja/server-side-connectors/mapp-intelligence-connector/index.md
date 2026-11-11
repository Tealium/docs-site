---
title: Mapp Intelligence コネクタ（旧称 Webtrekk）セットアップガイド
description: この記事では、Mapp Intelligence コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/mapp-intelligence-connector/
---
## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|ピクセルを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を構成します。

* **トラッキングドメイン**
  * （必須）Mapp によって定義されます。例：` track.webtrekk.net`

* **Mapp Intelligence トラッキング ID**
  * （必須）Mapp によって定義されます。例：`111111111111111`

## アクション構成 - パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - ピクセルを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|クライアント時刻|
|色深度|
|コンテンツ ID|
|Cookie の有効化|
|Java の有効化|
|JavaScript の有効化|
|モニター解像度|
|参照元 URL|
|バージョン|
|ウィンドウサイズ|
|カスタム Ever-ID|
|Ever-ID|
|参照元|
|ユーザーエージェント|
|ユーザー IP|
|E コマース商品パラメータ|  <ul><li>配列およびリストの値を、Mapp に渡すキーにマッピングします。</li><li>すべての配列とリストは同じ長さにする必要があります。</li><li>単一値の属性は、値を繰り返すことで、他のすべての配列と同じ長さの配列に展開されます。</li><li>Webtrekk に送信できるパラメータの一覧については、[トラッキングパラメータと JavaScript キーの概要](https://docs.mapp.com/docs/which-parameters-can-be-sent-to-mapp-intelligence)を参照してください。</li></ul> |
|テンプレート変数|  <ul><li>メッセージデータ用のテンプレート変数を指定します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>ネストされたテンプレート変数には、ドット表記で名前を付けます。例：`items.name`。</li><li>ネストされたテンプレート変数は通常、データレイヤーのリスト属性から作成されます。</li></ul> |
|テンプレート|  <ul><li>（任意）クエリパラメータで参照するテンプレートを指定します。</li><li>詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。./li><li>テンプレートは、サポートされているフィールドに、二重波括弧で囲んだ名前を使用して挿入されます。例：`{{SomeTemplateName}}`。</li></ul> |