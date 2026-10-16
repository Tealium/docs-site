---
title: ロードルールについて
description: この記事では、ロードルールの追加と管理についての情報を提供します。ロードルールは、タグをロードするタイミングと場所を定義する条件です。
url: https://docs.tealium.com/ja/iq-tag-management/load-rules/about/
---
ロードルールは、サイトやアプリでタグがロードされるタイミングを決定します。ロードルールは、データレイヤーの値に基づいた1つ以上の条件です。たとえば、検索ページを識別するロードルール条件は次のようになります：


[
  [
    {
      "input": "page_type",
      "operator": "equals",
      "filter": "search"
    }
  ]  
]


デフォルトのロードルールは**すべてのページ**で、条件を含まず、常に真です。

ロードルールを使用するコンポーネントは以下の通りです：

* タグ
* イベント
* 同意管理者
* 通貨変換拡張機能
* チャネル拡張機能

## ブール論理

複数の条件をブール論理を使用して組み合わせることで、より複雑なロードルールを形成できます。たとえば、ユーザーがログインしている場合にのみ検索ページでタグをロードするためのロードルール条件は次のようになります：


[
  [
    {
      "input": "page_type",
      "operator": "equals",
      "filter": "search"
    },
    {
      "input": "is_logged_in",
      "operator": "equals",
      "filter": "1"
    }
  ]  
]


この複雑な論理は単一のルールに組み合わせることも、2つのルールとして作成し、**すべてのルールに一致**構成を使用して適用することもできます。タグにロードルールを割り当てる方法については[こちらを参照してください](https://docs.tealium.com/manage-load-rules/)。

#### AND論理

AND論理を使用して、すべての条件が真である場合にのみ真となるルールを作成します。たとえば、AND論理を使用して3つの条件を組み合わせたルールは、各個別の条件も真である場合にのみ真と評価されます。いずれかの条件が偽と評価される場合、ルール全体も偽と評価されます。

#### OR論理

OR論理を使用して、いずれかの条件が真である場合に真となるルールを作成します。たとえば、OR論理を使用して3つの条件を組み合わせたルールは、いずれかの個別の条件が真である場合に真と評価されます。OR論理を使用するルールは、すべての個別の条件が偽である場合にのみ偽と評価されます。

## 比較演算子のリスト

各ルール条件は比較演算子とデータレイヤーの変数を使用します。以下の表は、ロードルール条件で使用できる比較演算子をリストしています。名前に「(ignore case)」が含まれる演算子の場合、比較前に変数のテキスト値を小文字に変換します。

|**比較演算子**| **ページ上でタグがロードされるタイミング**|
|---| ---|
|`contains`<br> `contains (ignore case)`| 変数が指定された文字列を含んでいます。|
|`does not contain`<br> `does not contain (ignore case)`| 変数が指定された文字列を含んでいません。|
|`does not end with`<br> `does not end with (ignore case)`| 変数が指定された文字列で終わっていません。|
|`does not equal`<br> `does not equal (ignore case)`| 変数が指定された値と等しくありません。|
|`does not start with`<br> `does not start with (ignore case)`| 変数が指定された文字列で始まっていません。|
|`ends with`<br> `ends with (ignore case)`| 変数が指定された文字列で終わっています。|
|`equals`<br> `equals (ignore case)`| 変数が指定された値と等しいです。|
|`greater than`| 変数が指定された値より大きいです。|
|`greater than or equal to`| 変数が指定された値以上です。|
|`is badge assigned`| バッジが訪問に割り当てられています。<br> [データレイヤーのエンリッチメントの構成](https://docs.tealium.com/configure-data-layer-enrichment-iq/)で使用します。|
|`is badge not assigned`| バッジが訪問に割り当てられていません。<br> [データレイヤーのエンリッチメントの構成](https://docs.tealium.com/configure-data-layer-enrichment-iq/)で使用します。|
|`is defined`| 変数がデータレイヤーで定義されています。|
|`is not defined`| 変数がデータレイヤーで定義されていません。|
|`is populated`| 変数がデータレイヤーで定義され、空白または空ではありません。|
|`is not populated`| 変数がデータレイヤーで定義され、空白または空です。|
|`less than`| 変数が指定された値より小さいです。|
|`less than or equal to`| 変数が指定された値以下です。|
|`regular expression`| 変数が正規表現に一致します。|
|`starts with`<br> `starts with (ignore case)`| 変数が指定された文字列で始まります。 |

## ロードルールと同意の強制

既存のロードルールに同意条件を追加することは可能ですが、より信頼性の高い同意の強制を実現するために同意統合を使用することが必要な場合があります。

同意統合は、Tealium iQ管理機能であり、組織がクライアントサイドのデータ活性化プロセスに同意の強制を簡単に組み込むことを可能にします。ロードルールとは異なり、タグの発火をページビューやユーザーのインタラクションなどの条件に基づいて制御するのではなく、同意統合はデータ収集および処理活動中にユーザーの同意が尊重されることに専念します。詳細については、[同意統合について](https://docs.tealium.com/about-consent-integrations/)を参照してください。

同意の強制にロードルールを使用すると、次のような問題が発生する可能性があります：

* 初期イベントの見逃し
* データ漏洩
* サーバーサイドツールの完全なトリガーの困難

さらに、[`utag.track`](https://docs.tealium.com/platforms/javascript/track/)の呼び出しでタグIDのオプショナル配列(`uid_array`)を使用することで、ロードルールを尊重せずにタグを発火させることができます。同意条件とともにロードルール全体が無視される場合、`uid_array`パラメータを使用して同意の強制にロードルールを使用します。

ロードルールと同意統合についての詳細は、[ロードルールを超えて：コンプライアンスのための同意統合の活用](https://tealium.com/blog/data-governance-privacy/beyond-load-rules-leveraging-consent-integrations-for-compliance/)を参照してください。