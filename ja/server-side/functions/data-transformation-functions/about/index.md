---
title: データ変換機能について
description: この記事では、データ変換機能の概要を説明します。
url: https://docs.tealium.com/ja/server-side/functions/data-transformation-functions/about/
---
データ変換機能は、データがTealiumシステムに入力された時点で実行されますが、データが処理される前に行われます。変換機能は、以下を含むさまざまな目的に役立ちます：

* 関数に渡されたイベントオブジェクトをフラット化する。
* 電話番号やメールアドレスなどの機密データを削除する。
* イベントオブジェクト内の変数を変更する（例：変数を小文字に変更する）。
* 他の値に基づいてイベントオブジェクト内の変数を構成する。
* 変数の名前を変更し、値を別の変数に割り当てて元の変数を削除する。


<blockquote>
ファイルインポートイベントはデータ変換機能ではサポートされていません。
</blockquote>


## データ変換機能への入力

データ変換機能は、データのソースに応じて以下の入力パラメータのいずれかを持ちます：

* `event`: Tealium Collectからのイベントデータオブジェクト。詳細については、[イベントパラメータ]()を参照してください。
* `dataRecord`: クラウドデータソースからのデータレコード。詳細については、[データレコードオブジェクト](https://docs.tealium.com/about-data-record-functions/#data-record-object)を参照してください。


<blockquote>
Tealiumモジュールは、データ変換機能用に`flatten()`ユーティリティをエクスポートしており、ネストされたオブジェクトをネストなしの新しいオブジェクトに変換します。
</blockquote>


## カスタムトリガー

データ変換機能は、関数のカスタムトリガーに基づいて呼び出されます。カスタムトリガーは、関数を実行するタイミングを指定するために作成するルールです。カスタムトリガールールはロードルールに似ており、ルール内の条件を組み合わせるためにブール論理を使用します。

例えば、以下のルールでは、特定のデータソース（`r2rbm8`）からの`purchase`イベントが来たときに関数がトリガーされます。


[
  [
    {
      "input": "$.dataSourceId",
      "operator": "equals",
      "filter": "r2rbm8"
    },
    {
      "input": "$.data.udo.tealium_event",
      "operator": "equals",
      "filter": "purchase"
    }
  ] 
]


条件は、入力データオブジェクトのプロパティセレクタ、比較演算子、および比較値に基づいています。セレクタはJSONPath式です（[JSONPath](https://github.com/json-path/JsonPath)を参照）し、オブジェクト内の任意のプロパティを参照できます。

データ変換機能とカスタムトリガーの作成についての情報は、[関数の作成](https://docs.tealium.com/create-function/)を参照してください。


<blockquote>
イベントまたはデータレコードは1つの関数のみをトリガーできます。入力データが複数のトリガールールに一致する場合、最も古い**変更日**の関数がトリガーされます。
</blockquote>


### イベント用

Tealium Collectからのイベントの場合、カスタムトリガー条件は`event`パラメータの任意のプロパティに基づくことができますが、通常はデータソースキー、データソースプラットフォーム、および`tealium_event`属性に基づいています。

`event`パラメータについての詳細は、[イベントパラメータ](https://docs.tealium.com/transforms-event-parameter/)を参照してください。

### データレコード用

クラウドデータソースからのイベントの場合、カスタムトリガー条件は`dataRecord`パラメータの任意のプロパティに基づくことができますが、データソースキー(`$.dataSourceId`)に基づく条件を含める必要があります。

`dataRecord`パラメータについての詳細は、[データレコードオブジェクト](https://docs.tealium.com/about-data-record-functions/#data-record-object)を参照してください。

### ルールの制限

* **セレクタ**および**値**フィールドは128文字に制限されます。
* 正規表現演算子は使用できません。
* ルールのサイズは10 KBに制限されます。
* ORブロックの数は10に制限されます。
* ANDブロック内の条件数は10に制限されます。

## デフォルト関数コード

データ変換機能を作成すると、**コード**タブにデフォルトコードが表示されます。デフォルトコードは`flatten`ライブラリをインポートし、`transform(event)`を呼び出します。ここで`event`パラメータは入力イベントのメタデータオブジェクトであり、入力された`event`オブジェクトをフラット化します。必要に応じてデフォルトの`transform()`コードを変更して、`event.data.udo`オブジェクト内のイベント属性を変更します。

```js
import flatten from "tealium/util/flatten";
// "transform" function lets you access event and apply changes

transform((event) => {
    // changes are applied through the mutation of the original event
    event.data.udo = flatten(event.data.udo);
    console.log(JSON.stringify(event, null, 2));
})
```

データ変換機能の例については、[例コード]()を参照してください。

## 既存の関数をカスタムトリガーに変換

カスタムトリガーは、データ変換機能の初期リリース後に導入されました。カスタムトリガーが導入される前に存在していたデータ変換機能については、以下のような条件が自動的に作成されます：

![](https://docs.tealium.com/images/server-side/transfm-conversion-edit-cond.png)

この新しい条件は、関数に関連付けられたデータソースのIDに構成されたデータソースIDを指定します。データソースからのすべてのイベントに対して関数がトリガーされます。この条件を編集して、より具体的なイベントに対して関数をトリガーすることができます。