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
&gt; product_name = [&#34;Nexus One&#34;, &#34;Samsung Razor&#34;, &#34;Apple iPhone&#34;]
[&#34;Nexus One&#34;, &#34;Samsung Razor&#34;, &#34;Apple iPhone&#34;]

&gt; product_name.toString()
&#34;Nexus One,Samsung Razor,Apple iPhone&#34;

&gt; product_name.toString().indexOf(&#34;Apple&#34;)
24
```