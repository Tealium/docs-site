---
title: Mapp Intelligence コネクター（以前の名称：Webtrekk）構成ガイド
description: この記事では、Mapp Intelligence コネクターの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/mapp-intelligence-connector/
---
## コネクターアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ピクセルを送信| ✓| ✓|

## 構成の構成

コネクターマーケットプレイスにアクセスし、新しいコネクターを追加します。コネクターを追加する一般的な手順については、[コネクター概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクターを追加した後、以下の構成を構成します：

* **トラックドメイン**
  * 必須。
  * Mappによって定義されます。例：`track.webtrekk.net`

* **Mapp Intelligence トラッキングID**
  * 必須。
  * Mappによって定義されます。例：`111111111111111`

## アクション構成 - パラメーターとオプション

**次へ**をクリックするか、**アクション**タブに進みます。ここでコネクターアクションを構成します。

このセクションでは、各アクションのパラメーターとオプションの構成方法について説明します。

### アクション - ピクセルを送信

#### パラメーター

|**パラメーター**| **説明**|
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
|Eコマース製品パラメーター|  <ul><li>Mappに渡すためのキーに配列とリストの値をマッピングします。</li><li>すべての配列とリストは同じ長さである必要があります。</li><li>単一値属性は、他のすべての配列と同じ長さの配列に展開され、値が繰り返されます。</li><li>Webtrekkに送信できるパラメーターのリストについては、[トラッキングパラメーターとJavaScriptキーの概要](https://docs.mapp.com/docs/which-parameters-can-be-sent-to-mapp-intelligence)を参照してください。</li></ul> |
|テンプレート変数|  <ul><li>メッセージデータのテンプレート変数を提供します。</li><li>詳細については、[connector-template-variables](https://docs.tealium.com/connector-template-variables/)を参照してください。</li><li>例：`items.name`のようにドット表記でネストされたテンプレート変数を名前付けします。</li><li>ネストされたテンプレート変数は通常、データレイヤーリスト属性から構築されます</li></ul> |
|テンプレート|  <ul><li>オプション：クエリパラメーターで参照されるテンプレートを提供します。</li><li>詳細については、[about-connector-templates](https://docs.tealium.com/about-connector-templates/)を参照してください。</li><li>テンプレートは、例えば`{{SomeTemplateName}}`のように、サポートされるフィールドに名前で注入されます。</li></ul> |
