---
title: イベント属性とエンリッチメントの参照
description: この記事では、すべてのイベント属性とそれらのエンリッチメント、対応するルール条件を一覧表示します。
url: https://docs.tealium.com/ja/server-side/attributes/reference/event-attributes-and-enrichments-reference/
---
## 仕組み

この参照では、属性タイプに以下のアイコンを使用します：

|   |   |
| --- | --- |
|  [文字列](#string) |  [文字列の配列](#array-of-strings) |
|  [数値](#number) |   [数値の配列](#array-of-numbers)|
| [ブール値](#boolean) |   [ブール値の配列](#array-of-booleans)|
| [iQ属性](#iq-attribute-and-omnichannel-attribute) |  カスタム値|
| [日付](#date)|  [オムニチャネル日付](#omnichannel-date)|
| 実験モード|  ビジターID|
| オムニチャネル属性|  イベントレベル属性|

## 文字列

* イベントレベルの属性
* ウェブフックで使用可能
* 例：`A String`
* 詳細情報は、[文字列属性]()を参照してください。

#### エンリッチメント

|エンリッチメント| ソース値|
|---| ---|
|文字列を構成|  ![](/images/server-side/untitled-drawing-(1).png) |
|分割（ランダムに分布した値に割り当て）| |
|削除|
|小文字化|
|デリミタで結合|  ![](/images/server-side/untitled-drawing-(1).png) |
|文字列を日付に構成|   ![](/images/server-side/untitled-drawing-(1).png)|

#### ルール条件

|ルール条件| ソース値|
|---| ---|
|含む&lt;br&gt; 含む [大文字小文字を無視]&lt;br&gt; 含まない&lt;br&gt; 含まない [大文字小文字を無視]|    ![](/images/server-side/untitled-drawing-(1).png) |
|等しい &lt;br&gt; 等しい [大文字小文字を無視]&lt;br&gt; 等しくない&lt;br&gt; 等しくない [大文字小文字を無視]|    ![](/images/server-side/untitled-drawing-(1).png) |
|で始まる/で終わる&lt;br&gt; で始まる/で終わる [大文字小文字を無視]|    ![](/images/server-side/untitled-drawing-(1).png) |
|割り当てられている&lt;br&gt; 割り当てられていない|
|正規表現に一致| |

## 文字列の配列

* イベントレベルの属性
* ウェブフックで使用可能
* 例：`[&#34;Hello&#34;, &#34;&#34;, &#34;Mark&#34;]` (空の文字列はそのまま保存されます)
* 詳細については、[属性データタイプ：配列]()を参照してください。

#### エンリッチメント

|エンリッチメント| ソース値|
|---| ---|
|配列に文字列を追加|  ![](/images/server-side/untitled-drawing-(1).png) |
|文字列の配列を追加| ![](/images/server-side/untitled-drawing-(1).png)|
|他の2つの配列間の差を構成| ![](/images/server-side/untitled-drawing-(1).png)|
|リセット（すべての値を削除）|
|すべてのエントリを小文字にする|
|最初/最後/すべてのエントリを削除|  ![](/images/server-side/untitled-drawing-(1).png)|

#### ルール条件

|ルール条件| ソース値|
|---| ---|
|[部分文字列]を含む &lt;br&gt; [部分文字列]を含む [大文字小文字を無視]|      ![](/images/server-side/untitled-drawing-(1).png) |
|(キー)を含まない &lt;br&gt; (キー)を含まない [大文字小文字を無視]|     ![](/images/server-side/untitled-drawing-(1).png) |
|で始まる/で終わる&lt;br&gt; で始まる/で終わる [大文字小文字を無視]|     ![](/images/server-side/untitled-drawing-(1).png) |

## 数値

* イベントレベルの属性
* Webhookで使用可能
* 例：`1.001`、または`1001`、ただし`1,001`は不可
* 数値は小数または整数であることができます。整数は最も近い整数に切り上げまたは切り捨てられます。（実験モード）
* 詳細については、[数値属性]()を参照してください。

#### エンリッチメント

|エンリッチメント| ソース値|
|---| ---|
|増分/減分| ![](/images/server-side/untitled-drawing-(1).png)|
|比率/積/差/合計| ![](/images/server-side/untitled-drawing-(1).png)|
|数値を構成| ![](/images/server-side/untitled-drawing-(1).png)|
|数値の配列の集計（平均、最小、最大）| |
|配列内のアイテム数に構成| |

#### ルール条件

|ルール条件| ソース値|
|---| ---|
|等しい&lt;br&gt; 等しくない| ![](/images/server-side/untitled-drawing-(1).png)|
|割り当てられている&lt;br&gt; 割り当てられていない|
|以上&lt;br&gt; 以下|  ![](/images/server-side/untitled-drawing-(1).png) |

## 数値の配列

* イベントレベルの属性
* Webhookで使用可能
* 例：`[&#34;1&#34;, &#34;&#34;, &#34;3&#34;, &#34;4&#34;]`は`[1, 0, 3, 4]`を出力します
* 詳細については、[属性データタイプ：配列]()を参照してください。

#### エンリッチメント

|エンリッチメント| ソース値|
|---| ---|
|配列に数値を追加| ![](/images/server-side/untitled-drawing-(1).png)|
|数値の配列を追加| ![](/images/server-side/untitled-drawing-(1).png)|
|他の2つの配列間の差を構成する| ![](/images/server-side/untitled-drawing-(1).png)|
|リセット（すべての値を削除）|

#### ルール条件

|ルール条件| ソース値|
|---| ---|
|割り当てられている&lt;br&gt; 割り当てられていない| ![](/images/server-side/untitled-drawing-(1).png)|
|数値を含む| ![](/images/server-side/untitled-drawing-(1).png)|

## ブール値

* イベントレベルの属性
* ウェブフックで使用可能
* 例：`true`
* 詳細については、[ブール属性]()を参照してください。

#### エンリッチメント物

|エンリッチメント物| ソース値|
|---| ---|
|真/偽に構成する|

#### ルール条件

|ルール条件| ソース値|
|---| ---|
|真/偽である|

## ブール値の配列

* イベントレベルの属性
* ウェブフックで使用可能
* 例：`[true, false, true]` (引用符なし)
* 詳細については、[属性データタイプ：配列]()を参照してください。

#### エンリッチメント物

|エンリッチメント物| ソース値|
|---| ---|
|ブール値を追加する|  ![](/images/server-side/untitled-drawing-(1).png) |
|ブール値の配列を追加する| ![](/images/server-side/untitled-drawing-(1).png)|
|リセット（すべての値を削除）|

#### ルール条件

|ルール条件|
|---|
|ブール値を含む&lt;br&gt; ブール値のみを含む|  |
|割り当てられている&lt;br&gt; 割り当てられていない|  |

## 日付

* イベントレベルの属性
* ウェブフックで使用可能
* 入力形式は&#34;日付形式から変換&#34;のエンリッチメント物を使用して制御します。例えば、このエンリッチメント物が`ddMMYY`に構成されている場合、2020年12月31日の入力として`31122020`を渡します。
* 詳細については、[日付属性]()を参照してください。

#### エンリッチメント物

|エンリッチメント物| ソース値|
|---| ---|
|日付形式から変換&lt;br&gt; (イベント変数の入力に期待する日付形式を構成します。)|
|現在の日付に構成する|
|日付を構成する&lt;br&gt; (日付形式には&#34;xxx&#34;を使用します。)| |
|日付を構成する（日付形式から） | ![](/images/server-side/untitled-drawing-(1).png)|
|エポックミリ秒から日付を構成する。&lt;br&gt; (日付形式には&#34;xxx&#34;を使用します。)| ![](/images/server-side/untitled-drawing-(1).png) |

#### ルール条件

|ルール条件| ソース値|
|---| ---|
|以上&lt;br&gt; 以下&lt;br&gt; (現在の時間と直接比較するか、秒、分、時間、日、週、月で未来または過去の時間枠と比較できます。)| |
|割り当てられている&lt;br&gt; 割り当てられていない|

## iQ属性とオムニチャネル属性

* イベントレベルの属性
* ウェブフックで使用可能
* 任意のデータ形式
* オムニチャネル属性についての詳細は、[属性：オフラインデータ（オムニチャネル）]()を参照してください。

#### ルール条件

|ルール条件|
|---|
|含む&lt;br&gt; 含む [大文字小文字を無視]&lt;br&gt; 含まない&lt;br&gt; 含まない [大文字小文字を無視]|    ![](/images/server-side/untitled-drawing-(1).png) |
|配列に含まれる&lt;br&gt; 配列に含まれない|    ![](/images/server-side/untitled-drawing-(1).png) |
|等しい &lt;br&gt; 等しい [大文字小文字を無視]&lt;br&gt; 等しくない&lt;br&gt; 等しくない [大文字小文字を無視]|    ![](/images/server-side/untitled-drawing-(1).png) |
|で始まる/で終わる&lt;br&gt; で始まる/で終わる [大文字小文字を無視]|    ![](/images/server-side/untitled-drawing-(1).png) |
|より小さい | 以上|    ![](/images/server-side/untitled-drawing-(1).png) |
|割り当てられている&lt;br&gt; 割り当てられていない|
|空である&lt;br&gt; 空でない|

## オムニチャネル日付

* イベントレベルの属性
* Webhookで使用可能
* Java Simple Date Formatを使用
* オムニチャネル属性についての詳細は、[属性: オフラインデータ (オムニチャネル)]()を参照してください。

#### ルール条件

|ルール条件| ソース値|
|---| ---|
|以上&lt;br&gt; 以下| |
|割り当てられている&lt;br&gt; 割り当てられていない|
|X分、時間、日、週、月前に発生した/発生していない| |