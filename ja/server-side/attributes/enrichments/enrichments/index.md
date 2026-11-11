---
title: エンリッチメントについて
url: https://docs.tealium.com/ja/server-side/attributes/enrichments/enrichments/
---

エンリッチメントとは、カスタムロジックを使用して属性を静的な値から動的な値に変換することです。新しいデータ値の作成や、受信データの変更に使用されます。各データ型には、事前定義されたエンリッチメントが用意されています。たとえば、数値属性では、数値を増減する機能を使用できます。

## リンクされたエンリッチメント

2つ以上のエンリッチメントが同じ属性に依存している場合、それらは「リンクされたエンリッチメント」になります。次の例は、訪問の開始時と終了時に適用されるエンリッチメントを示しています。`Visit Start`属性のエンリッチメントは`Visit End`属性を使用し、その逆も同様です。各エンリッチメントが属性によって相互にリンクされているため、リンクされたエンリッチメントとみなされます。

![](https://docs.tealium.com/images/server-side/whiteui-usingenrichments-visitstart-and-visitend-linked-enrichments-combined-screens.png)

## サイズ制限

属性の結合エンリッチメントなど、一部のエンリッチメントでは属性のサイズが増加する場合があります。Event StreamingおよびCustomer Data Platform（CDP）のほとんどの属性には保存容量の上限があり、その上限を超えた場合の動作も定められています。また、訪問プロファイルまたは訪問プロファイル全体には、圧縮および暗号化された状態で400 KBの上限があります。

詳細については、[属性について](https://docs.tealium.com/about-attributes/#size-limits)を参照してください。