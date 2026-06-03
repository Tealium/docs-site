---
title: ルール条件の定義
description: この記事では、オーディエンスとルールの条件を作成する際に利用可能な演算子を一覧で紹介します。
url: https://docs.tealium.com/ja/server-side/audiences/rule-conditions/
---

## 条件演算子

一部の演算子は特定の属性タイプにのみ適用されます。これは**適用対象**列で示されています。

|演算子| 説明| 適用対象|
|---| ---| ---|
|array contains|  配列内の項目が指定した値と完全に一致します。&lt;br&gt;&lt;br&gt;**真**&lt;br&gt; `[&#34;iOS&#34;, &#34;Android&#34;]` array contains &#34;Android&#34; &lt;br&gt;&lt;br&gt;**偽**&lt;br&gt; `[&#34;Women&#39;s Clothing&#34;, &#34;Shoes&#34;]` array contains &#34;Women&#34; |  配列 |
|array does not contain|  配列内の項目が指定した値と完全に一致しません。 &lt;br&gt;&lt;br&gt;**真**&lt;br&gt; `[&#34;iOS&#34;, &#34;Android&#34;]` array does not contain &#34;Samsung&#34; &lt;br&gt;&lt;br&gt;**偽**&lt;br&gt; `[&#34;Women&#39;s Clothing&#34;, &#34;Shoes&#34;]` array does not contain &#34;Shoes&#34; |  配列 |
|contains|  属性値が指定した値を含みます。 &lt;br&gt;&lt;br&gt;**真**&lt;br&gt; `&#34;user@tealium.com&#34;` contains &#34;tealium&#34;&lt;br&gt; `[&#34;iOS&#34;, &#34;Android&#34;]` array contains &#34;Android&#34; &lt;br&gt;&lt;br&gt;**偽**&lt;br&gt; `[&#34;Women&#39;s Clothing&#34;, &#34;Shoes&#34;]` array contains &#34;Women&#34; |  配列&lt;br&gt; 文字列&lt;br&gt; Tally&lt;br&gt; Visitor ID |
| contains&lt;br&gt; (ignore case) | 属性値が指定した値を含みます。|  文字列&lt;br&gt; Visitor ID |
|does not contain| 属性値が指定した値を含みません。|  配列&lt;br&gt; 文字列&lt;br&gt; Visitor ID&lt;br&gt; Tally |
| does not contain&lt;br&gt; (ignore case) | 属性値が指定した値を含みません。|  配列&lt;br&gt; 文字列&lt;br&gt; Visitor ID&lt;br&gt; Tally |
|contains partial string|  属性値が指定した値と部分的に一致します。 &lt;br&gt;&lt;br&gt;**真**&lt;br&gt; `[&#34;Women&#39;s Clothing&#34;, &#34;Shoes&#34;]` array contains &#34;Women&#34; &lt;br&gt;&lt;br&gt;**偽**&lt;br&gt; `[&#34;Women&#39;s Clothing&#34;, &#34;Shoes&#34;]` array contains &#34;Tops&#34; |  配列&lt;br&gt; Tally&lt;br&gt; Visitor ID |
| contains partial string&lt;br&gt; (ignore case) | 属性値が指定した値と部分的に一致します（大文字小文字を無視）。|  配列&lt;br&gt; Tally&lt;br&gt; Visitor ID |
|equals|  属性値が指定した全体の値と一致します。 &lt;br&gt;&lt;br&gt;**真**&lt;br&gt; `&#34;purchase&#34;` equals &#34;purchase&#34;&lt;br&gt;  equals 0 &lt;br&gt;&lt;br&gt;**偽**&lt;br&gt; `&#34;Luggage&#34;` equals &#34;luggage&#34;&lt;br&gt;  equals 1 |  数値&lt;br&gt; 文字列&lt;br&gt; Visitor ID |
| equals (ignore case) | 属性値が指定した全体の値と一致します。|  文字列&lt;br&gt; Visitor ID |
|does not equal| 属性値が指定した全体の値と一致しません。|  数値&lt;br&gt; 文字列&lt;br&gt; Visitor ID |
| does not equal (ignore case) | 属性値が指定した全体の値と一致しません。|  文字列&lt;br&gt; Visitor ID |
|less than| 属性値が指定した値より小さい。|  数値&lt;br&gt; 日付 |
|less than or equal to| 属性値が指定した値以下です。|  数値&lt;br&gt; 日付 |
|greater than| 属性値が指定した値を超えます。|  数値&lt;br&gt; 日付 |
|greater than or equal to| 属性値が指定した値以上です。|  数値&lt;br&gt; 日付 |
|is assigned|  属性が存在しますが、値があるかどうかは問いません。 &lt;br&gt;&lt;br&gt;**真**&lt;br&gt; `&#34;Shirts&#34;` is assigned &lt;br&gt;`[&#34;iOS&#34;, &#34;Android&#34;]` is assigned&lt;br&gt; `[]` is assigned &lt;br&gt;`&#34;&#34;` is assigned is assigned &lt;br&gt;`Is VIP` is assigned |  数値&lt;br&gt; タイムライン&lt;br&gt; リスト&lt;br&gt; バッジ&lt;br&gt; 文字列&lt;br&gt; Tally&lt;br&gt; Visitor ID&lt;br&gt; 日付 |
|is not assigned| 属性が存在しません。|  数値&lt;br&gt; タイムライン&lt;br&gt; リスト&lt;br&gt; バッジ&lt;br&gt; 文字列&lt;br&gt; Tally&lt;br&gt; 日付&lt;br&gt; Visitor ID |
|is empty|  Tealium iQ変数には値が含まれていません（例えば、値が未定義、null、または空文字列）。 &lt;br&gt;&lt;br&gt;**真**&lt;br&gt; `{ page_name : undefined }`&lt;br&gt; `{ page_name : null }`&lt;br&gt; `{ page_name : &#34;&#34; }`&lt;br&gt; `{ product_id : [] }` |  Tealium iQタグ管理からインポート |
|is not empty|  Tealium iQ変数には何らかの値が含まれています。例えば、1文字以上の文字列、値を持つ数値（`0`を含む）、または1つ以上の項目を持つ配列。 &lt;br&gt;&lt;br&gt;**真**&lt;br&gt; `{ page_name : &#34;Title&#34; }`&lt;br&gt; `{ page_num : 1 }`&lt;br&gt; `{ product_id : [&#34;WidgetXYZ&#34;] }` |  Tealium iQタグ管理からインポート |
|is true| ブール値が**真**に等しい。|  ブール |
|is false| ブール値が**偽**に等しい。|  ブール |
|occurred less than| 日付値が指定した分/時間/日/週/月を過ぎていません。|  日付 |
|occurred more than|  日付値が指定した分/時間/日/週/月を過ぎています。 |  日付 |
|is started| 訪問/訪問に対してファネルが開始されています。|  ファネル |
|is completed| 訪問/訪問に対してファネルが終了しています。|  ファネル |
|step completed| 訪問/訪問に対してステップが正常に完了しています。|  ファネル |
|step not completed| 訪問/訪問に対してステップが完了していません。|  ファネル |
|is executed| タグがページ上で正常に発火しています。| Tealium iQタグ管理プロファイル内のタグ|
|matches regex|  ルール、エンリッチメント、オーディエンスで正規表現（regex）を使用することを許可します。詳細については、[正規表現](#regular-expressions) を参照してください。  |  文字列 |

## Tally属性の拡張ルール条件の使用

`contains`演算子を使用して、[Tally]()属性のキーが特定の値を含むかどうかをチェックするルール条件を作成することができます。

この拡張ルール条件は、`contains`演算子を使用する場合にのみ利用可能です。

ルールにTally属性のキーとその値を含めるには、次の手順を実行します：

1. **Server-Side Tools &gt; Manage Rules**に移動します。
1. 新しいルールを追加するか、編集する既存のルールを選択します。
1. **Conditions**の下で、最初のドロップダウンリストからチェックしたいTally属性を選択します。
1. 次のドロップダウンリストで**contains**演算子を選択します。
1. 3つ目のドロップダウンリストで**Custom Value**を選択します。
1. Tally属性で期待するキー値を入力します。  
      ![](/images/server-side/tally-rule.png)

1. **Perform rule on value**をクリックし、指定したキーを評価するために使用したい演算子を選択します。
1. キーに対して評価したい値を指定します。属性を使用するか、カスタム値を入力することができます。
1. **Save**をクリックします。

## 正規表現

`matches regex`演算子は文字列属性にのみ利用可能です。文字列の一部が正規表現（regex）と一致すると、条件は`true`を返します。 

ルール条件に正規表現をスラッシュ(`/`)なしで入力します。例えば、値が`abc1234567890`の場合、全体の文字列に一致するために`^[a-z0-9]{13}$`を入力します。


![](/images/server-side/audiences/regex_example_ui.png)

`matches regex`演算子には2つのオプションがあります：

* **Multiline Mode**:  
全体の文字列の始まりや終わりだけでなく、属性値の文字列内の任意の行の始まりや終わりで`^`と`$`を一致させます。
* **Case Insensitive**:  
文字列を属性値と比較する際に、大文字小文字を無視します。

以下の正規表現は、例の値`abc1234567890`に対するさまざまな一般的な文字列修飾子の戻り値を示しています：

|正規表現|戻り値|説明|
|-----|------------|-----------|
|`\d{3}`|`true`|境界修飾子なし、文字列内のどこでも一致します。|
|`^abc`|`true`|文字列の開始修飾子(`^`)は文字列の開始部分で一致します。|
|`\d{3}$`|`true`|文字列の終了修飾子(`$`)は文字列の終了部分で一致します。|
|`^[a-z0-9]{13}$`|`true`|開始と終了修飾子は全体の文字列で一致します。|
|`^[a-zA-Z]{4}`|`false`|文字列の開始修飾子：4つの連続した大文字または小文字が一致しません。|
|`[a-zA-Z]{4}$`|`false`|文字列の終了修飾子：文字列の終わりに文字がありません。|
|`^[a-z0-9]{15}$`|`false`|開始と終了修飾子：15文字の値が必要ですが、存在しません。|
