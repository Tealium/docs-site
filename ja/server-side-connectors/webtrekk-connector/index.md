---
title: Webtrekkコネクタ構成ガイド
description: この記事では、Userlistコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/webtrekk-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ピクセルを送信| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法の一般的な指示については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **トラックドメイン**
  * 必須。
  * Webtrekkによって定義されます。例：` track.webtrekk.net`

* **WebtrekkトラッキングID**
  * 必須。
  * Webtrekkによって定義されます。例：`111111111111111`

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ピクセルを送信

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|クライアント時間|
|カラーデプス|
|コンテンツID|
|クッキー有効|
|Java有効|
|Javascript有効|
|モニター解像度|
|リファラーURL|
|バージョン|
|ウィンドウサイズ|
|カスタムEver-ID|
|Ever-ID|
|リファラー|
|ユーザーエージェント|
|ユーザーIP|
|E-コマース製品パラメータ|  <ul><li>Webtrekkに渡すためのキーに配列とリストの値をマップします。</li><li>すべての配列とリストは同じ長さであるべきです。</li><li>単一値の属性は、値を繰り返す他のすべての配列と同じ長さの配列に展開されます。</li><li>Webtrekkに送信できるパラメータのリストについては。</li><li>[Webtrekkに送信できるパラメータ](https://support.webtrekk.com/hc/en-us/articles/360000061559-Which-parameters-can-be-sent-to-Webtrekk-)を参照してください。</li></ul> |
|テンプレート変数|  <ul><li>メッセージデータのテンプレート変数を提供します。</li><li>参照：[テンプレート変数ガイド](https://docs.tealium.com/connector-template-variables/)</li><li>ドット表記法でネストしたテンプレート変数を名付けます。例：`items.name`。</li><li>ネストしたテンプレート変数は通常、データレイヤーリスト属性から構築されます</li></ul> |
|テンプレート|  <ul><li>オプション：クエリパラメータで参照されるテンプレートを提供します。</li><li>参照：[テンプレートガイド](https://docs.tealium.com/about-connector-templates/)</li><li>テンプレートは、例：`{{SomeTemplateName}}`のように、サポートされるフィールドに名前で注入されます。</li></ul> |
