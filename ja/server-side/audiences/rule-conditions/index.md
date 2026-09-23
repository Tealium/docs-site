---
title: ルール条件定義
description: この記事では、オーディエンスとルールの条件を構築する際に使用できる演算子を一覧表示します。
url: https://docs.tealium.com/ja/server-side/audiences/rule-conditions/
---
## 条件演算子


<blockquote>
一部の演算子は、**適用対象**列で示されている特定の属性タイプにのみ適用されます。
</blockquote>


|演算子| 説明| 適用対象|
|---| ---| ---|
|array contains| 配列内のアイテムが指定した値と正確に一致します。<br><br>**True**<br> `["iOS", "Android"]` array contains "Android" <br><br>**False**<br> `["Women's Clothing", "Shoes"]` array contains "Women" |  配列 |
|array does not contain| 配列内のどのアイテムも指定した値と正確に一致しません。<br><br>**True**<br> `["iOS", "Android"]` array does not contain "Samsung" <br><br>**False**<br> `["Women's Clothing", "Shoes"]` array does not contain "Shoes" |  配列 |
|contains| 属性値が指定した値を含みます。<br><br>**True**<br> `"user@tealium.com"` contains "tealium"<br> `["iOS", "Android"]` array contains "Android" <br><br>**False**<br> `["Women's Clothing", "Shoes"]` array contains "Women" |  配列<br> 文字列<br> 集計<br> 訪問ID |
| contains<br> (ignore case) | 属性値が指定した値を含みます。|  文字列<br> 訪問ID |
|does not contain| 属性値が指定した値を含みません。|  配列<br> 文字列<br> 訪問ID<br> 集計 |
| does not contain<br> (ignore case) | 属性値が指定した値を含みません。|  配列<br> 文字列<br> 訪問ID<br> 集計 |
|contains partial string| 属性値が指定した値と部分的に一致します。<br><br>**True**<br> `["Women's Clothing", "Shoes"]` array contains "Women" <br><br>**False**<br> `["Women's Clothing", "Shoes"]` array contains "Tops" |  配列<br> 集計<br> 訪問ID |
| contains partial string<br> (ignore case) | 属性値が指定した値と部分的に一致します。|  配列<br> 集計<br> 訪問ID |
|equals| 属性値が指定した全体の値と一致します。<br><br>**True**<br> `"purchase"` equals "purchase"<br>  equals 0 <br><br>**False**<br> `"Luggage"` equals "luggage"<br>  equals 1 |  数値<br> 文字列<br> 訪問ID |
| equals (ignore case) | 属性値が指定した全体の値と一致します。|  文字列<br> 訪問ID |
|does not equal| 属性値が指定した全体の値と一致しません。|  数値<br> 文字列<br> 訪問ID |
| does not equal (ignore case) | 属性値が指定した全体の値と一致しません。|  文字列<br> 訪問ID |
|less than| 属性値が指定した値より小さいです。|  数値<br> 日付 |
|less than or equal to| 属性値が指定した値以下です。|  数値<br> 日付 |
|greater than| 属性値が指定した値を超えています。|  数値<br> 日付 |
|greater than or equal to| 属性値が指定した値以上です。|  数値<br> 日付 |
|is assigned| 属性が存在しますが、値があるかどうかは不明です。<br><br>**True**<br> `"Shirts"` is assigned <br>`["iOS", "Android"]` is assigned<br> `[]` is assigned <br>`""` is assigned is assigned <br>`Is VIP` is assigned |  数値<br> タイムライン<br> リスト<br> バッジ<br> 文字列<br> 集計<br> 訪問ID<br> 日付 |
|is not assigned| 属性が存在しません。|  数値<br> タイムライン<br> リスト<br> バッジ<br> 文字列<br> 集計<br> 日付<br> 訪問ID |
|is empty| Tealium iQ変数に値が含まれていません（例：値がundefined、null、または空文字列の場合）。<br><br>**True**<br> `{ page_name : undefined }`<br> `{ page_name : null }`<br> `{ page_name : "" }`<br> `{ product_id : [] }` |  Tealium iQタグ管理からインポート |
|is not empty| Tealium iQ変数に値が含まれています。例えば、1文字以上の文字列、値を持つ数値（`0`を含む）、または1つ以上のアイテムを含む配列など。<br><br>**True**<br> `{ page_name : "Title" }`<br> `{ page_num : 1 }`<br> `{ product_id : ["WidgetXYZ"] }` |  Tealium iQタグ管理からインポート |
|is true| Boolean値が**True**と等しいです。|  Boolean |
|is false| Boolean値が**False**と等しいです。|  Boolean |
|occurred less than| 日付値が指定した分/時間/日/週/月より前です。|  日付 |
|occurred more than|  日付値が指定した分/時間/日/週/月を過ぎています。 |  日付 |
|is started| 訪問/訪問に対してファネルが開始されました。|  ファネル |
|is completed| 訪問/訪問に対してファネルが終了しました。|  ファネル |
|step completed| 訪問/訪問に対してステップが成功裏に完了しました。|  ファネル |
|step not completed| 訪問/訪問に対してステップが完了していません。|  ファネル |
|is executed| ページ上でタグが正常に発火しました。| Tealium iQタグ管理プロファイル内のタグ|
|matches regex| ルール、エンリッチメント、オーディエンスで正規表現（regex）を使用できます。詳細は[正規表現](#regular-expressions)を参照してください。|  文字列 |

## 除外条件での未割り当て属性

**除外**条件で使用される属性が未割り当ての場合、結果は演算子によって異なります。

| 演算子                       | 結果  | 訪問の結果 |
| ------------------------------ | ------- | --------------- |
| array does not contain         | `true`  | 保持        |
| does not contain               | `true`  | 保持        |
| does not contain (ignore case) | `true`  | 保持        |
| does not equal                 | `true`  | 保持        |
| does not equal (ignore case)   | `true`  | 保持        |
| is not assigned                | `true`  | 保持        |
| step not completed             | `true`  | 保持        |
| contains                       | `false` | 除外        |
| contains (ignore case)         | `false` | 除外        |
| array contains                 | `false` | 除外        |
| equals                         | `false` | 除外        |
| equals (ignore case)           | `false` | 除外        |
| is assigned                    | `false` | 除外        |
| step completed                 | `false` | 除外        |
| is completed                   | `false` | 除外        |

### 数値属性

数値属性は未割り当ての値を異なる方法で処理します。比較の最初のオペランドが未割り当ての数値属性の場合、Tealiumはその値を`0.0`として評価します。

例えば：

* `equals 0`は`true`と評価されます。
* 他の数値比較は属性を`0.0`と比較します。
* `does not equal <value>`は未割り当ての数値属性に対して`true`と評価されます。

この`0.0`のデフォルトは未割り当ての数値属性が最初のオペランドの場合にのみ適用されます。第二オペランドが未割り当ての数値属性の場合、条件は訪問に一致しません。

## 集計属性のための拡張ルール条件の使用

[tally]()属性の場合、`contains`演算子を使用して特定のキーをチェックし、そのキーに関連付けられた値を評価することができます。


<blockquote>
この拡張ルール条件は`contains`演算子でのみ利用可能です。
</blockquote>


集計属性のための拡張条件を作成するには：

1. **Transform > Rules**に移動します。
1. ルールを追加するか、既存のルールを編集します。
1. **Conditions**の下で、評価する集計属性を選択します。
1. **contains**演算子を選択します。
1. **Custom Value**を選択します。
1. 評価する集計のキーを入力します。  
   ![](https://docs.tealium.com/images/server-side/tally-rule.png)
1. **Perform rule on value**をクリックし、キーに関連付けられた値を評価するために使用する演算子を選択します。
1. 比較する値を指定します。属性を選択するか、カスタム値を入力します。
1. **Save**をクリックします。
## 正規表現

`matches regex` 演算子は文字列属性にのみ使用可能です。属性値の任意の部分が正規表現と一致するとき、条件は `true` を返します。


<blockquote>
正規表現をスラッシュ(`/`)なしで入力してください。例えば、値 `abc1234567890` に完全に一致させる場合は、`^[a-z0-9]{13}$` と入力します。
</blockquote>


![](https://docs.tealium.com/images/server-side/audiences/regex_example_ui.png)

`matches regex` 演算子は以下のオプションを提供します：

* **複数行モード**：文字列全体の始まりと終わりだけでなく、各行の始まりと終わりで `^` と `$` に一致します。
* **大文字小文字を区別しない**：属性値に対する正規表現の一致時に文字の大文字と小文字を無視します。

以下の例は、値 `abc1234567890` に対する一般的な正規表現の結果を示しています：

| 正規表現            | 戻り値 | 説明                                              |
| ---------------- | ------ | ------------------------------------------------- |
| `\d{3}`          | `true` | 文字列のどこかで3つの連続する数字に一致します。 |
| `^abc`           | `true` | `^` は文字列の始まりに一致します。                 |
| `\d{3}$`         | `true` | `$` は文字列の終わりに一致します。                 |
| `^[a-z0-9]{13}$` | `true` | `^` と `$` は13文字の文字列全体に一致します。      |
| `^[a-zA-Z]{4}`   | `false`| 文字列は4つの連続する文字で始まりません。         |
| `[a-zA-Z]{4}$`   | `false`| 文字列は4つの連続する文字で終わりません。         |
| `^[a-z0-9]{15}$` | `false`| 文字列は15文字の長さではありません。              |