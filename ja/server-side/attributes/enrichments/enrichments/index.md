---
title: エンリッチメントについて
url: https://docs.tealium.com/ja/server-side/attributes/enrichments/enrichments/
---

エンリッチメントとは、属性を静的な値から動的な値に変換するためのカスタムロジックの使用を指します。これは新しいデータ値を作成したり、受信データを変更したりするために使用されます。各データタイプには事前に構築されたエンリッチメントが用意されています。例えば、数値属性には数値を増減する機能が用意されています。

## リンクされたエンリッチメント

2つ以上のエンリッチメントが同じ属性に依存している場合、それらは_リンクされたエンリッチメント_となります。以下の例は、訪問の開始と終了に適用されたエンリッチメントを示しています。`Visit Start`属性のエンリッチメントは`Visit End`属性を使用し、その逆も同様です。各エンリッチメントが属性によって他方にリンクされているため、それらはリンクされたエンリッチメントと見なされます。

![](https://docs.tealium.com/images/server-side/whiteui-usingenrichments-visitstart-and-visitend-linked-enrichments-combined-screens.png)
