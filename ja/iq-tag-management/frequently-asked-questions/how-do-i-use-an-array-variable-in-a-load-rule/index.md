---
title: 配列変数をロードルールで使用する方法は？
description: この記事では、ロードルールで配列変数を使用する方法について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/frequently-asked-questions/how-do-i-use-an-array-variable-in-a-load-rule/
---## 質問

ロードルールで、CONTAINSのような条件を持つ配列変数を使用できますか？

## 回答

はい。

ロードルールの条件によって生成されるJavaScriptコードは、`toString()` メソッドを使用します。これにより、配列はコンマ区切りの文字列に変換されます。たとえば、CONTAINS条件を使用するロードルールは、`toString()` を使用して変数を文字列に変換し、その後 `indexOf()` を使用して変数内で目的の値を見つけます。

```
> product_name = ["Nexus One", "Samsung Razor", "Apple iPhone"]
["Nexus One", "Samsung Razor", "Apple iPhone"]

> product_name.toString()
"Nexus One,Samsung Razor,Apple iPhone"

> product_name.toString().indexOf("Apple")
24
```